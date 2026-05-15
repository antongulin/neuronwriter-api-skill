---
name: bundle-social-analytics
description: >-
  Retrieve and analyze social media performance metrics using the Bundle.social Analytics API.
  Use this skill when fetching analytics for social accounts or individual posts, getting raw metrics,
  bulk-comparing post performance, or forcing analytics refreshes on Bundle.social.
  Covers impressions, views, likes, comments, shares, saves, follower counts, engagement rates,
  and per-platform specific metrics. Supports date-range filtering, granularity control, and bulk post comparison.
  This skill should be triggered whenever a user mentions analytics, metrics, performance, engagement,
  impressions, or "how is my social media performing" in the context of Bundle.social.
---

> **Author**: Anton Gulin · **Tool**: [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) · **GitHub**: [@antongulin](https://github.com/antongulin) · **Registry**: [skills.sh](https://www.skills.sh/docs)

# Bundle.social Analytics

This skill covers retrieving performance metrics for social accounts and posts on Bundle.social.

## Authentication

```
x-api-key: <your-api-key>
```

Base URL: `https://api.bundle.social`

## Reference Docs

Read `references/README.md` for platform enums and standard errors.
Read `references/07-analytics.md` for endpoint details.

## How to Use This Skill

When a user asks about social media analytics or performance data:

1. **Determine scope** — account-level analytics or post-level analytics
2. **Identify time range** — ask for `dateFrom`/`dateTo` if not provided
3. **Read the reference doc** for the specific endpoint
4. **Generate curl command examples** with `<your-api-key>` as placeholder (NEVER call the actual API)
5. **Present the data clearly** — highlight key metrics, trends, and comparisons

### Analytics Data Structure

Account and post analytics share common metrics:
- `impressions`, `impressionsUnique` — how many times content was seen
- `views`, `viewsUnique` — video views where applicable
- `likes`, `comments`, `shares`, `saves` — engagement actions
- `followerCount` — audience growth
- `engagementRate` — engagement relative to reach

Per-platform metrics may differ — YouTube has watch time, Instagram has story metrics, etc.

## Endpoint Reference Summary

### Account Analytics
- `GET /api/v1/analytics/social-account` — Get analytics for a social account (supports `dateFrom`, `dateTo`, `granularity`)
- `GET /api/v1/analytics/social-account/raw` — Get raw analytics data
- `POST /api/v1/analytics/social-account/force` — Force refresh analytics

### Post Analytics
- `GET /api/v1/analytics/post` — Get analytics for a specific post
- `GET /api/v1/analytics/post/raw` — Get raw analytics data for a post
- `GET /api/v1/analytics/post/bulk` — Compare analytics for up to 60 posts at once
- `POST /api/v1/analytics/post/force` — Force refresh post analytics

## Common Patterns

1. **Account health check**: Get account analytics for last 30 days → Check trends in impressions and engagement
2. **Post performance comparison**: Use bulk endpoint with multiple postIds → Compare metrics side by side
3. **Deep dive**: Get post analytics → If interesting, get raw data for detailed analysis
4. **Fresh data**: If analytics seem stale, use force refresh → Wait → Re-fetch
5. **Reporting**: Pull account analytics with date range and granularity for weekly/monthly reports

## Using the Bulk Analytics Endpoint

The bulk endpoint (`GET /api/v1/analytics/post/bulk`) is powerful for comparison:
- Max 60 postIds per request, paginated 20 per page
- Requires `platformType` — all posts must be from the same platform
- Each result contains per-post metric arrays

## Error Handling

- Data may not be available immediately after posting — analytics update asynchronously
- Force refresh has rate limits — don't spam it
- Some metrics are platform-specific and may return null for platforms that don't support them
