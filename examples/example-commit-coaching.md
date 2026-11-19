# Commit Message Coaching: feature/rate-limit

## Context
- Diff summary: auth middleware + Redis token bucket + docs
- Repo style: Emoji + Conventional Commits (`iuricode/padroes-de-commits`)

## Per-commit feedback

### Commit a1b2c3d
**Verdict:** NEEDS EDIT
**Original:**
```
updated stuff for API
```
**Issues:**
- Missing emoji, type, and scope
- Vague ("stuff"); past tense
- No why

**Recommended:**
```
✨ feat(api): add per-token rate limiting

Prevent partner storms from exhausting the primary DB pool.
Uses Redis token bucket with fail-open if Redis is unavailable.
```
**Why this is better:** Adds the semantic emoji and `feat(api)` prefix, states the capability, explains the motivation, and records a critical failure-mode choice.

### Commit d4e5f6a
**Verdict:** GOOD
**Original:**
```
📚 docs(api): document rate-limit headers
```
**Issues:** none material

## Patterns to practice
- Match the emoji and type (`feat`, `fix`, `docs`, `security`, `cleanup`, `remove`, etc.) to the change intent.
- Lead with user/system impact, not file names.
- Record fail-open/fail-closed decisions in the body.
