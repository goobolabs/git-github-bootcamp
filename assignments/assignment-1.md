# Assignment: Git Basics

**Due:** Saturday, July 25, 2026 — 12:00 PM (Africa/Mogadishu / EAT)

**Goal:** Submit the practice repository you built through Exercises 1–3, proving you can use Git locally (commits, history, authorship) and push your work to GitHub.

---

## What you are submitting

Your submission is the **same project** you practiced with in Lessons 2–4. Before you submit, confirm:

- [ ] **Exercise 1** — at least **100 numbered commits** on `main`
- [ ] **Exercise 2** — **`main`** plus at least **5 other branches**, each with at least **1 commit**
- [ ] **Exercise 3** — project pushed to GitHub as **`git-github-practice`**, including your branches
- [ ] **At least 10 different files** visible on GitHub (`.txt`, `.md`, `.csv`, `.html`, `.css`, `.json`, images, PDF, etc.)
- [ ] Every commit shows **your** name and email from Lesson 1

---

## How to submit

Follow the [submissions guide](../submissions/README.md):

1. **Fork** this bootcamp repository to your GitHub account.
2. Create the folder `submissions/<your-github-username>/assignment-1/` (username must match exactly — case-sensitive).
3. Add a `submission.md` file with your repository URL and confirmation (see template below).
4. **Commit and push** your changes to your fork.
5. Open a **Pull Request** to this repository.
   - PR title: `Assignment Submission - <Your GitHub Username>` (for example, `Assignment Submission - sharafdin`)

### `submission.md` template

Create `submissions/your-username/assignment-1/submission.md`:

```md
# Assignment 1 — Git Basics

- **Name:** Your Full Name
- **GitHub username:** your-username
- **Repository URL:** https://github.com/your-username/git-github-practice

## Confirmation

- [ ] At least 100 commits are visible on GitHub
- [ ] At least 10 different files are visible on GitHub
- [ ] **`main`** plus at least **5 other branches** are visible on GitHub (each with at least 1 commit)
- [ ] Commit authors show my name and email
```

Replace the placeholders with your real details before opening your PR.

---

## Evaluation criteria

| **Criterion** | **What we check** |
| ------------- | ----------------- |
| Commit count | At least **110 commits** on GitHub |
| Commit messages | Numbered from `1 - ...` through `110 - ...` |
| Branches | **`main`** (or **`master`**) plus at least **5 other branches** on GitHub, each with at least **1 commit** |
| Author | Every commit shows **your** name and email from Lesson 1 |
| Timestamps | Commits were made over time during your practice (not all at once) |
| Files | At least **10 different files** pushed successfully |
| Submission | PR includes `submissions/<username>/assignment-1/submission.md` with a valid repo URL |

---

## Common mistakes

| **Mistake** | **Fix** |
| ----------- | ------- |
| Wrong author on commits | Set `user.name` and `user.email` **before** committing in Lesson 2 |
| Empty GitHub repo after push | Make sure you **committed** locally first — `git push` only sends commits |
| Branches missing on GitHub | Push each feature branch: `git push -u origin <branch-name>` (or `git push --all origin`) |
| Submission folder name wrong | Your folder must exactly match your GitHub username (case-sensitive) |
| Changing or modifying others' work | Only edit files inside **your own** folder under `submissions/<your-username>/`. Do not touch anyone else's submission |
| Committing files you did not mean to include | Run `git status` **before every commit**. Review the listed files and make sure only your intended changes are staged |

---

*Assignment 1 — Git & GitHub Bootcamp*
