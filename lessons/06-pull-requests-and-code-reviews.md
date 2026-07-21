# Lesson 6 – Pull Requests and Code Reviews

> In Lesson 5 we said teams merge their work through **Pull Requests**. This lesson covers **`git merge`**, **merge conflicts**, Pull Requests, and code review — the habits that make collaboration smooth and professional.

---

## What You'll Learn

By the end of this lesson, students will be able to:

1. Explain what a **Pull Request (PR)** is and why teams use them.
2. **Merge** one branch into another with `git merge`.
3. Understand what a **merge conflict** is and how to resolve it calmly.
4. **Review changes** in a Pull Request and leave helpful feedback.
5. **Merge** a Pull Request safely on GitHub.
6. Use **`git reset`** to remove a commit locally (before it is shared).
7. Use **`git revert`** to safely undo a commit that is already shared.
8. Apply **best practices** for writing and reviewing Pull Requests.

---

## What is a Pull Request?

When you finish work on a branch, you don't just merge it into `main` yourself. Instead, you **propose** the change and ask the team to look at it first. That proposal is called a **Pull Request**.

---

### Definition

**Pull Request (PR):**

> A request to merge the changes from one branch into another, giving teammates a chance to review, discuss, and approve the work before it becomes part of the main project.

The name makes sense: you are requesting that the project **pull in** your changes. (On GitLab, the same idea is called a "Merge Request.")

---

### Why Pull Requests Matter

A Pull Request is much more than a "merge button." It creates a moment for the team to catch problems and share knowledge:

- **Quality:** Bugs and mistakes get caught before they reach `main`.
- **Discussion:** Teammates can ask questions and suggest improvements.
- **Knowledge sharing:** Everyone learns how the project is evolving.
- **A written record:** The PR documents *what* changed and *why*, forever.

> Think of a Pull Request like submitting an essay for **peer review** before it gets published. A second pair of eyes catches what you missed.

---

### Where a PR Fits in the Workflow

```
 1. Create a branch       →  git switch -c feature-login
 2. Commit your work      →  git add . && git commit -m "..."
 3. Push the branch       →  git push -u origin feature-login
 4. Open a Pull Request   →  on GitHub (in the browser)
 5. Review & discuss      →  teammates leave feedback
 6. Merge the PR          →  changes join main
 7. Delete the branch     →  clean up
```

Notice this builds directly on Lessons 3, 4, and 5 — the branch, the push, and now the review.

---

## Opening a Pull Request

After you've pushed a branch (step 3 above), opening the PR happens on GitHub:

1. Go to your repository on GitHub. You'll often see a banner: **"Compare & pull request."** Click it. (Or click the **Pull requests** tab → **New pull request**.)
2. Choose the **base** branch (where the changes will go, usually `main`) and the **compare** branch (your feature branch).
3. Write a clear **title** and **description** explaining what you did and why.
4. Click **Create pull request**.

That's it — your work is now visible for the team to review.

---

### Writing a Good PR Description

A strong description helps reviewers understand your work quickly. A simple template:

```
## What this does
Adds a login form to the homepage.

## Why
Users requested a way to sign in directly from the landing page.

## How to test
1. Open index.html
2. Click "Login"
3. The form should appear
```

---

## Reviewing Changes

Once a PR is open, teammates **review** it. Reviewing means reading the proposed changes and giving feedback before approving.

---

### How Reviewing Works on GitHub

In the **Files changed** tab of a PR, GitHub highlights exactly what was added and removed:

- **Green lines** (with `+`) were **added**.
- **Red lines** (with `-`) were **removed**.

Reviewers can click any line to leave a **comment**, ask a question, or suggest an improvement. When done, a reviewer chooses one of three outcomes:

| **Review Outcome**     | **Meaning**                                            |
| ---------------------- | ------------------------------------------------------ |
| **Approve**            | The changes look good and can be merged.               |
| **Request changes**    | Something needs to be fixed before merging.            |
| **Comment**            | General feedback, without approving or blocking.       |

---

### Responding to a Review

If a reviewer requests changes, you don't open a new PR. You simply:

1. Make the fixes on the **same branch** locally.
2. Commit and push again:

   ```bash
   git add .
   git commit -m "Address review feedback: fix label text"
   git push
   ```

The Pull Request **updates automatically** with your new commits. The reviewer can then approve.

> 💡 This is why we keep working on the *same branch* — the PR tracks that branch and refreshes as you push.

---

## Merging Branches

Before we merge on GitHub, you need to understand **`git merge`** on your computer. In Lesson 3 you created branches; now you bring a branch's work back into `main`.

---

### Definition

**Merge:**

> The process of combining the changes from one branch into another, uniting two separate lines of work into one.

---

### How to Merge

The golden rule: **you merge *into* the branch you are currently on.** Switch to the destination (usually `main`), then merge the feature branch in.

```bash
# 1. Switch to the branch you want to merge INTO
git switch main

# 2. Merge the feature branch into main
git merge feature-contact-form
```

After this, `main` contains all the commits from `feature-contact-form`.

```
Before merge:
main:     A ─── B ─── C
                       \
feature:                D ─── E

After merging feature into main:
main:     A ─── B ─── C ─────────── F
                       \           /
feature:                D ─── E ───
```

(`F` is the new "merge commit" that ties the two lines together.)

---

### Cleaning Up After a Merge

Once a branch is merged, you usually don't need it anymore:

```bash
git branch -d feature-contact-form
```

The commits live on safely inside `main`.

---

## Merge Conflicts

Most merges are smooth and automatic. But sometimes Git gets stuck — that's a **merge conflict**. New learners often fear conflicts, but they are normal and easy to fix once you understand them.

---

### Definition

**Merge Conflict:**

> A situation that happens when two branches change the **same lines** of the **same file** in different ways, so Git can't decide which version to keep — and asks you to choose.

---

### Why Conflicts Happen

Git is smart, but it can't read your mind. If two branches edited the same line differently, Git doesn't know which one is correct. So it pauses and asks **you** to decide.

Example: both branches changed line 1 of `index.html`.

- `main` changed it to: `<h1>Welcome</h1>`
- `feature` changed it to: `<h1>Hello There</h1>`

Git can't pick one for you.

---

### What a Conflict Looks Like

When you merge, Git marks the conflict inside the file like this:

```
<<<<<<< HEAD
<h1>Welcome</h1>
=======
<h1>Hello There</h1>
>>>>>>> feature-login
```

| **Marker**      | **Meaning**                                      |
| --------------- | ------------------------------------------------ |
| `<<<<<<< HEAD`  | Start of the version from your current branch.   |
| `=======`       | Divider between the two versions.                |
| `>>>>>>> ...`   | End — the version from the branch you're merging.|

---

### How to Resolve a Conflict

Resolving a conflict is a calm, three-step process:

1. **Open the file** and decide what the final version should be. Edit it by hand, **removing the `<<<<<<<`, `=======`, and `>>>>>>>` markers**.

   For example, you might decide the final line is:

   ```html
   <h1>Welcome — Hello There</h1>
   ```

2. **Stage the resolved file:**

   ```bash
   git add index.html
   ```

3. **Complete the merge with a commit:**

   ```bash
   git commit -m "Merge feature-login and resolve heading conflict"
   ```

That's it — the conflict is resolved.

> ⚠️ **Common mistake:** Forgetting to delete the `<<<<<<<` / `=======` / `>>>>>>>` markers. If you leave them in, your code will break. Always remove them while resolving.

---

### Tips to Avoid Painful Conflicts

- Commit and merge **often** — small, frequent merges cause fewer conflicts than one giant merge.
- Communicate with teammates so two people don't edit the same lines at once.
- Keep branches **short-lived**: finish a feature and merge it rather than letting a branch drift for weeks.

---

## Removing a Commit with `git reset`

Sometimes you commit too soon — wrong message, wrong files, or you want to fix something before anyone else sees it. **`git reset`** moves your branch **backward** to an older commit. It **removes** the latest commit from your branch history. It does **not** create a new commit.

Use this on **local work you have not pushed yet** (or only on your own branch that nobody else depends on).

---

### Definition

**Reset:**

> Moving the current branch pointer to an older commit, optionally changing what stays in your staging area and working files.

Think of it like moving a bookmark backward in the book — not writing a new page.

---

### The three modes

| **Mode** | **Commit removed?** | **Changes kept?** | **Where?** |
| -------- | ------------------- | ----------------- | ---------- |
| `--soft` | Yes | Yes | Still **staged** |
| `--mixed` (default) | Yes | Yes | In your **files**, unstaged |
| `--hard` | Yes | **No** — discarded | Gone |

---

### How to remove the latest commit

**Keep the changes, still staged** (good for fixing the commit message or adding more files):

```bash
git reset --soft HEAD~1
git status
```

**Keep the changes, but unstaged** (good for editing before you commit again):

```bash
git reset HEAD~1
git status
```

**Remove the commit and throw away its changes** (use only when you're sure):

```bash
git reset --hard HEAD~1
```

`HEAD~1` means "one commit before the current one." Use `HEAD~2` to go back two commits, and so on.

---

### Example

```bash
git log --oneline
# abc1234 Bad commit I want gone
# def5678 Good commit

git reset --soft HEAD~1

git log --oneline
# def5678 Good commit        ← the bad commit is no longer on this branch

git status
# changes from the bad commit are still staged — edit and commit again
```

---

### Reset vs revert — when to use which

| **Situation** | **Use** |
| ------------- | ------- |
| Last commit is **only on your computer** — you want it **gone** | `git reset` |
| Commit is **already on GitHub** and others may have pulled it | `git revert` |
| You want to **keep history visible** on a shared repo | `git revert` |

> ⚠️ **Common mistake:** Using `git reset --hard` without checking `git status` first — you can lose work permanently. Prefer `--soft` or `--mixed` until you're sure.

> ⚠️ **Common mistake:** Resetting commits you've already pushed, then running `git push --force`. That rewrites shared history and can break things for teammates. On shared repos, prefer **`git revert`**.

---

## Reverting a Commit

What if a bad commit is **already on GitHub** and other people have pulled it? You can't erase history safely on a shared repo. Instead, use **`git revert`** — it creates a **new commit** that undoes the changes.

---

### Definition

**Revert:**

> Creating a new commit that reverses the changes from a previous commit, without deleting history.

---

### How to Revert

```bash
# Undo the most recent commit
git revert HEAD

# Undo a specific commit (use its hash from git log)
git revert abc1234
```

Git opens your editor for the revert commit message. Save and close to finish. Then push:

```bash
git push
```

The original commit stays in history — the revert commit cancels out its changes. That's why revert is safe for shared projects. For local-only mistakes, **`git reset`** (above) removes the commit instead of adding a new one.

---

## Merging Pull Requests

Once a PR is approved, it's time to **merge** it — combining your branch into `main`.

On GitHub, you click the **Merge pull request** button, then **Confirm merge**. GitHub does the merge in the cloud, so you don't need to run `git merge` yourself.

---

### After Merging

1. **Delete the branch.** GitHub offers a **Delete branch** button right after merging — click it to keep things tidy.
2. **Update your local `main`** so your computer matches the remote:

   ```bash
   git switch main
   git pull
   ```

Now your local project includes the freshly merged changes, and you're ready for the next task.

---

### Merge Conflicts in a Pull Request

Sometimes GitHub shows: *"This branch has conflicts that must be resolved."* That means two branches changed the same lines — the same kind of **merge conflict** you learned above.

Fix it locally:

1. Switch to your feature branch and pull the latest `main` into it (or merge `main` into your branch).
2. Open the conflicted files and remove the `<<<<<<<`, `=======`, and `>>>>>>>` markers.
3. Stage, commit, and push:

   ```bash
   git add .
   git commit -m "Resolve merge conflict with main"
   git push
   ```

The PR updates and becomes mergeable again.

---

## Best Practices

Following a few simple habits makes Pull Requests pleasant for everyone.

---

### For the Author (You)

- **Keep PRs small.** A small PR is easy to review; a huge one is overwhelming.
- **One purpose per PR.** Don't mix an unrelated bug fix into a feature PR.
- **Write a clear title and description.** Explain the *what* and the *why*.
- **Review your own changes first.** Read the diff before asking others to.
- **Respond politely to feedback.** Reviews improve the code, not attack you.

---

### For the Reviewer

- **Be kind and specific.** "Could we rename this for clarity?" beats "this is wrong."
- **Ask questions** instead of giving orders.
- **Praise good work**, not just problems.
- **Focus on what matters:** correctness and clarity over personal style.

| **Helpful Comment**                          | **Unhelpful Comment** |
| -------------------------------------------- | --------------------- |
| "Consider handling the empty-list case here."| "This is bad."        |
| "Nice clean solution! One small idea: ..."   | "No."                 |
| "What happens if the file doesn't exist?"    | "Wrong."              |

> ⚠️ **Common mistake:** Treating a review as criticism of the *person*. Code review is about improving the *code* — stay friendly and assume good intent on both sides.

---

## Summary

- A **Pull Request (PR)** proposes merging one branch into another, allowing review before changes reach `main`.
- **`git merge`** combines a branch into the branch you're on (usually merge feature branches into `main`).
- A **merge conflict** happens when the same lines change in two branches — resolve it by editing the file, removing the markers, then `git add` and `git commit`.
- **`git reset`** removes a commit locally by moving the branch backward (`--soft`, `--mixed`, or `--hard`).
- **`git revert`** safely undoes a shared commit by adding a new commit that reverses it.
- PRs improve quality, enable discussion, share knowledge, and create a permanent record.
- Workflow: branch → commit → push → open PR → review → merge → delete branch.
- **Reviewers** can approve, request changes, or comment; authors respond by pushing more commits to the same branch.
- After merging, delete the branch and run `git pull` on `main` to stay in sync.
- **Best practices:** keep PRs small and focused, write clear descriptions, and keep reviews kind and constructive.

---

*End of Lesson 6*

---
