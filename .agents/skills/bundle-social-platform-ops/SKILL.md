---
name: bundle-social-platform-ops
description: >-
  Execute platform-specific social media operations across 13 platforms using the Bundle.social API.
  Use for actions beyond general posting: YouTube playlists/thumbnails/video management;
  LinkedIn mentions; Google Business Profile (hours, attributes, services, reviews, menus);
  Reddit post requirements/flairs; Instagram tag/location search; Facebook recommendations;
  Pinterest/Mastodon/Slack/Bluesky/Twitter/Discord/TikTok operations.
  Trigger on mentions of "YouTube playlist", "Google Business hours", "LinkedIn mentions",
  "Reddit flairs", "GBP reviews", "TikTok music", or any platform-specific social media management.
---

> **Author**: Anton Gulin · **Tool**: [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) · **GitHub**: [@antongulin](https://github.com/antongulin) · **Registry**: [skills.sh](https://www.skills.sh/docs)

# Bundle.social Platform Operations

This skill covers platform-specific operations on Bundle.social — the 48 misc endpoints that handle unique features of each social platform.

## Authentication

```
x-api-key: <your-api-key>
```

Base URL: `https://api.bundle.social`

## Reference Docs

Read `references/README.md` for platform enums and standard errors.
Read `references/09-misc.md` for all endpoint details organized by platform.

## How to Use This Skill

When a user asks to do something platform-specific (not general posting/commenting):

1. **Identify the platform** — YouTube, LinkedIn, Google Business, Reddit, Instagram, Facebook, Pinterest, Mastodon, Slack, Bluesky, Twitter, Discord, or TikTok
2. **Read `references/09-misc.md`** to find the relevant endpoint(s)
3. **Generate curl command examples** with `<your-api-key>` as placeholder (NEVER call the actual API)
4. **Explain platform-specific concepts** — e.g., YouTube privacy statuses, GBP location profiles, LinkedIn URNs

## Platform Endpoints by Category

### YouTube — 12 endpoints
Playlist management (CRUD + items), video metadata editing, thumbnail setting, video/comment deletion, video categories, regions
- `POST /api/v1/misc/youtube/thumbnail` — Set video thumbnail
- `GET|POST|PUT|DELETE /api/v1/misc/youtube/playlist[*]` — Playlist CRUD
- `POST|DELETE /api/v1/misc/youtube/playlist-items[*]` — Playlist item management
- `PATCH|DELETE /api/v1/misc/youtube/video` — Edit/delete video
- `PATCH|DELETE /api/v1/misc/youtube/comment` — Edit/delete comment
- `GET /api/v1/misc/youtube/video-categories` — Get categories
- `GET /api/v1/misc/youtube/regions` — Get regions

### LinkedIn — 6 endpoints
Mentions, post/comment editing
- `GET /api/v1/misc/linkedin/mentions/tags` — Search mentionable people/orgs
- `POST /api/v1/misc/linkedin/mentions/builder` — Build text with @mentions
- `PATCH|DELETE /api/v1/misc/linkedin/post` — Edit/delete post
- `PATCH|DELETE /api/v1/misc/linkedin/comment` — Edit/delete comment

### Google Business — 19 endpoints
The largest set: media, location profile, hours, attributes, categories, services, food menus, place action links, reviews
- **Media**: add, list, delete photos/videos
- **Location**: get/update profile, hours (regular/special/more), attributes, available attributes, available categories
- **Services**: get/update service list
- **Food menus**: get/update menus
- **Place action links**: CRUD (book, order, etc.)
- **Reviews**: import, list, reply to reviews

### Reddit — 6 endpoints
- `GET /api/v1/misc/reddit/post-requirements` — Check subreddit rules/flair requirements
- `GET /api/v1/misc/reddit/subreddit-flairs` — Get available flairs
- `PATCH|DELETE /api/v1/misc/reddit/post` — Edit/delete post
- `PATCH|DELETE /api/v1/misc/reddit/comment` — Edit/delete comment

### Facebook — 9 endpoints
- **Recommendations**: import, list, reply to recommendations and thread comments
- **Posts**: edit/delete
- **Comments**: edit/delete

### Other Platforms
- **Instagram** (3): tag search, location search, comment deletion
- **Pinterest** (2): edit/delete pin
- **Mastodon** (4): edit/delete status, edit/delete comment
- **Slack** (2): edit/delete message
- **Bluesky** (2): delete post, delete comment
- **Twitter/X** (1): delete tweet
- **Discord** (1): delete message
- **TikTok** (2): trending music list, delete comment

## Common Patterns

1. **Find platform info first**: For YouTube, get categories/regions before creating. For Reddit, check post requirements before posting.
2. **GBP management**: Full location profile workflow — get profile → update hours → manage services → handle reviews
3. **LinkedIn mentions**: Search tags → Build text with mentions → Use in post
4. **Review management**: Import reviews → List → Reply to reviews
5. **Content cleanup**: Edit or delete platform-specific content as needed

## Important Notes

- Google Business has the most endpoints (19) — pay special attention here
- Some endpoints may be DISABLED (like Pinterest edit pin) — check the reference doc
- TikTok trending music has 40+ genre options and 3 date ranges
- Facebook recommendations are separate from regular comments
