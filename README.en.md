# git-commit-agent-skill

AI agent skill that analyzes implemented changes, organizes atomic commits, and writes, lints, or executes **Conventional Commits + Semantic Emoji** messages — automatically yielding to a repository's own `commitlint` config, hooks, or classic `50/72` style when documented.

![Skill](https://img.shields.io/badge/skill-gcas-blue)
![Standard](https://img.shields.io/badge/standard-Conventional%20Commits%20%2B%20Emojis-purple)
![Agents](https://img.shields.io/badge/agents-Codex%20%C2%B7%20Claude%20Code%20%C2%B7%20Antigravity%20%C2%B7%20Cursor-teal)
![Python](https://img.shields.io/badge/python-3%2B-brightgreen)

[🇧🇷 Português](README.md) | **🇺🇸 English**

---

## Available Skill (`gcas`)

The skill is registered under the identifier **`gcas`** (**G**it **C**ommit **A**gent **S**kill). In your agent's chat, it works as a direct shortcut: in **Codex**, prefix it with `$` (`$gcas`); in **Claude Code**, **Antigravity**, and compatible agents, prefix it with `/` (`/gcas`).

| Shortcut | Description | When to use |
|---|---|---|
| `gcas` | **Git Commit Agent Skill** — inspects `git status` / `git diff`, groups logical changes, suggests or runs `git commit`, and reviews commit messages | Committing implemented code, drafting a message for staged changes, or reviewing/fixing commit messages |

> [!TIP]
> **THE SKILL IS A SHORTCUT, NOT A REQUIREMENT**
>
> Natural language requests trigger the exact same workflow: *"commit the changes I implemented"* or *"what commit message should I use for this?"* follow the same `gcas` flow. Use `$gcas` or `/gcas` whenever you want to guarantee that path explicitly. In agents without Skills support, natural language works on its own.

---

## Installation

From GitHub, using the [Skills CLI](https://skills.sh):

```bash
# Install and automatically detect configured agents in your project
npx skills add rodolfocop/git-commit-agent-skill

# Target a specific agent
npx skills add rodolfocop/git-commit-agent-skill --agent codex
npx skills add rodolfocop/git-commit-agent-skill --agent claude-code

# Install globally (available across all your projects)
npx skills add rodolfocop/git-commit-agent-skill -g
```

> **Prerequisites:** `python3` and `git` on `PATH` (no third-party Python packages required).

<details>
<summary>Local / manual installation (before publishing or offline)</summary>

```bash
# Via Skills CLI pointing to the local folder
npx skills add /path/to/git-commit-agent-skill

# Or copy manually into your project's skills folder
mkdir -p .agents/skills/gcas
cp -R SKILL.md README.md README.en.md references templates examples scripts .agents/skills/gcas/
```

</details>

---

## Usage after installing

### In Codex (`$gcas`)

```text
$gcas "Write a commit message for my staged changes."
$gcas "What should I name this commit?"
$gcas "Check my commit message: Fixed the login bug."
$gcas "Help me commit this: added a toggle for dark mode in settings."
$gcas "Is 'update stuff' a good commit message?"
$gcas "Commit the implemented changes split by logical context."
```

### In Claude Code, Antigravity, and others (`/gcas`)

```text
/gcas Write a commit message for my staged changes.
/gcas What should I name this commit?
/gcas Check my commit message: Fixed the login bug.
/gcas Help me commit this: added a toggle for dark mode in settings.
/gcas Is "update stuff" a good commit message?
/gcas Commit the implemented changes split by logical context.
```

> [!NOTE]
> When you ask only for a **suggestion or review** (*"Write a commit message..."*, *"Check my commit message..."*), the agent inspects the repository/message and returns a validated recommendation without altering your Git history. When you ask it to **commit/confirm** (*"Commit the implemented changes..."*, *"Help me commit this..."*), it stages the right files with `git add`, validates with the linter, and runs `git commit`.

---

## Commit standard

Default message format:

```text
[emoji] <type>[optional scope][!]: <description>

[optional body explaining why]

[optional footer(s): Fixes #123, Refs #42, Reviewed-by: ..., BREAKING CHANGE: ...]
```

Examples:
- `✨ feat(auth): add login page`
- `🐛 fix(api)!: handle empty payload without panic`
- `🔒️ security(auth): reject unsigned JWT tokens`
- `📚 docs(readme): update installation instructions`

### Supported types (`16`)

| Type | Emoji | Use for |
|---|---|---|
| `feat` | ✨ `:sparkles:` | New feature or user-facing capability (`MINOR` in SemVer) |
| `fix` | 🐛 `:bug:` | Bug fix (`PATCH` in SemVer) |
| `docs` | 📚 `:books:` | Documentation or code comment changes only |
| `test` | 🧪 `:test_tube:` | Adding, updating, or removing tests |
| `build` | 📦 `:package:` | Build system, packaging, or external dependencies |
| `perf` | ⚡ `:zap:` | Performance improvements |
| `style` | 👌 `:ok_hand:` | Formatting, lint, whitespace, and code style without logic changes |
| `refactor` | ♻️ `:recycle:` | Code restructuring that neither adds a feature nor fixes a bug |
| `chore` | 🔧 `:wrench:` | Routine maintenance, configs, `.gitignore`, moving/renaming |
| `ci` | 🧱 `:bricks:` | Continuous integration / deployment (CI/CD) files and scripts |
| `raw` | 🗃️ `:card_file_box:` | Configuration files, raw data, parameters, and feature flags |
| `cleanup` | 🧹 `:broom:` | Removing commented-out code, dead code, or redundant snippets |
| `remove` | 🗑️ `:wastebasket:` | Deleting obsolete files, directories, or unused features |
| `init` | 🎉 `:tada:` | Initial commit of the project |
| `revert` | 💥 `:boom:` | Reverting a previous commit |
| `security` | 🔒️ `:lock:` | Security fixes, vulnerability patches, and hardening |

See [`references/emoji-patterns.md`](references/emoji-patterns.md) for the complete 38-entry semantic emoji table and [`references/conventional-commits.md`](references/conventional-commits.md) for structural details.

---

## CLI Linter (standalone usage)

You can also run the validator directly in your terminal or Git hooks:

```bash
python3 scripts/check_commit_msg.py path/to/COMMIT_EDITMSG
echo "✨ feat(api): add retry" | python3 scripts/check_commit_msg.py --require-emoji -
python3 scripts/test_check_commit_msg.py
```

- **Exit `0`**: no `HIGH` findings (`MEDIUM` and `LOW` still warrant review).
- **Exit `1`**: at least one `HIGH` finding.
- **Exit `2`**: invalid usage or unreadable file.

---

## Project layout

| Path | Role |
|---|---|
| `SKILL.md` | Agent instructions for `gcas` (commit + review workflows) |
| `scripts/check_commit_msg.py` | Heuristic linter supporting emojis and all 16 commit types |
| `scripts/test_check_commit_msg.py` | Unit tests for the linter |
| `references/conventional-commits.md` | Commit format, 16 types, scopes, breaking changes, body & footers |
| `references/emoji-patterns.md` | Full semantic emoji table and examples |
| `references/subject-line-rules.md` | Length, imperative mood, emoji + Conventional Commits vs classic `50/72` |
| `templates/review-notes.md` | Coaching/review notes template |
| `examples/example-commit-coaching.md` | Worked message review example |

---

## References & Credits

The commit types, semantic structure, and emoji standards incorporated into this project use **[iuricode/padroes-de-commits](https://github.com/iuricode/padroes-de-commits)** by **Iuri Silva ([@iuricode](https://github.com/iuricode))** (MIT License) as a reference, alongside the **[Conventional Commits](https://www.conventionalcommits.org/)** specification.
