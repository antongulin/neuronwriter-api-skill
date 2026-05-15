---
name: bundle-social-accounts
description: >-
  Manage Bundle.social social account connections across 14 platforms using the Bundle.social API.
  Use this skill when connecting, disconnecting, configuring channels, or managing social accounts on Bundle.social.
  Covers OAuth connection flow, disconnection, channel setup (Discord/Slack channels, Reddit subreddits),
  portal links, connection checks, profile refreshes, copying accounts between teams, and listing accounts by platform type.
  Supports Facebook, Instagram, TikTok, YouTube, Twitter/X, Pinterest, Reddit, Mastodon, Discord, Slack, Bluesky, Google Business, LinkedIn, and Threads.
  This skill should be triggered whenever a user says "connect", "disconnect", "social account", "OAuth", "channel", "portal link", or mentions linking any social media platform to Bundle.social.
---

> **Author**: Anton Gulin · **Tool**: [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) · **GitHub**: [@antongulin](https://github.com/antongulin) · **Registry**: [skills.sh](https://www.skills.sh/docs)

# Bundle.social Social Accounts

This skill covers managing social account connections on Bundle.social — the critical bridge between Bundle.social and your social media platforms.

## Authentication

All requests require the `x-api-key` header:
```
x-api-key: <your-api-key>
```

Base URL: `https://api.bundle.social`

## Reference Docs

Read `references/README.md` for platform enums and error standards.
Read `references/04-social-account.md` for all endpoint details.

## How to Use This Skill

When a user asks about connecting or managing social accounts in Bundle.social:

1. **Identify the platform** — use the enum value from the platforms table in `references/README.md`
2. **Read the reference doc** for the specific operation (connect, disconnect, set channel, etc.)
3. **Generate curl command examples** with `<your-api-key>` as placeholder (NEVER call the API — you won't have credentials)
4. **Explain OAuth flow** when the user connects — the connect endpoint returns a URL they need to visit in a browser

### Key Concepts

- **OAuth Connection Flow**: The `POST /api/v1/social-account/connect` endpoint generates an OAuth URL. The user must visit this URL in a browser to authorize. Bundle.social doesn't store credentials — it uses OAuth tokens.
- **Channels**: Discord servers/channels, Slack channels, Reddit subreddits are managed via `set-channel`/`unset-channel` endpoints.
- **Platform-specific fields**: Mastodon/Bluesky need a `serverUrl`; Instagram supports `instagramConnectionMethod` (FACEBOOK or INSTAGRAM).

## Endpoint Reference Summary

### Connection
- `POST /api/v1/social-account/connect` — Generate OAuth URL. Requires `type`, `teamId`, `redirectUrl`
- `DELETE /api/v1/social-account/disconnect` — Disconnect and remove from scheduled posts

### Channel Management
- `POST /api/v1/social-account/set-channel` — Set channel (server/channel/subreddit)
- `POST /api/v1/social-account/unset-channel` — Remove channel
- `POST /api/v1/social-account/refresh-channels` — Refresh available channels

### Maintenance
- `POST /api/v1/social-account/create-portal-link` — Create portal link for account management
- `POST /api/v1/social-account/connection-check` — Run connection/disconnect check
- `POST /api/v1/social-account/profile-refresh` — Refresh profile info from platform

### Queries
- `GET /api/v1/social-account/by-type` — Get account by team + platform type
- `POST /api/v1/social-account/copy` — Copy accounts to another team
- `GET /api/v1/social-account/to-delete` — List accounts scheduled for deletion

## Common Patterns

1. **Full connection flow**: Get org → Create team → Connect account (get OAuth URL) → User authorizes → Verify by getting account by type
2. **Channel setup**: Connect Discord/Slack/Reddit → Set channel → Refresh channels to confirm
3. **Account maintenance**: Periodically run connection checks and profile refreshes
4. **Cleanup**: Schedule disconnection, verify with to-delete list

## Error Handling

- 400: Validation error — check the `issues` array for field-level errors
- 401: Check your API key
- 404: Account not found — verify the ID and team
- Always check platform-specific error messages in the response
