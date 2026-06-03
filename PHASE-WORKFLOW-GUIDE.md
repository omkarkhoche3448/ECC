# Phase-wise Implementation Prompt Guide

> Copy-paste these prompts for each sub-phase. Replace `[X]` with your phase number (1a, 1b, 1c, etc.)

---

## Before You Start Any Phase

### 1. Verify previous phase is clean
```
/ecc:verify
Run full verification: lint, typecheck, unit tests, integration tests.
Confirm everything passes before starting Phase [X].
```

### 2. Check what Phase [X] requires
```
Read docs/phases/phase-[X].md and all feature specs referenced in it
(docs/features/F*.md). Summarize:
- What features are in scope
- What dependencies from previous phases are needed
- What files will be created or modified
- What tests are required

Do NOT write any code yet. Just summarize the scope.
```

---

## Build the Phase

### 3. Implement with TDD
```
/ecc:tdd

Implement Phase [X] following docs/phases/phase-[X].md exactly.
Reference feature specs in docs/features/ for acceptance criteria.

Rules:
- Write tests FIRST for each feature, then implement
- Follow docs/TECH-STACK.md for all technology choices
- Follow docs/ARCHITECTURE.md for folder structure and patterns
- Stay within this phase's scope — do NOT touch other phases
- Target 80%+ test coverage for new code
```

### 4. If build breaks mid-phase
```
/ecc:build-fix
Fix the build errors. Do not change test expectations.
Minimal fixes only — get green, then continue.
```

---

## After the Phase

### 5. Code review
```
/ecc:code-review

Review Phase [X] implementation against docs/phases/phase-[X].md.
Check:
- All acceptance criteria from feature specs are met
- No scope creep (nothing outside phase scope was touched)
- Test coverage is 80%+
- No security issues (auth, injection, secrets)
- Code follows docs/TECH-STACK.md patterns
```

### 6. Security check (for auth, API, user input phases)
```
/ecc:verify
Run full verification: lint, typecheck, tests, security scan.
Report any failures.
```

### 7. E2E tests (after major milestones)
```
/ecc:e2e

Generate E2E tests for Phase [X] features.
Test the full flow end-to-end based on feature specs.
Capture screenshots for visual verification.
```

### 8. Commit
```
Commit all Phase [X] changes with message:
feat: implement phase [X] — [brief description]
```

---

## Phase-Specific Prompts

### Phase 1a — Database + Prisma Schema
```
/ecc:tdd

Implement Phase 1a following docs/phases/phase-1a.md.

Focus:
- Prisma schema with all models from ARCHITECTURE.md
- PostgreSQL RLS policies
- Initial migration
- Database seed script for development
- Connection pooling setup

Write integration tests that verify:
- All models can be created/read/updated/deleted
- RLS policies work correctly
- Migrations run cleanly
```

### Phase 1b — Auth (JWT + API Key + HMAC)
```
/ecc:tdd

Implement Phase 1b following docs/phases/phase-1b.md.

Focus:
- JWT auth (issue, verify, refresh, revoke)
- API Key auth (generate, validate, scope)
- HMAC webhook signing
- Auth middleware for Fastify
- Rate limiting per auth method

Write tests FIRST for:
- Token generation and validation
- Token refresh flow
- Token revocation
- API key CRUD and validation
- HMAC signature verification
- Auth middleware (protected vs public routes)
- Rate limiting per auth type
- Edge cases: expired tokens, invalid keys, replay attacks
```

### Phase 1c — Upload System
```
/ecc:tdd

Implement Phase 1c following docs/phases/phase-1c.md.

Focus:
- File upload endpoint (multipart)
- Chunked upload for large files
- File validation (size, type, mime)
- Upload progress tracking
- Temporary storage before processing

Write tests FIRST for:
- Single file upload
- Chunked upload (multi-part)
- File size limit enforcement
- Blocked file type rejection
- Upload progress events
- Concurrent upload handling
```

### Phase 1d — Download System + Link Management
```
/ecc:tdd

Implement Phase 1d following docs/phases/phase-1d.md.

Focus:
- File download endpoint
- Streaming downloads for large files
- Share link generation (short URLs)
- Link expiry and access control
- Download count tracking

Write tests FIRST for:
- Direct file download
- Streaming large file download
- Share link creation and resolution
- Link expiry enforcement
- Password-protected links
- Download counter increment
```

### Phase 1e — Storage Adapters (S3/MinIO)
```
/ecc:tdd

Implement Phase 1e following docs/phases/phase-1e.md.

Focus:
- Storage adapter interface
- S3 adapter implementation
- MinIO adapter (S3-compatible, self-hosted)
- Local filesystem adapter (development)
- Adapter factory pattern

Write tests FIRST for:
- Upload to each adapter
- Download from each adapter
- Delete from each adapter
- Adapter switching via config
- Error handling (network, permissions, not found)
```

### Phase 1f — Async Workers (BullMQ)
```
/ecc:tdd

Implement Phase 1f following docs/phases/phase-1f.md.

Focus:
- BullMQ worker setup with Redis
- Worker factory pattern
- Job types: thumbnail, virus scan, cleanup, notifications
- Dead letter queue (DLQ)
- Job retry and backoff strategy

Write tests FIRST for:
- Job creation and processing
- Job retry on failure
- DLQ routing after max retries
- Worker concurrency limits
- Job progress reporting
- Graceful shutdown
```

### Phase 1g — API Gateway (middleware)
```
/ecc:tdd

Implement Phase 1g following docs/phases/phase-1g.md.

Focus:
- Request validation (Zod/Typebox schemas)
- Rate limiting middleware
- CORS configuration
- Request logging
- Error handling middleware
- API versioning

Write tests FIRST for:
- Request validation (valid and invalid payloads)
- Rate limit enforcement
- CORS headers
- Error response format consistency
- API version routing
```

---

## Quick Reference

| Step | Command | When |
|------|---------|------|
| Verify clean | `/ecc:verify` | Before starting any phase |
| Build | `/ecc:tdd` | Main implementation |
| Fix breaks | `/ecc:build-fix` | When build fails |
| Review | `/ecc:code-review` | After phase complete |
| Security | `/ecc:verify` | After auth/API/input phases |
| E2E | `/ecc:e2e` | After major milestones |
| Coverage | `/ecc:test-coverage` | If coverage drops below 80% |

## The Loop

```
verify clean → read phase scope → TDD build → code review → verify → commit → next phase
```

Repeat for every sub-phase until Phase 1 is complete, then move to Phase 2.
