# NEURONwriter API Skill

[![skills.sh](https://skills.sh/b/antongulin/neuronwriter-api-skill)](https://skills.sh/antongulin/neuronwriter-api-skill)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)

AI agent skill for the [NEURONwriter API](https://neuronwriter.com) — SEO content optimization platform with NLP-driven keyword analysis, competitor SERP analysis, and content scoring.

> **Author**: Anton Gulin · **Tool**: [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) · **GitHub**: [@antongulin](https://github.com/antongulin) · **Registry**: [skills.sh](https://www.skills.sh/docs)

AI agent skill providing structured instructions for creating SEO-optimized content through the NEURONwriter API — from keyword research and competitor analysis to content generation, import, and iterative scoring.

## Skill

### [neuronwriter-api](./skill/SKILL.md)

Complete API integration for NEURONwriter. Performs the full content optimization lifecycle: project discovery, keyword analysis (with quota-aware proxy fallback), content brief generation with NLP term ranges, HTML content generation that enforces real term frequency ranges, content import and scoring, and iterative improvement.

```bash
# List projects
./scripts/neuronwriter.sh list-projects

# Create a keyword analysis query
./scripts/neuronwriter.sh new-query '{
  "project": "PROJECT_ID",
  "keyword": "your target keyword",
  "engine": "google.com",
  "language": "English",
  "competitors_mode": "top-intent"
}'

# Poll until ready and get recommendations
./scripts/neuronwriter.sh wait-and-get QUERY_ID 30

# Import content and get score
./scripts/neuronwriter.sh import-content '{
  "query": "QUERY_ID",
  "html": "<h1>Title</h1><p>Content...</p>",
  "title": "SEO Title",
  "description": "Meta description"
}'
```

The skill handles quota exhaustion gracefully by falling back to proxy queries from existing data, using multi-proxy strategies (2-3 semantically similar queries), and always documenting every API command executed.

## Installation

### Using the Skills CLI (recommended)

**Project scope** — installs locally in the current project:

```bash
npx skills add antongulin/neuronwriter-api-skill
```

**Global scope** (`-g`) — available across all projects:

```bash
npx skills add antongulin/neuronwriter-api-skill -g
```

The CLI automatically detects your installed coding agents. See [skills.sh](https://skills.sh) for more options.

### Manual

Clone the repo and copy the skill to your agent's skills path:

```bash
git clone https://github.com/antongulin/neuronwriter-api-skill.git
cp -r neuronwriter-api-skill/skill <agent-skills-path>/neuronwriter-api
```

Replace `<agent-skills-path>` with your agent's skills directory. Common paths:

| Agent | Path |
|-------|------|
| Universal | `~/.agents/skills/` |
| OpenCode | `~/.config/opencode/skills/` |
| Claude Code | `~/.claude/skills/` |
| GitHub Copilot | `~/.copilot/skills/` |
| Cursor | `~/.cursor/skills/` |
| Gemini CLI | `~/.gemini/skills/` |
| Cline | `~/.agents/skills/` |
| Codex | `~/.codex/skills/` |

## API Overview

The NEURONwriter API (v0.5, beta) provides programmatic access to SEO content recommendations:

| Method | Description |
|--------|-------------|
| `list-projects` | List all projects in the account |
| `new-query` | Create a keyword analysis (consumes 1 content writer credit) |
| `get-query` | Get recommendations (poll `status` until `"ready"`) |
| `list-queries` | List/filter queries with status, source, tags |
| `get-content` | Get saved content revision |
| `import-content` | Import HTML content and get a content score |
| `evaluate-content` | Score content without saving |

**Authentication:** `X-API-KEY` header. Requires Gold plan or higher.

**Quota system:** Content writer analyses (1 per new-query) are separate from AI credits and plagiarism checks (web UI only, no API endpoints).

## Compatibility

Skills are compatible with AI coding assistants that support the [skills.sh](https://www.skills.sh/docs) skill format, including OpenCode, Claude Code, Copilot CLI, Cursor, Codex, Cline, Gemini CLI, and 50+ others.

## Related

- [NEURONwriter](https://neuronwriter.com) — The SEO content optimization platform
- [opencode-skill-creator](https://github.com/antongulin/opencode-skill-creator) — Tool used to generate this skill
- [mole-skills](https://github.com/antongulin/mole-skills) — macOS system maintenance skills by the same author
- [bundle-social-api-skill](https://github.com/antongulin/bundle-social-api-skill) — Social media API skills by the same author
