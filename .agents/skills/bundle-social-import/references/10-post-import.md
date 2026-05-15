# Post History Import

Tag: `postImport` — 6 endpoints

---

## POST /api/v1/post-history-import/

Start a new post history import.

**Request Body:**
```json
{
  "teamId": "team_123",
  "socialAccountId": "acc_123",
  "dateFrom": "2024-01-01",    // optional
  "dateTo": "2024-12-31",      // optional
  "importComments": true,       // optional
  "importAnalytics": true       // optional
}
```

**Response 200:** Import job object.

---

## GET /api/v1/post-history-import/

Get import status list.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `teamId` | string | no | — | Filter by team |
| `socialAccountId` | string | no | — | Filter by account |
| `status` | string | no | — | Filter by status |
| `offset` | number | no | 0 | Pagination offset |
| `limit` | number | no | 10 | Max items |

**Response 200:**
```json
{ "items": [ /* import objects */ ], "total": 5 }
```

---

## GET /api/v1/post-history-import/{importId}

Get import by ID.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `importId` | string | yes |

**Response 200:** Import job object.

---

## GET /api/v1/post-history-import/posts

Get imported posts with analytics for a social account.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `socialAccountId` | string | yes | — | Account ID |
| `teamId` | string | yes | — | Team ID |
| `offset` | number | no | 0 | Pagination offset |
| `limit` | number | no | 10 | Max items |

**Response 200:**
```json
{ "items": [ /* imported post objects */ ], "total": 50 }
```

---

## DELETE /api/v1/post-history-import/posts

Bulk delete imported posts and their analytics.

**Request Body:**
```json
{
  "postIds": ["post_123", "post_456"],
  "teamId": "team_123"
}
```

**Response 200:** Deletion confirmation.

---

## POST /api/v1/post-history-import/{importId}/retry

Retry a failed import.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `importId` | string | yes |

**Request Body:**
```json
{ "teamId": "team_123" }
```

**Response 200:** Retried import object.
