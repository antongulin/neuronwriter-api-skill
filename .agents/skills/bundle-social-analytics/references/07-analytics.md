# Analytics

Tag: `analytics` — 7 endpoints

---

## GET /api/v1/analytics/social-account

Get analytics for a social account.

**Query Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `socialAccountId` | string | yes | Account ID |
| `teamId` | string | yes | Team ID |
| `dateFrom` | string | no | Start date |
| `dateTo` | string | no | End date |
| `granularity` | string | no | Aggregation level |

**Response 200:** Analytics data object with metrics:
- Impressions, views, likes, comments, shares, saves
- Follower count, engagement rate
- Per-platform specific metrics

---

## GET /api/v1/analytics/social-account/raw

Get raw analytics data for a social account.

**Query Parameters:** Same as above.

**Response 200:** Raw analytics data array.

---

## POST /api/v1/analytics/social-account/force

Force refresh analytics for a social account.

**Request Body:**
```json
{
  "socialAccountId": "acc_123",
  "teamId": "team_123"
}
```

**Response 200:** Force refresh initiated confirmation.

---

## GET /api/v1/analytics/post

Get analytics for a specific post.

**Query Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `postId` | string | yes | Post ID |
| `teamId` | string | yes | Team ID |
| `dateFrom` | string | no | Start date |
| `dateTo` | string | no | End date |

**Response 200:**
```json
{
  "post": { "id": "post_123", "teamId": "team_123", "title": "...", "status": "...", "data": {} },
  "analytics": [ /* per-platform analytics with metrics */ ]
}
```

---

## GET /api/v1/analytics/post/raw

Get raw analytics data for a post.

**Query Parameters:** Same as above.

**Response 200:**
```json
{
  "post": { "id": "post_123", "teamId": "team_123", "title": "...", "status": "...", "data": {} },
  "analytics": [ /* raw per-platform analytics */ ]
}
```

---

## GET /api/v1/analytics/post/bulk

Retrieve analytics for multiple posts in a single request. Max 60 posts, paginated 20 per page.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `postIds` | string[] | yes | — | Post IDs (1-60) |
| `platformType` | enum | yes | — | Platform type (11 platforms) |
| `page` | number | no | 1 | Page number |
| `limit` | number | no | 20 | Items per page (max 20) |

**Response 200:**
```json
{
  "results": [
    {
      "postId": "post_123",
      "items": [
        {
          "id": "anal_123",
          "profilePostId": "pp_123",
          "impressions": 1000,
          "impressionsUnique": 800,
          "views": 500,
          "viewsUnique": 400
        }
      ]
    }
  ]
}
```

---

## POST /api/v1/analytics/post/force

Force refresh analytics for a post.

**Request Body:**
```json
{ "postId": "post_123" }
```

**Response 200:** Force refresh initiated confirmation.
