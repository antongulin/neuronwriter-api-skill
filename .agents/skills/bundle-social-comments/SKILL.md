---
name: bundle-social-comments
description: >-
  Manage social media comments across 10+ platforms using the Bundle.social API.
  Use this skill when reading, creating, updating, deleting comments, or importing comment threads
  from Facebook, Instagram, LinkedIn, YouTube, TikTok, Reddit, Threads, Mastodon, and Bluesky via Bundle.social.
  Covers comment CRUD and the full comment import workflow: start import → check status → retrieve fetched comments.
  This skill should be triggered whenever a user mentions comments, replies, engagements, comment imports,
  or conversation management on Bundle.social-connected accounts.
---

> **Author**: Anton Gulin · **Tool**: [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) · **GitHub**: [@antongulin](https://github.com/antongulin) · **Registry**: [skills.sh](https://www.skills.sh/docs)

# Bundle.social Comments

This skill covers managing comments and importing comment threads on Bundle.social.

## Authentication

```
x-api-key: <your-api-key>
```

Base URL: `https://api.bundle.social`

## Reference Docs

Read `references/README.md` for platform enums and standard errors.
Read `references/08-comment.md` for endpoint details.

## How to Use This Skill

When a user asks to manage comments or import comment threads:

1. **Identify the operation** — CRUD on individual comments, or bulk import of comment threads
2. **Read the reference doc** for the relevant endpoint
3. **Generate curl command examples** with `<your-api-key>` as placeholder (NEVER call the actual API)
4. **For imports**, guide the user through the multi-step flow

### Comment Import Flow

Importing comment threads is a multi-step async process:

1. **Start import**: `POST /api/v1/comment/import` with `postId` and `teamId`
2. **Monitor progress**: `GET /api/v1/comment/import` to see import jobs and their status
3. **Check specific job**: `GET /api/v1/comment/import/{importId}`
4. **Retrieve results**: `GET /api/v1/comment/import/comments` to get all fetched comments

Import statuses: `PENDING`, `FETCHING`, `RETRYING`, `COMPLETED`, `SKIPPED`, `FAILED`, `RATE_LIMITED`

## Endpoint Reference Summary

### Comment CRUD
- `GET /api/v1/comment/` — List comments (filterable by `teamId`, `postId`, `platform`, `socialAccountId`)
- `POST /api/v1/comment/` — Create a new comment (platform-specific payload)
- `GET /api/v1/comment/{id}` — Get single comment
- `PATCH /api/v1/comment/{id}` — Update comment
- `DELETE /api/v1/comment/{id}` — Delete comment

### Comment Import
- `POST /api/v1/comment/import` — Start comment import for a post
- `GET /api/v1/comment/import` — List import jobs
- `GET /api/v1/comment/import/{importId}` — Get import job by ID
- `GET /api/v1/comment/import/comments` — Get fetched comments for a post

## Common Patterns

1. **Comment moderation workflow**: List comments by post → Read individual comments → Reply or delete
2. **Import workflow**: Start import → Poll status until COMPLETED → Retrieve comments
3. **Filtering**: Use platform filter to see comments from specific platforms; use postId to narrow to specific content
4. **Rate limits**: Comment imports can hit platform rate limits — watch for `RATE_LIMITED` status and retry

## Platform Support for Comments

Comment operations are supported on: Facebook, Instagram, LinkedIn, YouTube, TikTok, Reddit, Threads, Mastodon, Bluesky
