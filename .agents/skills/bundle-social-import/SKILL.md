---
name: bundle-social-import
description: >-
  Import historical social media posts and bulk-create posts via CSV using the Bundle.social API.
  Use this skill when importing past post history from connected social accounts (with optional comments and analytics),
  or when bulk-creating posts via CSV file upload on Bundle.social.
  Covers the full post history import workflow: start import → monitor status → retrieve imported posts → bulk delete.
  Covers the full CSV import workflow: upload CSV → check processing status → view row results.
  This skill should be triggered whenever a user mentions importing posts, importing history, CSV import,
  bulk posting, migrating content, or backfilling social media data into Bundle.social.
---

> **Author**: Anton Gulin · **Tool**: [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) · **GitHub**: [@antongulin](https://github.com/antongulin) · **Registry**: [skills.sh](https://www.skills.sh/docs)

# Bundle.social Import: Post History & CSV Bulk Import

This skill covers two import workflows on Bundle.social: importing historical post data from connected social accounts, and bulk-creating posts via CSV upload.

## Authentication

```
x-api-key: <your-api-key>
```

Base URL: `https://api.bundle.social`

## Reference Docs

Read `references/README.md` for platform enums and standard errors.
Read `references/10-post-import.md` for post history import endpoints.
Read `references/11-post-csv-import.md` for CSV import endpoints.

## How to Use This Skill

IMPORTANT: Never try to call the Bundle.social API directly. Always generate curl command examples with `<your-api-key>` as the auth header placeholder.

### Post History Import

When a user wants to bring in historical posts from a connected social account:

1. **Start the import**: `POST /api/v1/post-history-import/` with `teamId`, `socialAccountId`, optional date range
2. **Monitor progress**: `GET /api/v1/post-history-import/` to see all imports, filterable by team/account/status
3. **Check specific import**: `GET /api/v1/post-history-import/{importId}` for detailed status
4. **View results**: `GET /api/v1/post-history-import/posts` to see imported posts with analytics
5. **Clean up**: `DELETE /api/v1/post-history-import/posts` to bulk delete imported posts
6. **Retry failures**: `POST /api/v1/post-history-import/{importId}/retry`

### CSV Import

When a user wants to bulk-create posts from a CSV file:

1. **Upload CSV**: `POST /api/v1/post-csv-import/` with `multipart/form-data` containing the CSV
2. **Check status**: `GET /api/v1/post-csv-import/{importId}/status` for processing status
3. **View results**: `GET /api/v1/post-csv-import/{importId}/rows` with optional `status` filter (SUCCESS/FAILED)
4. **Browse history**: `GET /api/v1/post-csv-import/` to see all CSV imports

## Endpoint Reference Summary

### Post History Import
- `POST /api/v1/post-history-import/` — Start import (supports `dateFrom`, `dateTo`, `importComments`, `importAnalytics`)
- `GET /api/v1/post-history-import/` — List imports (filterable by `teamId`, `socialAccountId`, `status`)
- `GET /api/v1/post-history-import/{importId}` — Get import by ID
- `GET /api/v1/post-history-import/posts` — Get imported posts with analytics
- `DELETE /api/v1/post-history-import/posts` — Bulk delete imported posts
- `POST /api/v1/post-history-import/{importId}/retry` — Retry failed import

### Post CSV Import
- `POST /api/v1/post-csv-import/` — Upload CSV (multipart/form-data)
- `GET /api/v1/post-csv-import/` — List CSV imports
- `GET /api/v1/post-csv-import/{importId}` — Get CSV import details
- `GET /api/v1/post-csv-import/{importId}/status` — Get processing status
- `GET /api/v1/post-csv-import/{importId}/rows` — Get row results (filterable by SUCCESS/FAILED)

## Common Patterns

1. **Full history migration**: Connect account → Start import → Poll until complete → View imported posts
2. **Analytics backfill**: Start import with `importAnalytics: true` → Get posts with historical analytics data
3. **CSV bulk posting**: Prepare CSV → Upload → Monitor status → View failed rows and fix errors
4. **Retry loop**: Import fails → Check status → Fix underlying issue → Retry → Monitor
5. **Cleanup after migration**: Verify imported posts → Bulk delete if re-import needed

## CSV Import Notes

- The CSV format determines the post structure — each row becomes one post
- After upload, processing is async — poll the status endpoint
- Row results show per-row success/failure with error messages and normalized payloads
- The CSV import has a `PENDING` initial status that transitions as processing begins

## Error Handling

- Imports can fail due to platform rate limits, authentication issues, or invalid data
- Always check the `error` field on failed imports
- CSV row failures include detailed error messages — use them to fix and re-upload
- Retry endpoint only works on failed imports
