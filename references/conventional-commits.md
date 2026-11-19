# Conventional Commits & `iuricode/padroes-de-commits`

Format:
```text
[emoji] <type>[optional scope][!]: <description>

[optional body]

[optional footer(s)]
```

Examples:
- `✨ feat(auth): add login page`
- `:bug: fix(api)!: handle empty payload without panic`
- `docs(readme): update install command` (emoji is recommended, optional if repo rules omit emojis)

## Supported types

Adapted from [Conventional Commits](https://www.conventionalcommits.org/) and [iuricode/padroes-de-commits](https://github.com/iuricode/padroes-de-commits):

| Type | Default emoji | Use for |
|------|---------------|---------|
| `feat` | ✨ `:sparkles:` | New user-facing feature or capability (SemVer `MINOR`) |
| `fix` | 🐛 `:bug:` | Bug fix (SemVer `PATCH`) |
| `docs` | 📚 `:books:` | Documentation or code comments only (no production code changes) |
| `test` | 🧪 `:test_tube:` / ✅ `:white_check_mark:` | Adding, updating, or removing tests (no production code changes) |
| `build` | 📦 `:package:` | Build system, packaging, or external dependencies |
| `perf` | ⚡ `:zap:` | Performance improvements |
| `style` | 👌 `:ok_hand:` | Code formatting, lint, whitespace, semicolons (no logic change) |
| `refactor` | ♻️ `:recycle:` | Code restructuring that neither fixes a bug nor adds a feature |
| `chore` | 🔧 `:wrench:` | Maintenance tasks, configs, `.gitignore`, tooling, moving/renaming |
| `ci` | 🧱 `:bricks:` | CI/CD configuration and pipeline scripts |
| `raw` | 🗃️ `:card_file_box:` | Configuration files, raw data, feature flags, parameters |
| `cleanup` | 🧹 `:broom:` | Removing commented-out code, dead code, or redundant snippets |
| `remove` | 🗑️ `:wastebasket:` | Deleting obsolete/unused files, directories, or features |
| `init` | 🎉 `:tada:` | Initial commit of the project |
| `revert` | 💥 `:boom:` | Reverting a previous commit |
| `security` | 🔒️ `:lock:` | Security fixes and hardening (vulnerabilities, auth/authz, data exposure) |

See [emoji-patterns.md](emoji-patterns.md) for the complete 38-entry semantic emoji table.

## Scope
Optional noun in parentheses: `✨ feat(api):`, `🐛 fix(auth):`. Keep short and stable across the repo.

## Breaking changes
- `feat!:` / `fix!:` in the subject (with or without leading emoji), and/or
- Footer: `BREAKING CHANGE: <description of impact and migration>`

## Body
- Explain **why**, constraints, impacts, and instructions for future maintenance.
- Wrap near 72 cols when practical.
- Bullet lists are fine for multiple motivations.

## Footers & Links
- Reference issues/cards and reviewers in footers:
  - `Fixes #123`
  - `Refs #42`
  - `Reviewed-by: Name`
- Use authentic, direct URLs only (no URL shorteners or affiliate links).
