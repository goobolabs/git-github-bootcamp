# Lesson 3 – Branching

> So far we've worked in a single straight line of commits. Real projects rarely move in a straight line. This lesson introduces **branches** — Git's way to work on separate ideas without touching `main`.

> **NB:** This lesson covers **branches**, **`git stash`**, and **`git restore`**. **Merging** and **merge conflicts** are covered in Lesson 6.

---

## What You'll Learn

By the end of this lesson, students will be able to:

1. Explain **why branches exist** and what problems they solve.
2. **Create** and **switch** between branches.
3. Use **`git branch`** to see which branch you are on.
4. Use **`git restore`** to discard uncommitted edits or unstage a file.
5. Use **`git stash`** to temporarily save work when switching branches.

---

## Why Branches Exist

Imagine your project's main version is live and working. Now you want to add a risky new feature. If you edit the main version directly and something breaks, you've broken the working project for everyone.

A **branch** solves this. It lets you create a separate, parallel line of work where you can experiment freely. If it works, you bring it back into the main project. If it fails, you simply throw the branch away — the main version was never touched.

---

### Definition

**Branch:**

> An independent line of development that lets you work on changes in isolation, without affecting the main version of the project.

By default, every Git repository starts with one branch, usually called **`main`**. Think of it as the "official, trusted" version of your project.

---

### A Real-World Analogy

Think of writing a book ✍️:

- The **`main` branch** is the published manuscript everyone reads.
- A **new branch** is a private draft where you try a new chapter.
- If the chapter is good, you'll bring it back into the manuscript.
- If it's bad, you discard the draft — the published book is untouched.

---

### Why Branches Are So Useful

| **Situation**                       | **How Branches Help**                                    |
| ----------------------------------- | -------------------------------------------------------- |
| Building a new feature              | Develop it separately on its own branch.                 |
| Fixing a bug urgently               | Create a quick fix branch without disturbing other work. |
| Trying an experiment                | Test freely; delete the branch if it doesn't work out.   |
| Many people on one project          | Each person works on their own branch (Lesson 5).        |

> Branches are **cheap and fast** in Git — creating one takes a fraction of a second. This is a big reason Git won (remember Lesson 0).

---

### Visualizing a Branch

```
main:     A ─── B ─── C
                       \
feature:                D ─── E
```

- Commits `A`, `B`, `C` are on `main`.
- You created a `feature` branch at `C` and added commits `D` and `E`.
- `main` is completely unaffected while you work on `feature`.

---

## Creating Branches

There are two common ways to create a branch. The modern, recommended command is `git switch`.

---

### Create a New Branch

```bash
# Modern way: create a branch AND switch to it
git switch -c feature-login

# Older equivalent (still very common):
git checkout -b feature-login
```

This creates a branch named `feature-login` based on your current branch, and moves you onto it.

---

### See Your Branches

```bash
git branch
```

Output (the `*` marks your current branch):

```
* feature-login
  main
```

> 💡 **Naming tip:** Use clear, descriptive branch names like `feature-login`, `fix-navbar`, or `update-readme`. Avoid vague names like `test` or `new`.

---

## Switching Branches

To move between existing branches, use `git switch`:

```bash
# Switch to the main branch
git switch main

# Switch back to your feature branch
git switch feature-login
```

When you switch, Git instantly changes the files in your working directory to match that branch. It feels like the project transforms before your eyes.

⚠️ **Common mistake:** Trying to switch branches with unsaved changes. **Commit** your work, **`git stash`** it to keep it, or **`git restore`** it to throw it away — then switch.

---

## Discarding Changes with `git restore`

Before you switch branches, sometimes you edited a file and decide you **don't want those changes at all**. **`git restore`** throws away uncommitted edits or removes a file from the staging area.

---

### Definition

**Restore:**

> Return a file in your working directory or staging area to a previous state — usually back to how it looked at the last commit.

---

### How to Restore

```bash
# Discard uncommitted edits in a file (back to last commit)
git restore notes.txt

# Unstage a file — keep your edits, remove from staging area
git restore --staged notes.txt
```

| **Situation**                        | **Command**                   |
| ------------------------------------ | ----------------------------- |
| "I edited a file and want to undo"   | `git restore <file>`          |
| "I staged the wrong file by mistake" | `git restore --staged <file>` |

> ⚠️ **`git restore <file>` throws away uncommitted edits.** There is no undo — make sure you really want to discard them.

When you need to **keep** uncommitted work but switch branches, use **`git stash`** instead (next section).

| **Goal**                         | **Use**              |
| -------------------------------- | -------------------- |
| Keep changes, switch branch      | `git stash`          |
| Throw away changes, switch branch| `git restore <file>` |
| Save changes permanently         | `git add` + `git commit` |

---

## Stashing Changes

Sometimes you're halfway through editing a file and need to switch branches — but you're not ready to commit. **`git stash`** temporarily hides your uncommitted changes so your working directory is clean.

---

### Definition

**Stash:**

> A temporary storage area where Git saves your uncommitted changes so you can switch branches or pull updates, then bring the changes back later.

Think of it like putting your papers in a drawer while you clean the desk — the work isn't gone, it's just out of the way.

---

### How to Stash

```bash
# Save uncommitted changes and clean the working directory
git stash

# Switch branches, do other work...
git switch main

# Come back and restore your saved changes
git switch feature-login
git stash pop
```

| **Command**        | **What It Does**                                      |
| ------------------ | ----------------------------------------------------- |
| `git stash`        | Saves uncommitted changes and clears your working dir |
| `git stash pop`    | Restores the most recent stash and removes it         |
| `git stash list`   | Shows all saved stashes                               |

> 💡 If `git stash pop` causes a conflict, resolve it the same way you would a merge conflict (Lesson 6).

---

### A Typical Branch Workflow

```bash
# 1. Start from main
git switch main

# 2. Create and move to a new branch
git switch -c feature-contact-form

# 3. Do your work: edit files
#    ... make changes ...

# 4. Stage and commit on the branch
git add .
git commit -m "Add contact form"

# 5. Switch back to main when you're done experimenting
git switch main
```

---

## Exercise — Branch Practice

> **Prerequisite:** Complete **Exercise 1** in [Lesson 2](02-git-basics.md) first (100 commits in `lesson-2-practice`).

Practice creating branches and switching between them. Do each step until the commands feel natural.

**Goal:** Create **5 branches**, make at least **1 commit** on each, switch back to `main` when you're done, and practice **`git restore`** and **`git stash`** at least **2** times each.

---

### Minimum practice counts

| **Command**     | **Minimum times** | **Notes** |
| --------------- | ----------------- | --------- |
| `git switch -c` | **5**             | Create 5 different branches. |
| `git switch`    | **15**            | Move between `main` and feature branches. |
| `git branch`    | **10**            | List branches after creating and switching. |
| `git status`    | **20**            | Check state before and after each switch. |
| `git restore`   | **2**             | Discard uncommitted edits before switching. |
| `git stash`     | **2**             | Save uncommitted work before switching. |
| `git stash pop` | **2**             | Restore stashed work when you return. |

---

### The workflow (repeat this)

**Create a branch and work on it:**

```bash
git switch main
git status
git switch -c feature-about
git branch
# edit a file, then:
git add about.txt
git commit -m "Add about section on feature-about branch"
git status
git switch main
git branch
```

**Discard uncommitted edits before switching:**

```bash
git status
git restore notes.txt
git status
git switch main
```

**Stash uncommitted work before switching:**

```bash
git status
git stash
git status
git switch main
git switch feature-about
git stash pop
git status
```

---

### Steps

1. **Open your project from Exercise 1**
   ```bash
   cd lesson-2-practice
   git switch main
   git branch
   git status
   ```

2. **Create 5 branches** — use clear names, for example:
   - `feature-about`
   - `feature-skills`
   - `feature-notes`
   - `feature-readme`
   - `feature-footer`

   For **each** branch:
   - `git switch main`
   - `git switch -c <branch-name>`
   - Edit or create a file
   - Commit with a clear message
   - Run `git branch` and `git status`
   - Switch back to `main`: `git switch main`

3. **Practice `git restore` at least 2 times**
   - On a feature branch, edit a file but **do not commit**
   - Run `git restore <file>` — confirm the edits are gone and `git status` is clean
   - `git switch main`, then switch back and try again on a **different** file or branch

4. **Practice `git stash` at least 2 times**
   - On one of your feature branches, edit a file but **do not commit**
   - Run `git stash` — confirm `git status` shows a clean working tree
   - `git switch main`, then switch back to that branch
   - Run `git stash pop` — confirm your edits are back
   - Repeat once on a **different** branch

5. **Switch between your branches**
   - Use `git switch` to visit each branch again
   - Run `git branch` and `git status` each time
   - Confirm the `*` shows which branch you're on

6. **Review your work**
   ```bash
   git branch
   git log --oneline
   git status
   ```
   You should end on **`main`** with a clean working tree and **5 feature branches** in your project.

---

### Done When

- [ ] You created **5 branches** with `git switch -c`.
- [ ] You made at least **1 commit** on each branch.
- [ ] You switched back to `main` after finishing each branch.
- [ ] You ran `git switch` **at least 15** times and `git branch` **at least 10** times.
- [ ] You ran `git restore` **at least 2** times.
- [ ] You ran `git stash` and `git stash pop` **at least 2** times each.
- [ ] You end on `main` with `git status` showing a clean working tree.

**Next:** Read Lesson 4, then complete **Exercise 3 — Push to GitHub** at the end of that lesson.

---

## Summary

- A **branch** is an independent line of work that protects the `main` version from unfinished or risky changes.
- Branches are cheap and fast, making them perfect for features, fixes, and experiments.
- Create and switch with `git switch -c <name>` and `git switch <name>`.
- Use `git branch` to see all branches and which one is active (`*`).
- Use **`git restore`** to discard edits or unstage a file before switching branches.
- Use **`git stash`** and **`git stash pop`** to pause work when you're not ready to commit.

---

*End of Lesson 3*

---
