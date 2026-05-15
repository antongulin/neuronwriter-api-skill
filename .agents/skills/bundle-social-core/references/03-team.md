# Team

Tag: `team` — 5 endpoints

---

## GET /api/v1/team/

Get list of teams.

**Query Parameters:**

| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `offset` | number | no | 0 | Pagination offset |
| `limit` | number | no | 10 | Max items to return |
| `search` | string | no | — | Search teams by name |

**Response 200:** `{ items: [TeamObject] }`

---

## POST /api/v1/team/

Create a new team.

**Request Body:**
```json
{
  "name": "My Team",
  "organizationId": "org_123",
  "avatarUrl": "https://..." // optional, nullable
}
```

**Response 200:** Created team object.

---

## GET /api/v1/team/{id}

Get a single team with full details.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Response 200:** Full team object including:
- `id`, `name`, `avatarUrl`, `organizationId`, `createdById`
- `organization` — nested organization info
- `createdBy` — user who created team
- `bots` — associated bots
- `socialAccounts` — connected accounts (with channels, webhooks, metadata)
- `bio` — bio items and analytics
- Timestamps: `createdAt`, `updatedAt`, `deletedAt`

---

## PATCH /api/v1/team/{id}

Update team.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Request Body:**
```json
{
  "name": "Updated Team Name",   // optional, 3-80 chars
  "avatarUrl": "https://..."     // optional, nullable
}
```

**Response 200:** Updated team object.

---

## DELETE /api/v1/team/{id}

Delete team.

**Path Parameters:**

| Name | Type | Required |
|------|------|----------|
| `id` | string | yes |

**Response 200:** Deleted team object.
