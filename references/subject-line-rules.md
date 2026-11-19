# Subject line rules

1. **Optional emoji prefix (`--emoji` or `gcas.emoji=true`):** By default, subjects omit emojis (`feat(auth): add login page`). When emoji mode is active (`--emoji` or persistent `git config gcas.emoji true`), start with a semantic emoji matching the change (`✨`, `🐛`, `♻️`, or `:sparkles:`, `:bug:`, `:recycle:`) per [emoji-patterns.md](emoji-patterns.md).
2. **Imperative mood:** "add", "fix", "remove" — not "added" / "adds" / "adding" (or follow the repo's language consistently, e.g., imperative/infinitive in Portuguese: "adiciona"/"adicionar", "corrige"/"corrigir").
3. **Complete the sentence:** "If applied, this commit will …"
4. **Concise subject (~50 characters ideal, 72 hard max):** Keep the title short and direct; put details in the body.
5. **No trailing period** on the subject.
6. **Capitalize** only if your project style requires; Conventional Commits usually use lowercase after the type colon — **follow the repo**.
7. **Avoid** issue-only subjects (`fix #123`, `🐛 fix: #123`, `Resolves #123`). Describe the fix and put the tracker id in a footer (`Fixes #123`).
8. **Avoid** file dumps ("update utils.py and helpers.go") — state the intent.
9. **One logical change** per commit so history stays clean and revertible.
10. **Avoid** joke or temporary subjects ("YOLO", "stuff", "WIP", "TODO", "TMP") in shared history.

## Subject styles

Default for this skill: **Conventional Commits** (`feat(scope): description`), with optional semantic emojis via `--emoji` or `git config gcas.emoji true` (`✨ feat(scope): description` or `:sparkles: feat(scope): description`), compatible with [iuricode/padroes-de-commits](https://github.com/iuricode/padroes-de-commits).

**Classic 50/72** differs in two places only:

- The subject starts with a capital letter and has **no** emoji or `type:` prefix (`Add retry`, not `✨ feat: add retry`).
- A missing type is not a defect.

Do not force an emoji or `type:` prefix on a classic 50/72 repo. Follow a repo's `commitlint` config, commit template, or contributing guide whenever present.
