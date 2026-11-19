---
name: gcas
description: >-
  Git Commit Agent Skill (gcas). Creates standardized Git commits for
  implemented changes and reviews/lints commit messages using Conventional
  Commits (default: no emoji) with optional semantic emojis from
  iuricode/padroes-de-commits (`--emoji` per command, or persistent toggle via
  `git config gcas.emoji true|false`). Supports 16 commit types, imperative
  subject, why-not-what body, and footers. Inspects git status/diffs, suggests
  or writes commit messages for staged changes, groups atomic logical commits,
  stages files safely, lints messages with `scripts/check_commit_msg.py`, and
  executes `git commit` when requested. Yields to a repo's commitlint config,
  hook, or classic 50/72 style when documented. Use when committing implemented
  code, drafting a message for staged changes, toggling emoji mode, preparing
  clean history before merge, or evaluating and rewriting commit messages (in
  English or Portuguese).
compatibility: Requires python3 and git on PATH. Standard library only.
metadata:
  version: "1.1.0"
---

# git-commit-agent-skill (`gcas`)

Create clear, atomic Git commits for implemented work and keep `git log` useful six months later, following Conventional Commits and the semantic emoji conventions from [iuricode/padroes-de-commits](https://github.com/iuricode/padroes-de-commits).

## Files in this skill

- [scripts/check_commit_msg.py](./scripts/check_commit_msg.py) — subject/body linter (stdlib only; supports `--require-emoji` and `--forbid-emoji`)
- [references/conventional-commits.md](./references/conventional-commits.md) — message format, 16 commit types, scopes, breaking changes, body & footers
- [references/emoji-patterns.md](./references/emoji-patterns.md) — full semantic emoji table and examples from `iuricode/padroes-de-commits`
- [references/subject-line-rules.md](./references/subject-line-rules.md) — length, imperative mood, emoji + Conventional Commits vs classic 50/72
- [templates/review-notes.md](./templates/review-notes.md) — feedback format for commit message coaching
- [examples/example-commit-coaching.md](./examples/example-commit-coaching.md) — worked coaching session

## Emoji mode (`--emoji` & persistent active/inactive toggle)

By default, commits **do not** include a leading emoji (`<type>[scope]: <description>`). Determine whether to include a semantic emoji using this precedence order:

1. **Per-command flag in the user prompt** (highest priority):
   - `--emoji` → **active** for this run only (prepend matching emoji from [references/emoji-patterns.md](./references/emoji-patterns.md)).
   - `--no-emoji` → **inactive** for this run only (omit emoji even if persistent mode is active).
2. **Repo convention**: if `commitlint`, `.git/hooks/commit-msg`, or `CONTRIBUTING.md` explicitly requires or forbids emojis, follow the repo.
3. **Persistent toggle (`git config gcas.emoji`)**: check `git config --get gcas.emoji` (reads local repo config first, then global user config).
   - `true` → **active** (always include leading emoji unless `--no-emoji` is passed).
   - `false` or unset → **inactive** (default; omit leading emoji unless `--emoji` is passed).

### Managing the persistent toggle
If the user asks to turn emoji mode on/off or check its status (e.g., `--emoji-on`, `--emoji-off`, `--emoji-status`, or *"ativar emoji sempre"* / *"desativar emoji"*):
- **Activate (this repo):** `git config gcas.emoji true` (add `--global` if the user asks for all projects).
- **Deactivate (this repo):** `git config gcas.emoji false` (add `--global` if the user asks for all projects).
- **Check status:** `git config --show-origin --get gcas.emoji` (if unset, report `inactive (default)`).

## Workflow A: Commit implemented changes

### 1. Inspect repository state & conventions
- Run `git status --short`, `git diff --cached --stat`, `git diff --stat` (plus `git diff` where needed to understand intent), and `git config --get gcas.emoji || echo "false"`.
- Check recent history (`git log -n 10 --oneline`, if commits exist) and repo configs (`commitlint.config.*`, `.commitlintrc*`, `.git/hooks/commit-msg`, `CONTRIBUTING.md`). Repo conventions override skill defaults.
- Match the repository's commit description language (e.g., English or Portuguese). When emoji mode is **active**, use Unicode `✨` by default (or `:sparkles:` shortcode if the repo uses shortcodes).

### 2. Plan atomic commits & stage safely
- Split unrelated changes into separate logical commits (e.g., `feat` vs `fix`, `test`, `docs`, `refactor`, `cleanup`, `remove`, `security`, `chore`).
- Stage intentional files explicitly (`git add <path ...>`). Never stage secrets (`.env*`, credentials, private keys) or OS junk (`.DS_Store`) unless explicitly tracked/intended.

### 3. Draft the commit message
Using [references/conventional-commits.md](./references/conventional-commits.md), [references/emoji-patterns.md](./references/emoji-patterns.md), and [references/subject-line-rules.md](./references/subject-line-rules.md):
1. Pick the accurate **type** (`feat`, `fix`, `docs`, `test`, `build`, `perf`, `style`, `refactor`, `chore`, `ci`, `raw`, `cleanup`, `remove`, `init`, `revert`, `security`). Prepend its matching **emoji** **only if emoji mode is active** (`--emoji` or `gcas.emoji=true`).
2. Add an optional concise **scope** (`(auth)`, `(api)`, `(ui)`) and `!` if breaking.
3. Write an imperative, specific **subject** (ideally ≤50 chars, hard max 72, no trailing period, no `WIP`/`TODO`/`TMP`, no issue-only subjects).
4. Add a **body** (separated by a blank line) explaining **why**, constraints, or tradeoffs when the change is non-trivial.
5. Add **footers** when applicable (`Fixes #123`, `Refs #42`, `Reviewed-by: ...`, `BREAKING CHANGE: ...`). Use direct, unshortened URLs if linking.

### 4. Lint & commit (or present message)
Run [scripts/check_commit_msg.py](./scripts/check_commit_msg.py) resolving its path relative to this skill's directory (where `SKILL.md` resides):
- When emoji mode is **inactive** (default / `--no-emoji`):
  ```bash
  printf '%s\n' "feat(auth): add login page" | python3 <skill-dir>/scripts/check_commit_msg.py --forbid-emoji -
  ```
- When emoji mode is **active** (`--emoji` / `gcas.emoji=true`):
  ```bash
  printf '%s\n' "✨ feat(auth): add login page" | python3 <skill-dir>/scripts/check_commit_msg.py --require-emoji -
  ```
Fix any `HIGH` or `MEDIUM` findings before finalizing.
- If the user asked only to **suggest or write** a commit message (e.g., for staged changes), present the validated message (ready to paste) and ask if they want you to run `git commit`.
- If the user asked to **commit/confirm** the implemented changes, execute `git commit` and report the resulting commit SHA and `git log -1 --stat`.

If the repo uses classic 50/72 (capitalized imperative, no emoji or `type:` prefix), ignore `type-missing`, `type-case`, `type-unknown`, and `emoji-missing`, while still keeping length, mood, period, blank line, and body checks.

## Workflow B: Review & coach commit messages

1. Collect the commit message(s) (`git log -1 --format=%B` or `git log --oneline`) and optional diff summary (`git diff --stat` / `git diff --cached --stat`).
2. Lint with `python3 <skill-dir>/scripts/check_commit_msg.py` (exit `0` means no `HIGH` finding; `MEDIUM` and `LOW` still require review).
3. Evaluate type/emoji accuracy, imperative mood, why-not-what body, breaking-change markers, and noise.
4. Provide ready-to-paste rewrites (preserving author intent) and write coaching notes using [templates/review-notes.md](./templates/review-notes.md) like [examples/example-commit-coaching.md](./examples/example-commit-coaching.md).

## Verdicts (when reviewing)
- **GOOD** — ship as-is (nits optional). `LOW` findings may stay `GOOD`.
- **NEEDS EDIT** — any `MEDIUM`, or a `HIGH` that applies to this repo's style. Rewrite provided.
- **SPLIT OR SQUASH** — history structure is the real problem.

## Rules
- Never amend, rebase, reset, or force-push unless the user explicitly asks.
- Never leak secrets from diffs into commit messages or examples.
- Prefer one clear, searchable subject over vague or witty wording.
- A repo's `commitlint` config, commit hook/template, or documented style wins over built-in defaults.
