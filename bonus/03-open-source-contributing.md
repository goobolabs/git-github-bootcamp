# Bonus 3 — Open Source Contributing

> Goes deeper than [Lesson 8](../lessons/08-open-source-workflows.md): organizing issues, syncing forks, and finding good projects.

**Prerequisites:** [Lesson 5](../lessons/05-collaboration-with-github.md), [Lesson 8](../lessons/08-open-source-workflows.md)

---

## Issues — labels, templates

- **Labels** — filter work (`bug`, `good first issue`, `documentation`). Issues → **Labels** → **New label**.
- **Templates** — `.github/ISSUE_TEMPLATE/bug_report.md` pre-fills new issues.
- **Auto-close** — put `Fixes #12` in the **PR description** (not just the commit message).

**Filters:** `label:"good first issue"`, `is:open`, `author:your-username`

---

## Sync your fork

Forks do **not** auto-update. Before an OSS PR:

1. Open **your fork** on GitHub → **Sync fork** → **Update branch**
2. Locally: `git switch main && git pull origin main`
3. Branch from fresh `main`: `git switch -c fix/docs-typo`

**Workflow:** Fork → sync if behind → clone fork → branch → push → PR to **original** repo.

---

## Stars, forks, discovery

| **Action** | **Use when** |
| ---------- | ------------ |
| **Star** | Bookmark a repo you like |
| **Fork** | You plan to push changes and open a PR |

**Find projects:** [github.com/explore](https://github.com/explore), [github.com/topics/good-first-issue](https://github.com/topics/good-first-issue), search e.g. `topic:good-first-issue language:markdown`.

**Before contributing, check:**

| **Healthy** | **Warning** |
| ----------- | ----------- |
| Clear README, recent commits | Empty README, years of silence |
| Maintainers reply to issues | Many ignored PRs |
| LICENSE + CONTRIBUTING.md | No license — see [Bonus 6](06-open-source-licenses.md) |

Pin finished work on your profile — [Bonus 8](08-github-profile.md).

---

## Common mistakes

| **Mistake** | **Fix** |
| ----------- | ------- |
| PR from outdated fork | Sync first |
| PR targets your fork only | Base repo = **original** project |
| `Fixes #N` in commit title only | Put it in **PR description** |
| Star when you need to contribute | Fork → branch → PR |

---

*End of Bonus 3 — Open Source Contributing*

---
