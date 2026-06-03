# Everything Claude Code - Full Catalog

> Quick reference of all components installed globally from this repo.
> Source: `everything-claude-code` | Installed to: `~/.claude/`

---

## Agents (16) — `~/.claude/agents/`

Specialized sub-agents Claude delegates tasks to automatically.

| # | Agent | Purpose |
|---|-------|---------|
| 1 | `architect` | System design, scalability, technical decisions |
| 2 | `build-error-resolver` | Fix build/type errors with minimal diffs |
| 3 | `chief-of-staff` | Triage email, Slack, LINE, Messenger communications |
| 4 | `code-reviewer` | Code quality, security, maintainability review |
| 5 | `database-reviewer` | PostgreSQL query optimization, schema design, Supabase |
| 6 | `doc-updater` | Update codemaps, READMEs, documentation |
| 7 | `e2e-runner` | Generate and run E2E tests (Playwright) |
| 8 | `go-build-resolver` | Fix Go build, vet, and linter errors |
| 9 | `go-reviewer` | Go code review (idioms, concurrency, errors) |
| 10 | `harness-optimizer` | Optimize agent harness config (reliability, cost) |
| 11 | `loop-operator` | Monitor and manage autonomous agent loops |
| 12 | `planner` | Plan complex features and refactoring |
| 13 | `python-reviewer` | Python code review (PEP 8, type hints, security) |
| 14 | `refactor-cleaner` | Remove dead code, duplicates, unused imports |
| 15 | `security-reviewer` | Detect OWASP Top 10, secrets, injection, SSRF |
| 16 | `tdd-guide` | Test-driven development, 80%+ coverage |

---

## Commands (40) — `~/.claude/commands/`

Slash commands you type in Claude Code (e.g. `/plan`, `/tdd`).

### Core Workflow
| # | Command | What it does |
|---|---------|-------------|
| 1 | `/plan` | Create step-by-step implementation plan |
| 2 | `/tdd` | Enforce test-driven development (tests first) |
| 3 | `/code-review` | Run code quality review |
| 4 | `/build-fix` | Fix build errors |
| 5 | `/e2e` | Generate and run Playwright E2E tests |
| 6 | `/verify` | Run verification checks |
| 7 | `/refactor-clean` | Dead code cleanup and consolidation |
| 8 | `/test-coverage` | Check and improve test coverage |
| 9 | `/quality-gate` | Run quality gate checks |
| 10 | `/checkpoint` | Create a checkpoint |

### Multi-Model Collaboration
| # | Command | What it does |
|---|---------|-------------|
| 11 | `/multi-plan` | Multi-model collaborative planning |
| 12 | `/multi-execute` | Multi-model collaborative execution |
| 13 | `/multi-frontend` | Frontend-focused multi-model development |
| 14 | `/multi-backend` | Backend-focused multi-model development |
| 15 | `/multi-workflow` | Full multi-model collaborative workflow |

### Learning & Patterns
| # | Command | What it does |
|---|---------|-------------|
| 16 | `/learn` | Extract reusable patterns from session |
| 17 | `/learn-eval` | Learn + self-evaluate before saving |
| 18 | `/skill-create` | Generate SKILL.md from git history |
| 19 | `/instinct-status` | Show learned instincts with confidence |
| 20 | `/instinct-import` | Import instincts from file or URL |
| 21 | `/instinct-export` | Export instincts to a file |
| 22 | `/promote` | Promote project instincts to global |
| 23 | `/evolve` | Analyze and evolve instinct structures |

### Go-Specific
| # | Command | What it does |
|---|---------|-------------|
| 24 | `/go-build` | Fix Go build errors and vet warnings |
| 25 | `/go-review` | Go code review (idioms, concurrency) |
| 26 | `/go-test` | TDD workflow for Go (table-driven tests) |

### Python-Specific
| # | Command | What it does |
|---|---------|-------------|
| 27 | `/python-review` | Python code review (PEP 8, security) |

### Operations & Sessions
| # | Command | What it does |
|---|---------|-------------|
| 28 | `/orchestrate` | Orchestrate multi-agent workflows |
| 29 | `/loop-start` | Start an autonomous loop |
| 30 | `/loop-status` | Check loop status |
| 31 | `/sessions` | Manage sessions |
| 32 | `/projects` | List known projects and instinct stats |
| 33 | `/pm2` | PM2 process manager init |
| 34 | `/setup-pm` | Configure package manager (npm/pnpm/yarn/bun) |

### Utilities
| # | Command | What it does |
|---|---------|-------------|
| 35 | `/claw` | Start NanoClaw REPL (model routing, branching) |
| 36 | `/eval` | Run evaluations |
| 37 | `/harness-audit` | Audit agent harness config |
| 38 | `/model-route` | Route tasks to optimal model |
| 39 | `/update-codemaps` | Update code maps |
| 40 | `/update-docs` | Update documentation |

---

## Skills (65) — `~/.claude/skills/`

Deep knowledge packs Claude uses for domain expertise. Grouped by category.

### TypeScript / JavaScript / React
| # | Skill | Focus |
|---|-------|-------|
| 1 | `coding-standards` | TS/JS/React coding standards and best practices |
| 2 | `frontend-patterns` | React, Next.js, state management, UI patterns |
| 3 | `backend-patterns` | Node.js, API design, server-side best practices |
| 4 | `api-design` | REST API naming, status codes, pagination, errors |
| 5 | `e2e-testing` | Playwright patterns, Page Object Model, CI/CD |
| 6 | `tdd-workflow` | Test-driven development enforcement |
| 7 | `verification-loop` | Comprehensive verification system |
| 8 | `plankton-code-quality` | Auto-formatting, linting, Claude-powered fixes |

### Python
| # | Skill | Focus |
|---|-------|-------|
| 9 | `python-patterns` | Pythonic idioms, PEP 8, type hints |
| 10 | `python-testing` | pytest, TDD, fixtures, mocking, coverage |

### Django
| # | Skill | Focus |
|---|-------|-------|
| 11 | `django-patterns` | Architecture, DRF, ORM, caching, signals |
| 12 | `django-security` | Auth, CSRF, SQL injection prevention |
| 13 | `django-tdd` | Testing with pytest-django, factory_boy |
| 14 | `django-verification` | Migrations, linting, tests, security scans |

### Go
| # | Skill | Focus |
|---|-------|-------|
| 15 | `golang-patterns` | Idiomatic Go, concurrency, error handling |
| 16 | `golang-testing` | Table-driven tests, benchmarks, fuzzing |

### Java / Spring Boot
| # | Skill | Focus |
|---|-------|-------|
| 17 | `java-coding-standards` | Spring Boot naming, immutability, streams |
| 18 | `springboot-patterns` | REST API, layered services, caching, async |
| 19 | `springboot-security` | Auth, validation, CSRF, rate limiting |
| 20 | `springboot-tdd` | JUnit 5, Mockito, MockMvc, Testcontainers |
| 21 | `springboot-verification` | Build, static analysis, tests, security scans |
| 22 | `jpa-patterns` | Entity design, relationships, query optimization |

### C++
| # | Skill | Focus |
|---|-------|-------|
| 23 | `cpp-coding-standards` | C++ Core Guidelines |
| 24 | `cpp-testing` | GoogleTest, CTest, flaky test diagnosis |

### Swift / iOS
| # | Skill | Focus |
|---|-------|-------|
| 25 | `swiftui-patterns` | @Observable, view composition, navigation |
| 26 | `swift-concurrency-6-2` | Swift 6.2 concurrency, @concurrent |
| 27 | `swift-actor-persistence` | Thread-safe persistence with actors |
| 28 | `swift-protocol-di-testing` | Protocol-based DI for testable Swift |
| 29 | `foundation-models-on-device` | Apple FoundationModels framework, on-device LLM |
| 30 | `liquid-glass-design` | iOS 26 Liquid Glass UI design system |

### Database
| # | Skill | Focus |
|---|-------|-------|
| 31 | `postgres-patterns` | Query optimization, schema, indexing, security |
| 32 | `clickhouse-io` | Analytics, query optimization, data engineering |
| 33 | `database-migrations` | Schema changes, rollbacks, zero-downtime |

### DevOps / Deployment
| # | Skill | Focus |
|---|-------|-------|
| 34 | `docker-patterns` | Containers, security, networking, volumes |
| 35 | `deployment-patterns` | CI/CD, health checks, rollback strategies |

### AI / Agents
| # | Skill | Focus |
|---|-------|-------|
| 36 | `agentic-engineering` | Eval-first execution, cost-aware model routing |
| 37 | `ai-first-engineering` | Teams where AI generates most implementation |
| 38 | `agent-harness-construction` | AI agent action spaces, tool definitions |
| 39 | `autonomous-loops` | Autonomous Claude Code loop architectures |
| 40 | `continuous-agent-loop` | Continuous loops with quality gates, evals |
| 41 | `enterprise-agent-ops` | Long-lived agent workloads, observability |
| 42 | `cost-aware-llm-pipeline` | LLM cost optimization, model routing, budgets |
| 43 | `eval-harness` | Eval-driven development (EDD) framework |
| 44 | `iterative-retrieval` | Progressive context retrieval for subagents |
| 45 | `ralphinho-rfc-pipeline` | RFC-driven multi-agent DAG execution |
| 46 | `nanoclaw-repl` | NanoClaw v2 session-aware REPL |
| 47 | `regex-vs-llm-structured-text` | Regex vs LLM decision framework for parsing |

### Learning & Patterns
| # | Skill | Focus |
|---|-------|-------|
| 48 | `continuous-learning` | Auto-extract patterns from sessions |
| 49 | `continuous-learning-v2` | Instinct-based learning with confidence scores |
| 50 | `search-first` | Research before coding workflow |
| 51 | `content-hash-cache-pattern` | SHA-256 content hash caching pattern |
| 52 | `strategic-compact` | Smart context compaction at logical intervals |
| 53 | `skill-stocktake` | Audit skills and commands for quality |

### Security
| # | Skill | Focus |
|---|-------|-------|
| 54 | `security-review` | Auth, user input, secrets, API security |
| 55 | `security-scan` | Scan .claude/ config for vulnerabilities |

### Content & Business
| # | Skill | Focus |
|---|-------|-------|
| 56 | `article-writing` | Articles, guides, blog posts, tutorials |
| 57 | `content-engine` | Multi-platform content (X, LinkedIn, YouTube) |
| 58 | `frontend-slides` | HTML presentations from scratch or PowerPoint |
| 59 | `investor-materials` | Pitch decks, one-pagers, financial models |
| 60 | `investor-outreach` | Cold emails, intros, investor communications |
| 61 | `market-research` | Competitive analysis, due diligence |
| 62 | `visa-doc-translate` | Translate visa documents to bilingual PDF |
| 63 | `nutrient-document-processing` | PDF processing, OCR, redaction, signing |

### Configuration
| # | Skill | Focus |
|---|-------|-------|
| 64 | `configure-ecc` | Interactive ECC installer |
| 65 | `project-guidelines-example` | Example project-specific skill template |

---

## Rules (2 sets) — `~/.claude/rules/`

Always-active guidelines loaded into every conversation.

| # | Rule Set | Files |
|---|----------|-------|
| 1 | `common/` | coding-style, security, testing, git-workflow, hooks, patterns, performance, development-workflow |
| 2 | `typescript/` | TypeScript-specific conventions and patterns |

---

## Hooks (14) — NOT installed globally (test per-project)

See main README for details. Control with `ECC_HOOK_PROFILE` env var.

## MCP Configs (16 servers) — NOT installed (opt-in)

See `mcp-configs/mcp-servers.json`. Copy servers you need to `~/.claude.json`.

---

## Quick Reference

```
/plan          -> plan a feature
/tdd           -> write tests first, then code
/code-review   -> review your code
/build-fix     -> fix build errors
/e2e           -> generate E2E tests
/learn         -> extract patterns from session
/skill-create  -> generate skill from git history
/verify        -> run verification checks
```
