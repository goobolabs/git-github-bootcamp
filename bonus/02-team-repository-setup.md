# Bonus 2 — Team Repository Setup

> Teams configure repos with **collaborators**, **branch protection**, **PR templates**, and **CODEOWNERS** — guardrails on top of Lessons 5–6.

**Prerequisites:** [Lesson 4](../lessons/04-remote-repositories.md), [Lesson 5](../lessons/05-collaboration-with-github.md), [Lesson 6](../lessons/06-pull-requests-and-code-reviews.md)

---

## Collaborators

When **you own the repo**, invite teammates as **collaborators** — one shared remote. Use **forks** only when contributing to someone else's project ([Lesson 8](../lessons/08-open-source-workflows.md)).

| **Role** | **Can do** |
| -------- | ---------- |
| **Read** | Clone, pull, open issues |
| **Write** | Push branches, open/merge PRs (unless branch protection blocks) |
| **Admin** | Change Settings, invite others |

**Invite:** Settings → **Collaborators** → **Add people** → pick role. Teammate accepts, clones your repo, branches, pushes, opens a PR — same as Lesson 6.

---

## Branch protection

Enforces "no direct pushes to `main`" on GitHub.

1. Settings → **Branches** → **Add rule**
2. Pattern: `main`
3. Enable **Require a pull request before merging**
4. Save

Test: a direct push to `main` should fail; branch → PR → merge should still work.

---

## PR template

File: `.github/pull_request_template.md`

```markdown
## What this does

## Why

## How to test

Fixes #
```

Commit and push. New PRs pre-fill this description.

---

## CODEOWNERS

File: `.github/CODEOWNERS` — maps paths to reviewers.

```
# Global fallback: Catch-all owner for any file not caught by later rules
* @global-lead-user

# Match by file extension: JavaScript files are owned by a specific team
*.js @org-name/frontend-developers

# Match an entire directory: Every file inside the /docs/ folder
/docs/ @tech-writer-user

# Match a specific file: Exactly matches a single key file
/scripts/deploy.sh @devops-engineer @security-lead
```

When those files change in a PR, GitHub requests review from the listed owner.

---

## Settings worth knowing

| **Area** | **Note** |
| -------- | -------- |
| **General** | Name, visibility (public/private), default branch |
| **Pull Requests** | Squash merge vs merge commit; auto-delete head branches (recommended) |
| **Danger Zone** | Delete/archive — no undo |

---

## Common mistakes

| **Mistake** | **Fix** |
| ----------- | ------- |
| Teammate can't push | Confirm invite **accepted** and role is **Write**+ |
| Used fork for your own team repo | Invite collaborator instead |
| Template not showing | Path must be `.github/pull_request_template.md` |
| Protection on wrong branch | Match default branch name exactly (`main`) |

---

*End of Bonus 2 — Team Repository Setup*

---
