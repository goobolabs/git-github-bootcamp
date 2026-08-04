# Lesson 8 – Open Source Workflows

> You now have every skill needed to contribute to real projects. This lesson shows how the **open-source world** works on GitHub — how people coordinate through issues and discussions, and how to contribute respectfully.

---

## What You'll Learn

By the end of this lesson, students will be able to:

1. Explain what **open source** is and why it matters.
2. Use **Issues** to report bugs and suggest features.
3. Understand **Discussions** and how they differ from issues.
4. Follow good **contribution etiquette**.
5. Open a PR that **links to an issue** (for example, `Fixes #42`).
6. Find and tackle **good first issues** as a newcomer.
7. **Fork** a project and **sync your fork** when the original repository changes.

---

## What is Open Source?

Most of the software that powers the world — your browser, your operating system's tools, programming languages like Python — is **open source**. It's built in public, by communities, and anyone can read it, use it, and improve it.

---

### Definition

**Open Source:**

> Software whose source code is made publicly available, so that anyone can view, use, modify, and contribute to it.

GitHub is the largest home for open-source projects in the world. The skills from Lessons 5 and 6 — **fork, clone, branch, pull request** — are exactly how people contribute to these projects.

If you **don't own** the project, **fork** it. Collaborator invites are for teammates on a repo someone already owns — a different workflow used on private team projects.

---

### Why Contribute to Open Source?

- **Learn from real code** written by experienced developers.
- **Build a portfolio** — your contributions are public and visible to employers.
- **Give back** to tools you use and enjoy.
- **Join a community** and meet other developers worldwide.

> You don't need to be an expert to contribute. Fixing a typo in documentation is a real, welcome contribution. Everyone starts somewhere.

---

## Issues

An **Issue** is the main way people communicate about *work* on a GitHub project. It's a place to report a bug, request a feature, or ask a question about the project.

---

### Definition

**Issue:**

> A tracked item on a GitHub repository used to report bugs, request features, or discuss specific tasks that need attention.

Each issue has a title, a description, a discussion thread, and a status (**open** or **closed**). You'll find them under the **Issues** tab of any repository.

---

### What Issues Are Used For

| **Issue Type**   | **Example**                                                |
| ---------------- | ---------------------------------------------------------- |
| Bug report       | "The login button doesn't work on mobile."                 |
| Feature request  | "Please add a dark mode option."                           |
| Task             | "Update the documentation for version 2.0."                |
| Question         | "How do I configure the app for offline use?"              |

---

### Writing a Good Issue

A helpful issue makes it easy for maintainers to understand and act. For a **bug report**, include:

```
**Describe the bug**
The search box returns no results when the query has spaces.

**Steps to reproduce**
1. Go to the homepage
2. Type "new york" in the search box
3. Press Enter

**Expected behavior**
It should show cities matching "new york".

**Screenshots / environment**
Browser: Chrome 125, OS: Windows 11
```

> 💡 Maintainers are often volunteers with limited time. A clear, complete issue is a gift — it dramatically increases the chance your problem gets fixed.

⚠️ **Common mistake:** Vague issues like *"It doesn't work."* Without steps to reproduce, nobody can help you. Always explain **what you did**, **what happened**, and **what you expected**.

---

### Labels

Maintainers organize issues with **labels** — colored tags that describe an issue at a glance:

| **Label**          | **Meaning**                                  |
| ------------------ | -------------------------------------------- |
| `bug`              | Something is broken.                          |
| `enhancement`      | A request for a new feature.                  |
| `documentation`    | Related to docs or guides.                    |
| `good first issue` | Beginner-friendly — perfect for newcomers.    |
| `help wanted`      | Maintainers are looking for contributors.     |

---

## Discussions

Not every conversation is about a specific task. **Discussions** are a more relaxed, forum-style space for open-ended conversation.

---

### Definition

**Discussions:**

> A GitHub feature that provides a forum-like space for open-ended conversations, questions, ideas, and community announcements — separate from task-focused issues.

---

### Issues vs Discussions

This is a common point of confusion. The simple rule: **Issues are for tasks; Discussions are for conversations.**

| **Issues**                         | **Discussions**                          |
| ---------------------------------- | ---------------------------------------- |
| Track specific, actionable work    | Open-ended conversation and Q&A          |
| Have a clear "done" state (closed) | Ongoing; no fixed resolution             |
| "Fix this bug"                     | "What features should we build next?"    |
| "Add dark mode"                    | "How do you all use this tool?"          |

> If you're not sure whether something is a real task, start a **Discussion**. Maintainers can always turn it into an issue later.

---

## Contribution Etiquette

Open source runs on goodwill. Being a respectful, considerate contributor is just as important as writing good code.

---

### The Golden Rules

1. **Read the contributing guide first.** Many projects have a `CONTRIBUTING.md` file with their rules. Follow it.
2. **Search before posting.** Your bug or question may already have an issue. Don't create duplicates.
3. **Comment before you start.** On an issue you'd like to work on, say "I'd like to work on this" so two people don't do the same task.
4. **Be patient and polite.** Maintainers are often unpaid volunteers. A "thank you" goes a long way.
5. **Keep contributions focused.** One pull request should solve one problem (remember Lesson 6).
6. **Accept feedback gracefully.** Reviews are about the code, not about you.

---

### Files You'll See in Open Source Repos

Before you fork, scan the repository root. Most serious projects include a few standard files:

| **File** | **Purpose** |
| -------- | ----------- |
| `README.md` | What the project is and how to get started |
| `CONTRIBUTING.md` | How to contribute — **read this first** |
| `LICENSE` | Legal terms for using and sharing the code |
| `CODE_OF_CONDUCT.md` | Expected community behavior |
| Issue / PR **templates** | Pre-filled forms when opening issues or PRs on GitHub |

> 💡 **Read the README and `CONTRIBUTING.md` before you fork.** They tell you what the maintainers expect — branch names, test steps, and where to ask questions.

For writing a strong README and keeping secrets out of your repo, review [Lesson 7 — .gitignore and Project Organization](07-gitignore-and-project-organization.md).

---

### The Typical Contribution Flow

This ties together everything from the bootcamp:

```
 1. Find an issue to work on      →  (Issues tab: "good first issue" or "documentation")
 2. Comment that you'll take it
 3. Fork the repository           →  (Lesson 5)
 4. Clone your fork               →  git clone ...
 5. Create a branch → commit → push to your fork
 6. Open a Pull Request           →  from your fork to the original repo (Lesson 6)
 7. PR description includes       →  Fixes #N
 8. Respond to review feedback
 9. PR merged — issue auto-closes 🎉
```

---

## Forking and Keeping Your Fork Up to Date

When you contribute to open source, you work from a **fork** — your copy of someone else's repository under your GitHub account ([Lesson 5](05-collaboration-with-github.md)). Two actions on GitHub matter before you branch:

### Star vs Fork

| **Action** | **What it does** | **When to use** |
| ---------- | ---------------- | --------------- |
| **Star** | Bookmarks the repo for you | Save projects you like or may contribute to later |
| **Fork** | Creates **your copy** under your account | You plan to push changes and open a Pull Request |

Starring does not copy the code. Forking does.

### Sync Your Fork

Your fork is a **snapshot** — it does **not** auto-update when the original repository changes.

**Sync fork:**

> Updating your fork so its default branch matches the original (upstream) repository.

**When you need to sync:**

- The original repo got new commits after you forked
- A maintainer asks you to update your branch
- Your PR shows *"This branch is out-of-date with the base branch"*

**Steps — sync on GitHub:**

1. Open **your fork** on GitHub (under your account, not the original owner).
2. If the original has moved ahead, GitHub shows **Sync fork** (or *"This branch is X commits behind"*).
3. Click **Sync fork** → **Update branch** (for `main`).
4. On your computer, pull the update:

   ```bash
   git switch main
   git pull origin main
   ```

5. Create your feature branch from fresh `main`:

   ```bash
   git switch -c fix/docs-typo
   ```

> ⚠️ **Common mistake:** Cloning the **original** repo URL when you should clone **your fork**. Always push to your fork, then open a PR into the original project.

---

## Linking Your PR to an Issue

When your PR fixes a tracked issue, say so in the **PR description**. GitHub can **close the issue automatically** when the PR merges.

Use keywords like **`Fixes #42`** or **`Closes #42`** (replace `42` with the real issue number):

```md
## What this does
Fixes a typo in the installation guide.

Fixes #42
```

| **Keyword** | **Effect when PR merges** |
| ----------- | ------------------------- |
| `Fixes #N` | Closes issue #N |
| `Closes #N` | Closes issue #N |
| `Resolves #N` | Closes issue #N |

> ⚠️ **Common mistake:** Typing the wrong issue number, or describing the fix without the keyword — the issue stays open even after merge.

---

## Good First Issues

The hardest part of open source is **starting**. Thankfully, the community created a special label just for beginners: **`good first issue`**.

---

### Definition

**Good First Issue:**

> An issue specially labeled by maintainers as simple, well-scoped, and suitable for first-time contributors.

These issues are deliberately small and well-explained, making them the perfect place to make your **first contribution** without feeling overwhelmed.

---

### How to Find Them

- On a repository, go to **Issues** and filter by the **`good first issue`** label.
- In the Issues search box, try:
  ```
  label:"good first issue" is:open
  ```
- Browse GitHub's curated page: **[github.com/topics/good-first-issue](https://github.com/topics/good-first-issue)**.
- Look for projects you actually **use and care about** — you'll be more motivated.
- **Star** repos you like; **fork** when you are ready to contribute.

---

### Tips for Your First Contribution

- **Start small.** A documentation fix or typo correction is a great first PR.
- **Read the project's README and `CONTRIBUTING.md`** before diving in.
- **Don't be afraid to ask** politely if instructions are unclear.
- **Celebrate the small win.** Your first merged PR is a real milestone. 🎉

> Many professional developers got their start by fixing a single typo in an open-source project. The first step is the most important one.

---

## Your First Open Source Contribution (Encouraged)

> You already open Pull Requests to **this bootcamp repository** when you submit assignments. This exercise is **different**: contribute to a **real open-source project** — especially a **[Goobo Labs](https://github.com/goobo-labs)** repository.

**Goal:** Make one small contribution outside the bootcamp repo — a docs fix, typo correction, or labeled **`good first issue`**.

This exercise is **encouraged**, not graded like Assignment 1. A merged PR (or a submitted PR awaiting review) is a real portfolio milestone.

---

### Steps

1. **Browse Goobo Labs projects**
   - Visit **[github.com/goobo-labs](https://github.com/goobo-labs)** (your instructor may suggest specific repos)
   - Pick a project with an open **`good first issue`**, **`documentation`**, or **`help wanted`** label — or a clear typo in the docs

2. **Claim the work**
   - Find or open an issue describing the change
   - Comment politely: *"I'd like to work on this"* — wait for a maintainer to confirm if the project asks you to

3. **Fork, sync, and clone**
   - On the **original** repo page, click **Fork** (top right) to copy it to your account.
   - Open **your fork** → if needed, click **Sync fork** → **Update branch** so you start from the latest code.
   - Clone **your fork** (not the original URL):
   ```bash
   git clone https://github.com/your-username/some-project.git
   cd some-project
   git remote -v
   ```

4. **Branch, change, commit, push**
   ```bash
   git switch -c fix/docs-typo
   # edit the file
   git add .
   git commit -m "Fix typo in installation guide"
   git push -u origin fix/docs-typo
   ```

5. **Open a Pull Request to the original repo**
   - On GitHub, open a PR **from your fork** → **goobo-labs/some-project** (not into your own fork's `main` by mistake)
   - Write a clear title and description
   - Include **`Fixes #N`** if an issue exists

6. **Respond to review feedback**
   - If a maintainer requests changes, push more commits to the **same branch** — the PR updates automatically (Lesson 6)

---

### Done When

- [ ] You commented on an issue (or opened one) **before** you started coding.
- [ ] Your PR targets the **original** repository, not only your fork.
- [ ] Your PR description includes **`Fixes #N`** when an issue applies.

**Next:** [Lesson 9 — GitHub Actions Introduction](09-github-actions-introduction.md). After that, [Lesson 10 — Putting It All Together](10-putting-it-all-together.md) is your capstone walkthrough.

---

## Summary

- **Open source** is publicly available software anyone can use, study, and improve — and GitHub is its home.
- **Issues** track specific work: bug reports, feature requests, and tasks. Write them clearly with steps to reproduce.
- **Discussions** are forum-style conversations for open-ended questions and ideas.
- **Contribution etiquette** matters: read the guides, search first, claim issues, and be patient and polite.
- Look for **`README.md`**, **`CONTRIBUTING.md`**, **`LICENSE`**, and **`CODE_OF_CONDUCT.md`** before you contribute.
- Link PRs to issues with **`Fixes #N`** so GitHub closes the issue when the PR merges.
- **Star** to bookmark a repo; **fork** to contribute. **Sync your fork** before branching when the original has changed.
- The **`good first issue`** label marks beginner-friendly tasks — the perfect place to make your first contribution.
- The **encouraged exercise** targets a real OSS project (especially Goobo Labs) — separate from assignment PRs to this bootcamp repo.
- Contributing uses every skill you've learned: fork, clone, branch, commit, push, and pull request.

---

*End of Lesson 8*

---
