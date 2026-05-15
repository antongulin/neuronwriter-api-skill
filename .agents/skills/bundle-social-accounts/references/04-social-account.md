# Social Account

Tag: `socialAccount` — 11 endpoints

---

## POST /api/v1/social-account/connect

Generate OAuth URL to connect a social account to a team. Redirect user to the returned URL.

**Request Body:**
```json
{
  "type": "INSTAGRAM",                        // required — platform enum
  "teamId": "team_123",                       // required
  "redirectUrl": "https://myapp.com/callback", // required — URI
  "serverUrl": "https://mastodon.social",     // optional — Mastodon/Bluesky only
  "disableAutoLogin": false,                   // optional
  "forceBrowserOAuth": false,                  // optional — Instagram only
  "instagramConnectionMethod": "FACEBOOK",     // optional — FACEBOOK or INSTAGRAM
  "withBusinessScope": false                   // optional — Facebook/Instagram only
}
```

**Response 200:**
```json
{ "url": "https://..." }
```

---

## DELETE /api/v1/social-account/disconnect

Disconnect a social account from a team. Also removes account from scheduled posts.

**Request Body:**
```json
{
  "id": "acc_123",
  "teamId": "team_123"
}
```

**Response 200:** Disconnected social account object.

---

## POST /api/v1/social-account/set-channel

Set channel for a social account (e.g., Discord channel, Slack channel, Reddit subreddit).

**Request Body:**
```json
{
  "socialAccountId": "acc_123",
  "channel": {
    "id": "ch_123",
    "name": "general",
    "username": "mybot",
    "address": "#general",
    "avatarUrl": "https://...",
    "webhook": { "id": "wh_123", "name": "webhook", "avatar": "https://...", "url": "https://..." },
    "metadata": {
      "allowImages": true,
      "allowVideos": true,
      "allowGalleries": false,
      "linkFlairEnabled": true
    }
  }
}
```

**Response 200:** Updated social account object.

---

## POST /api/v1/social-account/unset-channel

Remove channel from a social account.

**Request Body:**
```json
{ "socialAccountId": "acc_123" }
```

**Response 200:** Updated social account object.

---

## POST /api/v1/social-account/refresh-channels

Refresh available channels for a social account.

**Request Body:**
```json
{ "socialAccountId": "acc_123" }
```

**Response 200:** Updated social account with refreshed channels.

---

## POST /api/v1/social-account/create-portal-link

Create a portal link for the social account.

**Request Body:**
```json
{
  "socialAccountId": "acc_123",
  "teamId": "team_123",
  "redirectUrl": "https://myapp.com/callback"
}
```

**Response 200:**
```json
{ "url": "https://..." }
```

---

## POST /api/v1/social-account/connection-check

Manually run connection/disconnect check.

**Request Body:**
```json
{ "socialAccountId": "acc_123" }
```

**Response 200:** Social account object with updated disconnect check status.

---

## POST /api/v1/social-account/profile-refresh

Manually refresh social account profile info.

**Request Body:**
```json
{ "socialAccountId": "acc_123" }
```

**Response 200:** Social account object with refreshed profile info.

---

## GET /api/v1/social-account/by-type

Get social account by team and platform type.

**Query Parameters:**

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `type` | enum | yes | Platform type |
| `teamId` | string | yes | Team ID |

**Response 200:** Full social account object:
- `id`, `type`, `teamId`, `username`, `displayName`, `avatarUrl`, `externalId`
- `userUsername`, `userDisplayName`, `userId`
- `channels`, `mastodonServerId`, `instagramConnectionMethod`, `twitterSubType`
- `isTiktokBusinessAccount`, `disconnectCheckTryAt`, `deleteOn`
- Timestamps

---

## POST /api/v1/social-account/copy

Copy social accounts to another team.

**Request Body:**
```json
{
  "socialAccountIds": ["acc_123", "acc_456"],  // required, 1-50 items
  "toTeamId": "team_456"                        // required
}
```

**Response 200:** Object with copied social accounts information.

---

## GET /api/v1/social-account/to-delete

Get paginated social accounts scheduled for deletion.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `page` | number | no | 1 | Page number (min: 1) |
| `pageSize` | number | no | 20 | Items per page (1-100) |

**Response 200:**
```json
{
  "items": [ /* social account objects */ ],
  "pagination": { "page": 1, "pageSize": 20, "total": 5, "totalPages": 1 }
}
```
