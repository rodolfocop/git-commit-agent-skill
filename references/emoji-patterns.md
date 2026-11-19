# Emoji Patterns (`iuricode/padroes-de-commits`)

Reference table of semantic commit emojis and keywords adapted from [iuricode/padroes-de-commits](https://github.com/iuricode/padroes-de-commits) by Iuri Silva.

Format:
```text
:emoji: type(optional-scope): description
```

Either the Unicode character (`✨`) or the GitHub shortcode (`:sparkles:`) may be used at the start of the subject line.

## Emoji & Keyword Table

| Context / Change | Emoji | Shortcode | Keyword (`type`) |
|---|---|---|---|
| Accessibility | ♿ | `:wheelchair:` | — (`feat` / `fix`) |
| Adding a test | ✅ | `:white_check_mark:` | `test` |
| Upgrading submodule version | ⬆️ | `:arrow_up:` | — (`build` / `chore`) |
| Downgrading submodule version | ⬇️ | `:arrow_down:` | — (`build` / `chore`) |
| Adding a dependency | ➕ | `:heavy_plus_sign:` | `build` |
| Code review changes | 👌 | `:ok_hand:` | `style` |
| Animations and transitions | 💫 | `:dizzy:` | — (`feat` / `style`) |
| `.gitignore` file | 🙈 | `:see_no_evil:` | `chore` |
| Bugfix | 🐛 | `:bug:` | `fix` |
| Code comments | 💡 | `:bulb:` | `docs` |
| Initial commit | 🎉 | `:tada:` | `init` |
| Configuration | 🔧 | `:wrench:` | `chore` |
| Deploy | 🚀 | `:rocket:` | — (`ci` / `chore`) |
| Documentation | 📚 | `:books:` | `docs` |
| Work in progress (avoid on main) | 🚧 | `:construction:` | — |
| UI styling | 💄 | `:lipstick:` | `feat` |
| Infrastructure / CI | 🧱 | `:bricks:` | `ci` |
| Task / idea list | 🔜 | `:soon:` | — |
| Mocks | 🤡 | `:clown_face:` | `test` |
| Move / Rename | 🚚 | `:truck:` | `chore` |
| New feature | ✨ | `:sparkles:` | `feat` |
| `package.json` / JS packages | 📦 | `:package:` | `build` |
| Performance | ⚡ | `:zap:` | `perf` |
| Refactoring | ♻️ | `:recycle:` | `refactor` |
| Code cleanup | 🧹 | `:broom:` | `cleanup` |
| Removing a file | 🗑️ | `:wastebasket:` | `remove` |
| Removing a dependency | ➖ | `:heavy_minus_sign:` | `build` |
| Responsiveness | 📱 | `:iphone:` | — (`feat` / `fix`) |
| Reverting changes | 💥 | `:boom:` | `fix` / `revert` |
| Security | 🔒️ | `:lock:` | `security` |
| SEO | 🔍️ | `:mag:` | — (`feat` / `perf`) |
| Version tag | 🔖 | `:bookmark:` | — (`chore`) |
| Approval / passing test | ✔️ | `:heavy_check_mark:` | `test` |
| Tests | 🧪 | `:test_tube:` | `test` |
| Text / copy | 📝 | `:pencil:` | — (`docs` / `feat`) |
| Typing / type definitions | 🏷️ | `:label:` | — (`refactor` / `feat`) |
| Error handling | 🥅 | `:goal_net:` | — (`fix` / `feat`) |
| Raw data / parameters | 🗃️ | `:card_file_box:` | `raw` |

## Practical Examples

```text
🎉 init: initial repository setup
✨ feat(auth): add OAuth login flow
🐛 fix(api): resolve timeout in user endpoint
📚 docs(readme): update installation instructions
🧪 test(cart): add unit tests for discount calculation
📦 build: upgrade typescript to 5.8
⚡ perf(query): add index on user email lookup
👌 style(lint): apply formatter rules
♻️ refactor(parser): extract token validation helper
🔧 chore: update gitignore for local env files
🧱 ci: add test step to GitHub Actions workflow
🗃️ raw: add 2026 tax bracket parameters
🧹 cleanup: remove dead code in payment handler
🗑️ remove: delete deprecated v1 billing module
💥 revert: revert caching layer due to stale reads
🔒️ security(auth): reject unsigned JWT tokens
```
