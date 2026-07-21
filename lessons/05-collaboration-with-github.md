# Lesson 5 – Collaboration with GitHub

> Git's real power shows when **people work together**. Now that you can push and pull, this lesson covers how to start from someone else's project and how teams coordinate their work.

---

## What You'll Learn

By the end of this lesson, students will be able to:

1. **Clone** an existing repository to their computer.
2. **Fork** a repository and explain when forking is needed.
3. Distinguish between **cloning** and **forking**.
4. Understand common **team workflows** for collaborating on a shared project.
5. Use **`git rebase`** as an alternative way to update a branch with the latest `main`.

---

## Cloning Repositories

So far you've created your own repositories. But often you'll want to start from a project that **already exists** on GitHub — yours or someone else's. **Cloning** makes a full local copy of a remote repository.

---

### Definition

**Clone:**

> Creating a complete local copy of a remote repository, including all its files and full history, on your own computer.

When you clone, Git automatically sets up the remote connection (`origin`) for you — no need to run `git remote add`.

---

### How to Clone

1. On the GitHub repository page, click the green **Code** button.
2. Copy the URL (for example, `https://github.com/someuser/cool-project.git`).
3. Run `git clone` with that URL:

```bash
git clone https://github.com/someuser/cool-project.git
```

This creates a new folder named `cool-project` containing the full project. Then:

```bash
cd cool-project
git status
```

You now have the entire project and its history locally, ready to work on.

---

### Clone vs Init

You've now seen two ways to start a local repository:

| **`git init`**                          | **`git clone`**                              |
| --------------------------------------- | -------------------------------------------- |
| Starts a **brand-new** empty repository | Copies an **existing** remote repository     |
| No remote connection yet                | Remote (`origin`) is set up automatically    |
| Used when you begin from scratch        | Used when you join an existing project       |

---

## Forking Repositories

Cloning gives you a local copy, but you usually can't push changes back to a repository you don't own. That's where **forking** comes in.

A **fork** is your **own personal copy** of someone else's repository, stored under **your** GitHub account.

---

### Definition

**Fork:**

> A personal copy of someone else's repository, created under your own GitHub account, which you fully control and can modify freely.

Forking happens **on GitHub** (in the browser), not on your computer. You click a button and GitHub creates the copy for you.

---

### How to Fork

1. Go to the repository you want to contribute to on GitHub.
2. Click the **Fork** button in the top-right corner.
3. GitHub creates a copy at `github.com/your-username/that-project`.
4. Now **clone your fork** to work on it locally:

```bash
git clone https://github.com/your-username/that-project.git
```

You can change your fork however you like without affecting the original.

---

### Clone vs Fork

These two are easy to mix up. Here's the difference:

| **Clone**                            | **Fork**                                       |
| ------------------------------------ | ---------------------------------------------- |
| Happens on **your computer**         | Happens on **GitHub** (in the browser)         |
| A local copy of a repo               | A personal **server-side** copy under your account |
| You may not be able to push back     | You fully own the fork and can push to it      |
| Used to **work** on a project        | Used to **contribute** to a project you don't own |

> 💡 In open-source projects (Lesson 8), the typical pattern is: **fork** the project to your account, then **clone** your fork to your computer.

---

### When to Use Each

- **You own the repo or are a team member?** → Just **clone** it; you can push directly.
- **You want to contribute to a project you don't own?** → **Fork** it first, then clone your fork.

---

## Team Workflows

When several people work on the same project, you need an agreed way to avoid chaos. Most teams use a **branch-based workflow** built on what you already learned in Lesson 3.

---

### The Shared Repository Workflow

This is the most common workflow for teams who all have access to one repository:

1. **Everyone clones** the shared repository.
2. For each task, a developer **creates their own branch** (never works directly on `main`).
3. They **commit** their work to that branch and **push** the branch to GitHub.
4. They open a **Pull Request** to merge it into `main` (covered fully in Lesson 6).
5. After review, the branch is **merged** and deleted.

```
            Shared Repository (GitHub)
                       │
        ┌──────────────┼──────────────┐
   clone│         clone│         clone│
        ▼              ▼              ▼
   Developer A    Developer B    Developer C
  (feature-x)    (fix-bug-y)    (feature-z)
        │              │              │
        └──── push branches & open Pull Requests ───┘
```

---

### The Golden Rules of Team Work

| **Rule**                                  | **Why It Matters**                                       |
| ----------------------------------------- | -------------------------------------------------------- |
| Never commit directly to `main`           | Keeps the official version stable and protected.         |
| One branch per feature or fix             | Keeps work isolated and easy to review.                  |
| `git pull` before you start               | Begins your work from the latest version.                |
| Push often                                | Backs up your work and keeps teammates informed.         |
| Write clear commit messages               | Helps the whole team understand the history.             |

> ⚠️ **Common mistake:** Two people working on `main` at the same time. They overwrite each other and create messy conflicts. The fix is simple: **always work on your own branch.**

---

### Keeping Your Branch Up to Date

While you work on your branch, `main` may receive new changes from teammates. To stay current and reduce conflicts later:

```bash
# Switch to main and get the latest
git switch main
git pull

# Switch back to your branch and bring main's changes in
git switch feature-login
git merge main
```

Doing this regularly keeps your branch close to the team's latest work, so the final merge is smooth.

---

### Updating with Rebase (Alternative)

Some teams use **`git rebase`** instead of **`git merge`** to bring in the latest `main`. Both keep your branch up to date — they just organize history differently.

```bash
# Switch to main and get the latest
git switch main
git pull

# Switch back to your branch and replay your commits on top of main
git switch feature-login
git rebase main
```

| **`git merge main`**                         | **`git rebase main`**                              |
| -------------------------------------------- | -------------------------------------------------- |
| Creates a merge commit combining both lines  | Replays your commits on top of the latest `main`   |
| Preserves the exact branch history           | Produces a straighter, linear history              |
| Safer for beginners and shared branches      | Common on teams that prefer a clean log            |

> ⚠️ **Common mistake:** Rebasing commits you've **already pushed** and shared with others can confuse teammates. Use `git rebase` on branches you're still working on locally, or only when your team agrees on it.

---

## Summary

- **Cloning** makes a full local copy of a remote repository, with `origin` set up automatically.
- **Forking** creates your own copy of someone else's repository under your GitHub account.
- `git init` starts fresh; `git clone` copies an existing repo. Cloning is local; forking is on GitHub.
- For open source, the pattern is usually **fork → clone**.
- Teams use a **branch-based workflow**: clone the shared repo, work on your own branch, push, and open a Pull Request.
- Update your branch with **`git merge main`** or **`git rebase main`** to stay current with the team.
- Golden rule: **never work directly on `main`** — always use a branch.

---

*End of Lesson 5*

---
