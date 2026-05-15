# App — Health Check

Tag: `app`

---

## GET /api/v1/

Check API health and platform status.

**Parameters:** None

**Response 200:**
```json
{
  "status": "ok",
  "createdAt": "2024-01-01T00:00:00Z",
  "note": "All systems operational",
  "platforms": {
    "FACEBOOK": { "status": "operational", "note": "" },
    "INSTAGRAM": { "status": "operational", "note": "" },
    "TIKTOK": { "status": "operational", "note": "" },
    "YOUTUBE": { "status": "operational", "note": "" },
    "TWITTER": { "status": "operational", "note": "" },
    "PINTEREST": { "status": "operational", "note": "" },
    "REDDIT": { "status": "operational", "note": "" },
    "MASTODON": { "status": "operational", "note": "" },
    "DISCORD": { "status": "operational", "note": "" },
    "SLACK": { "status": "operational", "note": "" },
    "BLUESKY": { "status": "operational", "note": "" },
    "GOOGLE_BUSINESS": { "status": "operational", "note": "" },
    "LINKEDIN": { "status": "operational", "note": "" },
    "THREADS": { "status": "operational", "note": "" }
  }
}
```

Platform status enum: `operational`, `degraded`, `outage`, `maintenance`
