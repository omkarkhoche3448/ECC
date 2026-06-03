---
description: Deep technical research before planning or coding. Finds research papers, existing implementations, open-source solutions, architectural patterns, and proven approaches. Use before /plan to make informed decisions.
---

# Technical Research Command

Invokes the **technical-researcher** agent to find existing solutions, research papers, and proven implementations BEFORE you start planning or coding.

## Usage

```
/research [what you want to research]
```

### Examples

```
/research WebSocket session persistence for voice AI assistants
/research multi-tenant file storage with BYOS (Bring Your Own Storage)
/research real-time STT → LLM → TTS voice pipeline architectures
/research conversation history maintenance patterns for chat applications
/research CRDT vs OT for real-time collaborative editing
/research rate limiting strategies for multi-tenant SaaS APIs
/research PostgreSQL row-level security vs application-level tenancy
```

## What It Searches

- Research papers (arXiv, Google Scholar, ACM, IEEE)
- Open-source implementations (GitHub, npm, PyPI, crates.io)
- Engineering blogs (Netflix, Uber, Stripe, Discord, Cloudflare, AWS)
- Architecture patterns and case studies
- RFCs and standards (IETF, W3C, OWASP, CNCF)
- Awesome lists and curated resources
- Stack Overflow discussions

## Output

A structured **Technical Research Brief** with:
1. Key findings ranked by relevance
2. Research papers table
3. Open-source implementations comparison
4. Architecture patterns found
5. Known failure modes and anti-patterns
6. **Build vs Adopt vs Extend** recommendation
7. Essential reading list before implementing

## Recommended Workflow

```
/research [topic]          ← Find what exists first
/plan [feature]            ← Plan informed by research findings
/tdd [implementation]      ← Build with TDD
/code-review               ← Review what you built
```

## Related

- **Agent**: `technical-researcher` (`~/.claude/agents/technical-researcher.md`)
- **Skill**: `search-first` — lighter-weight library/package search
- **Skill**: `market-research` — business/market research (not technical)
- **Command**: `/plan` — use AFTER research to create implementation plan
