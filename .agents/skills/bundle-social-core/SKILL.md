---
name: bundle-social-core
description: >-
  Manage Bundle.social organization settings, teams, and health checks using the Bundle.social API.
  Use this skill when working with Bundle.social organization configuration, team management, checking API health/platform status, viewing usage limits (posts, comments, uploads, imports), or setting up a Bundle.social account for the first time.
  Covers all organization and team CRUD operations: creating teams, listing teams, getting org details, checking usage quotas, and the health-check endpoint.
  This skill should be triggered whenever a user mentions Bundle.social organizations, teams, API health, platform status, or usage limits — even if they just say "check my org" or "set up teams."
  Must be used whenever the conversation involves Bundle.social setup or configuration.
---

> **Author**: Anton Gulin · **Tool**: [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) · **GitHub**: [@antongulin](https://github.com/antongulin) · **Registry**: [skills.sh](https://www.skills.sh/docs)

# Bundle.social Core: Organization & Team Management

This skill covers the Bundle.social API endpoints for:
- **Health check** — checking API and platform status
- **Organization** — getting org details, viewing usage limits (posts, comments, uploads, imports)
- **Team** — CRUD operations for teams

## Authentication

All requests require the `x-api-key` header. The API base URL is `https://api.bundle.social`.

```
x-api-key: <your-api-key>
```

## Reference Docs

Read `references/README.md` for the full API overview (platform enums, standard errors, authentication).

The detailed endpoint specs are in:
- `references/01-app.md` — health check
- `references/02-organization.md` — org details and usage
- `references/03-team.md` — team CRUD

## How to Use This Skill

When a user asks you to do something related to Bundle.social org/team management:

1. **Read the relevant reference doc(s)** for the specific endpoint needed
2. **Generate curl command examples** with `<your-api-key>` as the placeholder (NEVER try to call the actual API — you won't have credentials)
3. **Optionally generate code examples** (JavaScript fetch, Python requests) in the user's preferred language
4. **Explain the response** in plain language — what the response fields mean, what to do next

### Making API Calls (Generate Examples Only)

Always generate examples with `<your-api-key>` as the auth header value. Never attempt to make live API calls — you will not have a valid key.

Example:
```bash
curl -s https://api.bundle.social/api/v1/ \
  -H "x-api-key: <your-api-key>"
```

### Generating Code Examples

When the user asks for code, generate examples in the language/framework they prefer. Always include authentication setup and error handling.

**JavaScript/TypeScript (fetch):**
```javascript
const response = await fetch('https://api.bundle.social/api/v1/team/', {
  headers: { 'x-api-key': '<your-api-key>' }
});
const data = await response.json();
```

**Python (requests):**
```python
import requests
response = requests.get('https://api.bundle.social/api/v1/team/',
  headers={'x-api-key': '<your-api-key>'})
data = response.json()
```

## Endpoint Reference Summary

### Health Check
- `GET /api/v1/` — API health check. Returns status, platform statuses.

### Organization Endpoints
- `GET /api/v1/organization/` — Get org details (subscription, teams, limits)
- `GET /api/v1/organization/usage/posts` — Daily post usage
- `GET /api/v1/organization/usage/comments` — Daily comment usage
- `GET /api/v1/organization/usage/uploads` — Upload usage
- `GET /api/v1/organization/usage/imports` — Import usage per social account (paginated)

### Team Endpoints
- `GET /api/v1/team/` — List teams (supports `offset`, `limit`, `search`)
- `POST /api/v1/team/` — Create team (requires `name`, `organizationId`)
- `GET /api/v1/team/{id}` — Get single team with full details
- `PATCH /api/v1/team/{id}` — Update team name/avatar
- `DELETE /api/v1/team/{id}` — Delete team

## Common Patterns

1. **Setup flow**: Health check → Get org → Create team → Connect social accounts
2. **Usage monitoring**: Check org usage before creating posts/comments to avoid hitting limits
3. **Error handling**: Always check for 401 (bad API key), 403 (insufficient permissions), 429 (rate limited)
