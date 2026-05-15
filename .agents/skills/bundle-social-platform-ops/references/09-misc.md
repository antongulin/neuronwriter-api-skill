# Misc — Platform-Specific Operations

Tag: `misc` — 48 endpoints across 13 platforms

---

## YouTube (12 endpoints)

### `POST /api/v1/misc/youtube/thumbnail`
Set or change thumbnail for a YouTube video.
```json
{ "videoId": "vid_123", "uploadId": "up_123", "teamId": "team_123" }
```

### `GET /api/v1/misc/youtube/playlist`
Get channel playlists. Query: `teamId` (required), `offset`, `limit`.

### `POST /api/v1/misc/youtube/playlist`
Create a new playlist.
```json
{ "teamId": "team_123", "title": "My Playlist", "description": "...", "privacyStatus": "PUBLIC" }
```

### `PUT /api/v1/misc/youtube/playlist`
Update a playlist.
```json
{ "playlistId": "pl_123", "teamId": "team_123", "title": "...", "description": "...", "privacyStatus": "PUBLIC" }
```

### `DELETE /api/v1/misc/youtube/playlist/{playlistId}`
Delete a playlist. Body: `{ "teamId": "team_123" }`

### `POST /api/v1/misc/youtube/playlist-items`
Add a video to a playlist.
```json
{ "playlistId": "pl_123", "videoId": "vid_123", "teamId": "team_123" }
```

### `GET /api/v1/misc/youtube/playlist-items`
Get videos from a playlist. Query: `playlistId` (required), `teamId` (required), `offset`, `limit`.

### `DELETE /api/v1/misc/youtube/playlist-items/{playlistItemId}`
Remove a video from a playlist. Body: `{ "teamId": "team_123" }`

### `PATCH /api/v1/misc/youtube/video`
Edit YouTube video metadata.
```json
{ "videoId": "vid_123", "teamId": "team_123", "title": "...", "description": "...", "tags": ["tag1"], "categoryId": "22", "madeForKids": false }
```

### `DELETE /api/v1/misc/youtube/video`
Delete a YouTube video. Body: `{ "videoId": "vid_123", "teamId": "team_123" }`

### `PATCH /api/v1/misc/youtube/comment`
Edit a YouTube comment. Body: `{ "commentId": "c_123", "text": "updated text", "teamId": "team_123" }`

### `DELETE /api/v1/misc/youtube/comment`
Delete a YouTube comment. Body: `{ "commentId": "c_123", "teamId": "team_123" }`

### `GET /api/v1/misc/youtube/video-categories`
Get YouTube video categories. Query: `teamId` (required).

### `GET /api/v1/misc/youtube/regions`
Get YouTube regions. Query: `teamId` (required).

---

## LinkedIn (6 endpoints)

### `GET /api/v1/misc/linkedin/mentions/tags`
Get mentionable people & organizations. Query: `teamId` (required), `search` (optional).

### `POST /api/v1/misc/linkedin/mentions/builder`
Build LinkedIn text with mentions inserted at tag placeholders.
```json
{ "text": "Hello @[name]", "tags": [{ "urn": "urn:li:person:abc", "name": "John" }], "teamId": "team_123" }
```

### `PATCH /api/v1/misc/linkedin/post`
Edit a LinkedIn post. Body: `{ "postId": "p_123", "teamId": "team_123", "commentary": "new text" }`

### `DELETE /api/v1/misc/linkedin/post`
Delete a LinkedIn post. Body: `{ "postId": "p_123", "teamId": "team_123" }`

### `PATCH /api/v1/misc/linkedin/comment`
Edit a LinkedIn comment. Body: `{ "commentId": "c_123", "text": "updated", "teamId": "team_123" }`

### `DELETE /api/v1/misc/linkedin/comment`
Delete a LinkedIn comment. Body: `{ "commentId": "c_123", "teamId": "team_123" }`

---

## Google Business (19 endpoints)

### Media
| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/api/v1/misc/google-business/media` | Add media (photo/video) — query: `teamId`, `locationName`; body: `{ uploadId, category, sourceUrl? }` |
| `GET` | `/api/v1/misc/google-business/media` | List media — query: `teamId`, `locationName`, `category`, `pageSize`, `pageToken` |
| `DELETE` | `/api/v1/misc/google-business/media` | Delete media — body: `{ name, teamId }` |

### Posts
| Method | Path | Description |
|--------|------|-------------|
| `DELETE` | `/api/v1/misc/google-business/post` | Delete a GBP post — body: `{ name, teamId }` |

### Location Profile
| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/v1/misc/google-business/location` | Get location profile — query: `teamId`, `locationName?` |
| `PATCH` | `/api/v1/misc/google-business/location` | Update location profile — query: `teamId`, `locationName?` |
| `PATCH` | `/api/v1/misc/google-business/location/hours` | Update hours (regular/special/more) |
| `GET` | `/api/v1/misc/google-business/location/attributes` | Get attributes |
| `PATCH` | `/api/v1/misc/google-business/location/attributes` | Update attributes — body: `{ attributes: [{ name, value }] }` |
| `GET` | `/api/v1/misc/google-business/location/attributes/available` | List available attributes — query: `teamId`, `locationName?`, `category?` |
| `GET` | `/api/v1/misc/google-business/location/categories/available` | List available categories — query: `teamId`, `regionCode?`, `languageCode?`, `search?` |
| `GET` | `/api/v1/misc/google-business/location/service-list` | Get service list |
| `PATCH` | `/api/v1/misc/google-business/location/service-list` | Update service list — body: `{ services: [{ serviceTypeId, ... }] }` |
| `GET` | `/api/v1/misc/google-business/location/food-menus` | Get food menus |
| `PATCH` | `/api/v1/misc/google-business/location/food-menus` | Update food menus |

### Place Action Links
| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/v1/misc/google-business/location/place-action-links` | List place action links |
| `POST` | `/api/v1/misc/google-business/location/place-action-links` | Create — body: `{ placeActionLink: { uri, placeActionType } }` |
| `PATCH` | `/api/v1/misc/google-business/location/place-action-links` | Update — body: `{ name, placeActionLink: { uri?, placeActionType? } }` |
| `DELETE` | `/api/v1/misc/google-business/location/place-action-links` | Delete — body: `{ name }` |

### Reviews
| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/api/v1/misc/google-business/reviews/import` | Start review import — body: `{ teamId, locationName? }` |
| `GET` | `/api/v1/misc/google-business/reviews/import` | Get review import status list |
| `GET` | `/api/v1/misc/google-business/reviews/import/{importId}` | Get review import by ID |
| `GET` | `/api/v1/misc/google-business/reviews` | List imported reviews |
| `GET` | `/api/v1/misc/google-business/reviews/{reviewId}` | Get single review |
| `PUT` | `/api/v1/misc/google-business/reviews/{reviewId}/reply` | Reply to review — body: `{ teamId, comment }` |
| `DELETE` | `/api/v1/misc/google-business/reviews/{reviewId}/reply` | Delete review reply — body: `{ teamId }` |

---

## Reddit (6 endpoints)

### `GET /api/v1/misc/reddit/post-requirements`
Get subreddit post requirements. Query: `teamId` (required), `subreddit` (required).
```json
{ "flairEnabled": true, "flairRequired": false }
```

### `GET /api/v1/misc/reddit/subreddit-flairs`
Get subreddit flairs. Query: `teamId` (required), `subreddit` (required).

### `PATCH /api/v1/misc/reddit/post`
Edit a Reddit post. Body: `{ "postId": "...", "teamId": "...", "title?": "...", "text?": "...", "flairId?": "...", "flairText?": "..." }`

### `DELETE /api/v1/misc/reddit/post`
Delete a Reddit post. Body: `{ "postId": "...", "teamId": "..." }`

### `PATCH /api/v1/misc/reddit/comment`
Edit a Reddit comment. Body: `{ "commentId": "...", "text": "...", "teamId": "..." }`

### `DELETE /api/v1/misc/reddit/comment`
Delete a Reddit comment. Body: `{ "commentId": "...", "teamId": "..." }`

---

## Instagram (3 endpoints)

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/api/v1/misc/instagram/tags` | Search Instagram Business/Creator by username — query: `teamId`, `username` |
| `GET` | `/api/v1/misc/instagram/locations` | Search Instagram location IDs — query: `teamId`, `search` |
| `DELETE` | `/api/v1/misc/instagram/comment` | Delete an Instagram comment — body: `{ commentId, teamId }` |

---

## Facebook (9 endpoints)

### Recommendations
| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/api/v1/misc/facebook/recommendations/import` | Start recommendations import — body: `{ teamId }` |
| `GET` | `/api/v1/misc/facebook/recommendations/import` | Get import status list |
| `GET` | `/api/v1/misc/facebook/recommendations/import/{importId}` | Get import by ID |
| `GET` | `/api/v1/misc/facebook/recommendations` | List recommendations |
| `GET` | `/api/v1/misc/facebook/recommendations/{recommendationId}` | Get single recommendation |
| `GET` | `/api/v1/misc/facebook/recommendations/{recommendationId}/comments` | Get recommendation thread comments |
| `PUT` | `/api/v1/misc/facebook/recommendations/{recommendationId}/reply` | Reply to recommendation — body: `{ teamId, message }` |
| `PUT` | `/api/v1/misc/facebook/recommendations/{recommendationId}/comments/{commentId}/reply` | Reply to thread comment — body: `{ teamId, message }` |

### Posts & Comments
| Method | Path | Description |
|--------|------|-------------|
| `PATCH` | `/api/v1/misc/facebook/post` | Edit Facebook post — body: `{ postId, teamId, message? }` |
| `DELETE` | `/api/v1/misc/facebook/post` | Delete Facebook post — body: `{ postId, teamId }` |
| `PATCH` | `/api/v1/misc/facebook/comment` | Edit Facebook comment — body: `{ commentId, teamId, message }` |
| `DELETE` | `/api/v1/misc/facebook/comment` | Delete Facebook comment — body: `{ commentId, teamId }` |

---

## Pinterest (2 endpoints)

| Method | Path | Description |
|--------|------|-------------|
| `PATCH` | `/api/v1/misc/pinterest/pin` | [DISABLED] Edit pin — body: `{ pinId, teamId }` |
| `DELETE` | `/api/v1/misc/pinterest/pin` | Delete pin — body: `{ pinId, teamId }` |

---

## Mastodon (4 endpoints)

| Method | Path | Description |
|--------|------|-------------|
| `PATCH` | `/api/v1/misc/mastodon/status` | Edit status — body: `{ statusId, teamId, text? }` |
| `DELETE` | `/api/v1/misc/mastodon/status` | Delete status — body: `{ statusId, teamId }` |
| `PATCH` | `/api/v1/misc/mastodon/comment` | Edit comment — body: `{ commentId, text, teamId }` |
| `DELETE` | `/api/v1/misc/mastodon/comment` | Delete comment — body: `{ commentId, teamId }` |

---

## Slack (2 endpoints)

| Method | Path | Description |
|--------|------|-------------|
| `PATCH` | `/api/v1/misc/slack/message` | Edit message — body: `{ messageId, teamId, text? }` |
| `DELETE` | `/api/v1/misc/slack/message` | Delete message — body: `{ messageId, teamId }` |

---

## Bluesky (2 endpoints)

| Method | Path | Description |
|--------|------|-------------|
| `DELETE` | `/api/v1/misc/bluesky/post` | Delete post — body: `{ postId, teamId }` |
| `DELETE` | `/api/v1/misc/bluesky/comment` | Delete comment — body: `{ commentId, teamId }` |

---

## Twitter/X (1 endpoint)

| Method | Path | Description |
|--------|------|-------------|
| `DELETE` | `/api/v1/misc/twitter/tweet` | Delete tweet — body: `{ tweetId, teamId }` |

---

## Discord (1 endpoint)

| Method | Path | Description |
|--------|------|-------------|
| `DELETE` | `/api/v1/misc/discord/message` | Delete message — body: `{ messageId, teamId }` |

---

## TikTok (2 endpoints)

### `GET /api/v1/misc/tiktok/cml/trending-list`
Get popular tracks from TikTok Commercial Music Library. Query: `teamId` (required), `genre` (default: POP), `dateRange` (default: 7DAY).

40+ genre options and 3 date ranges: `1DAY`, `7DAY`, `30DAY`.

### `DELETE /api/v1/misc/tiktok/comment`
Delete a TikTok comment. Body: `{ commentId, teamId }`
