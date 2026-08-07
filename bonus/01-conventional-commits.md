# Bonus 1 — Conventional Commits

> Bootcamp exercises use numbered messages like `101 - Added a note`. Many teams use **conventional commits** instead — a `type:` prefix so history is easy to scan.

**Prerequisite:** [Lesson 2 — Git Basics](../lessons/02-git-basics.md)

---

## The format

```
type: short description in lowercase
```

| **Type** | **Use for** |
| -------- | ----------- |
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Formatting, no logic change |
| `refactor` | Restructure, same behavior |
| `test` | Tests |
| `chore` | Deps, config, maintenance |

| **Style** | **Example** |
| --------- | ----------- |
| Numbered (bootcamp) | `42 - Updated README` |
| Descriptive | `Add bio paragraph to homepage` |
| **Conventional** | `feat: add bio paragraph to homepage` |

All three are valid. Use conventional on team repos and open source when asked.

---

## Examples

```bash
git commit -m "feat: add skills list to homepage"
git commit -m "fix: correct typo in contact link"
git commit -m "docs: update README with setup steps"
```

Avoid vague messages like `fix: stuff` or `feat: changes`. README-only changes → `docs:`, not `feat:`.

---

## Try it

On any practice repo, make three commits: one `docs:`, one `feat:`, one `fix:` or `chore:`. Run `git log --oneline` and notice how the types stand out.

---

*End of Bonus 1 — Conventional Commits*

---
