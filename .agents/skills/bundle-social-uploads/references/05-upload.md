# Upload

Tag: `upload` — 8 endpoints

---

## GET /api/v1/upload/

Get paginated upload list.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `teamId` | string | no | — | Filter by team |
| `type` | enum | no | — | `image`, `video`, or `other` |
| `search` | string | no | — | Search by filename |
| `offset` | number | no | 0 | Pagination offset |
| `limit` | number | no | 20 | Max items |

**Response 200:** Paginated list of upload objects.

---

## POST /api/v1/upload/

Upload a file.

**Request Body:** `multipart/form-data`
- `file` (binary, required)

**Response 200:** Created upload object.

---

## GET /api/v1/upload/{id}

Get single upload.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Response 200:** Upload object.

---

## DELETE /api/v1/upload/{id}

Delete single upload.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Response 200:** Deleted upload object.

---

## DELETE /api/v1/upload/

Bulk delete uploads.

**Request Body:**
```json
{ "ids": ["up_123", "up_456"] }
```

**Response 200:** Deletion confirmation.

---

## POST /api/v1/upload/from-url

Create upload from a remote URL.

**Request Body:**
```json
{
  "url": "https://example.com/image.jpg",
  "teamId": "team_123"
}
```

**Response 200:** Created upload object.

---

## POST /api/v1/upload/init

Initialize a large file upload (multipart).

**Request Body:**
```json
{
  "fileName": "video.mp4",
  "fileSize": 104857600,
  "mimeType": "video/mp4",
  "teamId": "team_123"
}
```

**Response 200:** Upload session info with `uploadUrl`.

---

## POST /api/v1/upload/finalize

Finalize a large file upload after all parts are uploaded.

**Request Body:**
```json
{
  "uploadId": "up_123",
  "fileId": "file_123",
  "parts": [
    { "ETag": "\"etag1\"", "PartNumber": 1 },
    { "ETag": "\"etag2\"", "PartNumber": 2 }
  ]
}
```

**Response 200:** Finalized upload object.
