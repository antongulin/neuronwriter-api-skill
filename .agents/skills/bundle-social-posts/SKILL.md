---
name: bundle-social-posts
description: >-
  Create, read, update, delete, and retry publishing social media posts across 14 platforms using the Bundle.social API.
  Use this skill when creating multi-platform posts, scheduling content, checking post status, updating published posts,
  deleting posts, or retrying failed publishes on Bundle.social.
  Covers the full post lifecycle: draft → schedule → publish → retry-on-failure → edit → delete.
  Handles per-platform content blocks, status tracking, post search, and pagination.
  This skill should be triggered whenever a user mentions posting, scheduling, publishing, creating content, or managing posts on Bundle.social.
  Essential for daily social media content workflows.
---

> **Author**: Anton Gulin · **Tool**: [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) · **GitHub**: [@antongulin](https://github.com/antongulin) · **Registry**: [skills.sh](https://www.skills.sh/docs)

# Bundle.social Posts

This skill covers the full lifecycle of social media posts on Bundle.social — from creation through publishing, editing, and deletion.

## Authentication

```
x-api-key: <your-api-key>
```

Base URL: `https://api.bundle.social`

## Reference Docs

Read `references/README.md` for platform enums and standard errors.
Read `references/06-post.md` for endpoint details.

## How to Use This Skill

When a user asks to create, schedule, or manage posts on Bundle.social:

1. **Understand the post structure** — Posts contain platform-specific content blocks. Each target platform gets its own content configuration (text, media, scheduling).
2. **Read the reference doc** for the operation needed
3. **Generate curl command examples** with `<your-api-key>` as placeholder (NEVER call the actual API)
4. **Interpret the response** — explain post status, platform delivery status, any errors

### Post Data Model

A post in Bundle.social has:
- **Common fields**: `id`, `teamId`, `title`, `status`, scheduling info
- **Platform-specific data**: Per-platform content blocks with text, media attachments, and platform options
- **Statuses**: draft, scheduled, publishing, published, failed, etc.

### Creating Posts

The `POST /api/v1/post/` endpoint accepts a complex payload. The exact shape depends on which platforms you're posting to. Help the user construct the right payload by:

1. Identifying target platforms (e.g., Instagram + Facebook + LinkedIn)
2. Building platform-specific content blocks (text, images, videos, links)
3. Setting scheduling options (publish now or schedule for later)
4. Adding any platform-specific options (e.g., TikTok comments, Instagram first comment)

## Endpoint Reference Summary

- `GET /api/v1/post/` — List posts (supports `teamId`, `status`, `offset`, `limit`, `search`)
- `POST /api/v1/post/` — Create a new post (complex payload with per-platform content)
- `GET /api/v1/post/{id}` — Get single post with full platform data
- `PATCH /api/v1/post/{id}` — Update post (edit content, reschedule)
- `DELETE /api/v1/post/{id}` — Delete a post
- `POST /api/v1/post/{id}/retry` — Retry publishing a failed post

## Common Patterns

1. **Create and publish**: Build content → Create post → Check status via GET
2. **Schedule workflow**: Create post with future schedule → Verify via list with status filter → Edit if needed
3. **Retry on failure**: Check post status → Identify failed platforms → Retry → Monitor
4. **Multi-platform posting**: One post object can target multiple platforms. Each platform gets its own content config.
5. **Search and filter**: Use the search parameter and status filter to find specific posts in large collections

## Error Handling

- Failed posts have a `failed` status — use the retry endpoint
- Check `issues` array in 400 responses for validation errors
- Rate limits (429) are per-organization — check org usage before bulk operations
- Platform-specific publishing errors appear in the post's platform data
