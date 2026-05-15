# Bundle.social API Documentation

**Base URL:** `https://api.bundle.social`
**API Version:** 1.0.0
**OpenAPI:** 3.0.2

## Authentication

All endpoints require authentication via the `x-api-key` header.

## Supported Platforms

| Platform | Enum Value |
|----------|-----------|
| Facebook | `FACEBOOK` |
| Instagram | `INSTAGRAM` |
| TikTok | `TIKTOK` |
| YouTube | `YOUTUBE` |
| Twitter/X | `TWITTER` |
| Pinterest | `PINTEREST` |
| Reddit | `REDDIT` |
| Mastodon | `MASTODON` |
| Discord | `DISCORD` |
| Slack | `SLACK` |
| Bluesky | `BLUESKY` |
| Google Business | `GOOGLE_BUSINESS` |
| LinkedIn | `LINKEDIN` |
| Threads | `THREADS` |

## Standard Error Responses

All endpoints share these common error responses:

| Status | Description |
|--------|-------------|
| `400` | Validation error — includes Zod validation `issues` array |
| `401` | Unauthorized — missing or invalid API key |
| `403` | Forbidden — insufficient permissions |
| `404` | Resource not found |
| `429` | Rate limited |
| `500` | Internal server error |

Error body format:
```json
{
  "statusCode": 400,
  "message": "Validation error",
  "issues": [
    { "code": "invalid_type", "message": "Expected string, received number", "path": ["fieldName"] }
  ]
}
```

## Endpoints Index

| # | Tag | Count | File |
|---|-----|-------|------|
| 1 | `app` | 1 | [01-app.md](./01-app.md) |
| 2 | `organization` | 5 | [02-organization.md](./02-organization.md) |
| 3 | `team` | 5 | [03-team.md](./03-team.md) |
| 4 | `socialAccount` | 11 | [04-social-account.md](./04-social-account.md) |
| 5 | `upload` | 8 | [05-upload.md](./05-upload.md) |
| 6 | `post` | 6 | [06-post.md](./06-post.md) |
| 7 | `analytics` | 7 | [07-analytics.md](./07-analytics.md) |
| 8 | `comment` | 9 | [08-comment.md](./08-comment.md) |
| 9 | `misc` | 48 | [09-misc.md](./09-misc.md) |
| 10 | `postImport` | 6 | [10-post-import.md](./10-post-import.md) |
| 11 | `postCSV` | 5 | [11-post-csv-import.md](./11-post-csv-import.md) |

**Total: 111 endpoints** (down from 144 in raw spec — misc platform endpoints collapsed into one file)
