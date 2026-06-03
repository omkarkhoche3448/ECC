---
description: Generate build-in-public content from your codebase. Turns architecture decisions, pivots, and learnings into blog posts, dev logs, Twitter threads, and LinkedIn articles. Reads your actual code and git history.
---

# Build Journal Command

Invokes the **build-journalist** agent to turn your real code, git history, and architecture decisions into authentic technical content.

## Usage

```
/build-journal [what to write about]
```

### Examples

```
/build-journal Write a blog post about why I chose Bun + Elysia over Express
/build-journal Weekly dev log for this project
/build-journal Write about switching from REST to WebSocket for real-time voice
/build-journal Turn my architecture into a Twitter thread
/build-journal Write a "what I learned" post about my PostgreSQL → SQLite migration
/build-journal LinkedIn post about building a multi-tenant SaaS with S3 BYOS
/build-journal Technical deep dive on how WebSocket session persistence works in this project
```

## Content Types

| Type | Length | Best For |
|------|--------|----------|
| **Architecture Decision** | 800-1500 words | "Why we chose X over Y" posts |
| **Dev Log** | 300-600 words | Weekly/biweekly build updates |
| **"I Was Wrong" Post** | 500-1000 words | Pivots, mistakes, learnings (highest engagement) |
| **Technical Deep Dive** | 1000-2000 words | Complex feature explanations |
| **Twitter Thread** | 5-8 tweets | Quick insights, promote blog posts |
| **LinkedIn Post** | 150-300 words | Professional learnings, decisions |

## What It Reads From Your Project

- Git history (recent commits, changed files, refactors)
- CLAUDE.md / README.md (architecture)
- package.json (tech stack)
- docker-compose.yml (infrastructure)
- Actual source code (for real code snippets)
- Prisma schemas, config files

## Recommended Workflow

```
/build-journal Weekly dev log           ← every week
/build-journal Architecture decision    ← after major choices
/build-journal Pivot post               ← when you change direction
/build-journal Deep dive                ← for complex features
```

Then use **content-engine** skill to repurpose across platforms:
```
Use the content-engine skill to turn this blog post into X/LinkedIn/newsletter content
```

## Related

- **Agent**: `build-journalist` (`~/.claude/agents/build-journalist.md`)
- **Skill**: `article-writing` — general long-form writing (voice matching, essays)
- **Skill**: `content-engine` — repurpose content across platforms (X, LinkedIn, TikTok, YouTube)
