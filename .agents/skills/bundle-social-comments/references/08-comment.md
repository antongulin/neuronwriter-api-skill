# Comment

Tag: `comment` — 9 endpoints

---

## GET /api/v1/comment/

Get paginated comment list.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `teamId` | string | yes | — | Team ID |
| `postId` | string | no | — | Filter by post |
| `platform` | enum | no | — | Filter by platform |
| `socialAccountId` | string | no | — | Filter by account |
| `offset` | number | no | 0 | Pagination offset |
| `limit` | number | no | 10 | Max items |

**Response 200:**
```json
{ "items": [ /* comment objects */ ], "total": 100 }
```

---

## POST /api/v1/comment/

Create a new comment.

**Request Body:** Comment creation payload with platform-specific data.

**Response 200:** Created comment object.

---

## GET /api/v1/comment/{id}

Get a single comment.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Response 200:** Full comment object with details.

---

## PATCH /api/v1/comment/{id}

Update a comment.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Request Body:** Comment update payload.

**Response 200:** Updated comment object.

---

## DELETE /api/v1/comment/{id}

Delete a comment.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Response 200:** Deleted comment object.

---

## POST /api/v1/comment/import

Start a new comment import for a post.

**Request Body:**
```json
{
  "postId": "post_123",
  "teamId": "team_123"
}
```

**Response 200:** Import job object.

---

## GET /api/v1/comment/import

Get comment import list.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `teamId` | string | yes | — | Team ID |
| `postId` | string | no | — | Filter by post |
| `status` | enum | no | — | PENDING, FETCHING, RETRYING, COMPLETED, SKIPPED, FAILED, RATE_LIMITED |
| `offset` | number | no | 0 | Pagination offset |
| `limit` | number | no | 10 | Max items |

**Response 200:**
```json
{ "items": [ /* import objects */ ], "total": 5 }
```

---

## GET /api/v1/comment/import/{importId}

Get comment import by ID.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `importId` | string | yes |

**Response 200:** Import job object.

---

## GET /api/v1/comment/import/comments

Get fetched comments for a post.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `teamId` | string | yes | — | Team ID |
| `postId` | string | yes | — | Post ID |
| `platform` | enum | no | — | Filter by platform (FACEBOOK, INSTAGRAM, LINKEDIN, YOUTUBE, TIKTOK, REDDIT, THREADS, MASTODON, BLUESKY) |
| `socialAccountId` | string | no | — | Filter by account |
| `offset` | number | no | 0 | Pagination offset |
| `limit` | number | no | 10 | Max items |

**Response 200:**
```json
{ "items": [ /* comment objects */ ], "total": 50 }
```
