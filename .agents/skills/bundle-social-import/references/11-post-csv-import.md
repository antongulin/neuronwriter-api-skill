# Post CSV Import

Tag: `postCSV` — 5 endpoints

---

## POST /api/v1/post-csv-import/

Upload CSV for async bulk post import.

**Request Body:** `multipart/form-data`
- `file` (binary, required) — CSV file with post data

**Response 201:**
```json
{
  "status": "PENDING",
  "fileName": "posts.csv",
  "totalRows": 100,
  "processedRows": 0,
  "successRows": 0,
  "failedRows": 0,
  "error": null,
  "createdAt": "2024-01-01T00:00:00Z",
  "updatedAt": "2024-01-01T00:00:00Z"
}
```

---

## GET /api/v1/post-csv-import/

Get CSV import history.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `teamId` | string | no | — | Filter by team |
| `status` | string | no | — | Filter by status |
| `offset` | number | no | 0 | Pagination |
| `limit` | number | no | 10 | Max items |

**Response 200:** `{ items: [CSV import objects], total }`

---

## GET /api/v1/post-csv-import/{importId}

Get CSV import details.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `importId` | string | yes |

**Response 200:** CSV import object (status, fileName, row counts, error, timestamps).

---

## GET /api/v1/post-csv-import/{importId}/status

Get CSV import processing status.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `importId` | string | yes |

**Response 200:** Processing status object.

---

## GET /api/v1/post-csv-import/{importId}/rows

Get CSV import row results.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `importId` | string | yes |

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `status` | enum | no | — | Filter: `SUCCESS` or `FAILED` |
| `offset` | number | no | 0 | Pagination offset |
| `limit` | number | no | 10 | Max items |

**Response 200:**
```json
{
  "items": [
    {
      "id": "row_123",
      "importId": "csv_123",
      "rowNumber": 5,
      "status": "SUCCESS",
      "postId": "post_123",
      "rawRow": { "title": "...", "content": "..." },
      "normalizedPayload": {},
      "error": null,
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ],
  "total": 100
}
```
