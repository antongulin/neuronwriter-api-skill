# Organization

Tag: `organization` — 5 endpoints

---

## GET /api/v1/organization/

Get organization details including subscription, teams, and limits.

**Parameters:** None

**Response 200:** Full organization object with:
- `id`, `createdById`, `name`, `avatarUrl`, `ref`
- `dailyPostLimit`, `dailyCommentLimit` (per-platform objects)
- `monthlyImportLimitPerAccount`, `commentImportLimitPerPost`, `monthlyReviewImportLimitPerAccount`
- `apiAccess`, `analyticsDisabled`, `analyticsPostsDisabled`, `uploadsCompressionEnabled`
- `analyticsInterval`, `analyticsPostsInterval`, `showVerboseErrors`, `disconnectCheckEnabled`
- `deleteAccountAfter` (0-168 hours)
- `subscription` — Stripe subscription details (tier, billing, status, coupon, promotion code)
- `promotionCode` — active promo code
- `teams` — array of team objects
- `createdBy` — user who created org
- Timestamps: `createdAt`, `updatedAt`, `deletedAt`

---

## GET /api/v1/organization/usage/posts

Get organization posts usage.

**Parameters:** None

**Response 200:**
```json
{ "used": 42, "limit": 1000, "remaining": 958 }
```

---

## GET /api/v1/organization/usage/comments

Get organization comments usage.

**Parameters:** None

**Response 200:**
```json
{ "used": 10, "limit": 500, "remaining": 490 }
```

---

## GET /api/v1/organization/usage/uploads

Get organization uploads usage.

**Parameters:** None

**Response 200:**
```json
{ "used": 5, "limit": 200, "remaining": 195 }
```

---

## GET /api/v1/organization/usage/imports

Get organization imports usage per social account (paginated).

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `page` | number | no | 1 | Page number (min: 1) |
| `pageSize` | number | no | 20 | Items per page (1-100) |
| `teamId` | string | no | — | Filter by team |
| `socialAccountType` | enum | no | — | Filter by platform type |
| `socialAccountId` | string | no | — | Filter by account |

**Response 200:**
```json
{
  "limitPerSocialAccount": 1000,
  "socialAccounts": [
    {
      "id": "acc_123",
      "type": "INSTAGRAM",
      "username": "my_business",
      "displayName": "My Business",
      "used": 50,
      "limit": 1000,
      "remaining": 950
    }
  ],
  "pagination": { "page": 1, "pageSize": 20, "total": 1, "totalPages": 1 }
}
```
