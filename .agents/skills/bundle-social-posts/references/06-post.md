# Post

Tag: `post` — 6 endpoints

---

## GET /api/v1/post/

Get paginated post list.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `teamId` | string | no | — | Filter by team |
| `status` | string | no | — | Filter by post status |
| `offset` | number | no | 0 | Pagination offset |
| `limit` | number | no | 10 | Max items |
| `search` | string | no | — | Search posts |

**Response 200:**
```json
{
  "items": [ /* post objects */ ],
  "pagination": { "page": 1, "pageSize": 10, "total": 100, "totalPages": 10 }
}
```

---

## POST /api/v1/post/

Create a new post. The body contains platform-specific content data for each target platform.

**Request Body:** Post creation payload (complex — includes per-platform content blocks for text, media, scheduling, and platform-specific options).

**Response 200:** Created post object.

---

## GET /api/v1/post/{id}

Get a single post with full platform data.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Response 200:** Full post object with all platform-specific content data.

---

## PATCH /api/v1/post/{id}

Update an existing post.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Request Body:** Post update payload (various platform-specific fields).

**Response 200:** Updated post object.

---

## DELETE /api/v1/post/{id}

Delete a post.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Response 200:** Deleted post object.

---

## POST /api/v1/post/{id}/retry

Retry publishing a failed post.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Response 200:** Retried post object.
