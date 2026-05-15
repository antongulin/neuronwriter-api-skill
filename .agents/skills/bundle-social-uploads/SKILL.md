---
name: bundle-social-uploads
description: >-
  Upload and manage media files for social media posts using the Bundle.social Upload API.
  Use this skill when uploading images/videos for social media content, creating uploads from URLs,
  handling large file multipart uploads, listing existing uploads, or deleting media on Bundle.social.
  Covers direct file upload, URL-based upload, multipart large file upload (init → upload parts → finalize),
  upload listing/searching, and single/bulk deletion.
  This skill should be triggered whenever a user mentions uploading files, images, videos, media assets,
  or attaching media to Bundle.social posts — even if they just say "I need to upload an image for my post."
---

> **Author**: Anton Gulin · **Tool**: [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) · **GitHub**: [@antongulin](https://github.com/antongulin) · **Registry**: [skills.sh](https://www.skills.sh/docs)

# Bundle.social Uploads

This skill covers media file upload and management on Bundle.social.

## Authentication

```
x-api-key: <your-api-key>
```

Base URL: `https://api.bundle.social`

## Reference Docs

Read `references/README.md` for platform enums and standard errors.
Read `references/05-upload.md` for endpoint details.

## How to Use This Skill

When a user needs to upload or manage media files:

1. **Determine upload type** — direct file, URL import, or large file multipart
2. **Read the reference doc** for the specific endpoint
3. **Generate curl command examples** with `<your-api-key>` as placeholder (NEVER call the actual API)
4. **Return the upload ID** — the user will need it for creating posts (cross-reference with `bundle-social-posts` skill)

### Upload Types

#### Direct Upload (small/medium files)
`POST /api/v1/upload/` with `multipart/form-data` containing the file.
Best for images and short videos under ~100MB.

#### URL Import (files already online)
`POST /api/v1/upload/from-url` — Bundle.social fetches the file from a URL.
Useful when the file is already hosted somewhere accessible.

#### Multipart Upload (large files)
For files over ~100MB, use the three-step process:
1. `POST /api/v1/upload/init` — Initialize with `fileName`, `fileSize`, `mimeType`, `teamId`
2. Upload parts to the returned `uploadUrl` (standard S3 multipart upload)
3. `POST /api/v1/upload/finalize` — Finalize with ETags and PartNumbers

## Endpoint Reference Summary

- `GET /api/v1/upload/` — List uploads (filterable by `teamId`, `type`, `search`)
- `POST /api/v1/upload/` — Upload file (multipart/form-data)
- `GET /api/v1/upload/{id}` — Get single upload
- `DELETE /api/v1/upload/{id}` — Delete single upload
- `DELETE /api/v1/upload/` — Bulk delete uploads
- `POST /api/v1/upload/from-url` — Create upload from remote URL
- `POST /api/v1/upload/init` — Initialize large file upload
- `POST /api/v1/upload/finalize` — Finalize multipart upload

## Common Patterns

1. **Simple post with image**: Upload file → Get upload ID → Create post with upload ID as media
2. **Import from web**: Found an image online → Use from-url → Get upload ID → Use in post
3. **Large video upload**: Init → Upload parts (client-side) → Finalize → Use in post
4. **Media management**: List uploads by team → Search by filename → Delete old/unused files
5. **Bulk cleanup**: List uploads → Bulk delete old/unused media

## Important Notes

- Upload endpoint uses `multipart/form-data` — not JSON
- For `from-url`, Bundle.social fetches the file server-side
- Multipart upload follows S3 conventions — parts can be uploaded in parallel
- Check org upload usage before uploading large files
- Upload type enum: `image`, `video`, `other`
