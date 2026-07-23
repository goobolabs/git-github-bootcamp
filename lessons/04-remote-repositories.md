# Lesson 4 – Remote Repositories

> Up to now, everything has lived on your computer. In this lesson we connect your local project to the cloud — putting your code on **GitHub** so it's backed up and ready to share.

---

## What You'll Learn

By the end of this lesson, students will be able to:

1. Explain the difference between **local** and **remote** repositories.
2. Create a repository on **GitHub** and connect it to a local project.
3. Understand what **`origin`** means.
4. Use **`git push`**, **`git pull`**, and **`git fetch`** to sync work between local and remote.

---

## Local vs Remote Repositories

Everything you did in Lesson 2 happened in a **local repository** — the copy of the project on your own machine. A **remote repository** is a copy of that same project hosted somewhere else, usually on a server like GitHub.

---

### Definition

**Remote Repository:**

> A version of your Git repository hosted on a server (such as GitHub), used as a shared, central copy that you and others can sync with.

Because Git is **distributed** (remember Lesson 0), the local and remote copies each hold the full history. You connect them so changes can flow back and forth.

---

### Local vs Remote at a Glance

| **Local Repository**         | **Remote Repository**                  |
| ---------------------------- | -------------------------------------- |
| Lives on **your computer**   | Lives on a **server** (e.g., GitHub)   |
| Where you do your daily work | The shared "official" copy             |
| Works offline                | Accessed over the internet             |
| Private to you               | Can be shared with a team or the world |

---

### Why You Need a Remote

- **Backup:** If your laptop breaks, your code is safe in the cloud.
- **Sharing:** Others can see and use your project.
- **Collaboration:** Teammates sync their work through the remote.
- **Portfolio:** Your GitHub profile showcases your projects to the world.

```
   Your Computer                          GitHub (Cloud)
 ┌─────────────────┐    push  ───►   ┌─────────────────────┐
 │ Local Repository│                 │  Remote Repository  │
 │  (your work)    │   ◄───  pull    │   (shared copy)     │
 └─────────────────┘                 └─────────────────────┘
```

---

## Creating a GitHub Repository

To get a remote, you first create an empty repository on GitHub:

1. Log in to [github.com](https://github.com).
2. Click the **+** in the top-right corner and choose **New repository**.
3. Give it a **name** (for example, `my-project`).
4. Choose **Public** (anyone can see) or **Private** (only you and invited people).
5. For now, **don't** add a README — we'll connect an existing local project.
6. Click **Create repository**.

GitHub will then show you a page with a URL like:

```
https://github.com/your-username/my-project.git
```

This URL is the address of your new remote.

---

## Understanding `origin`

When you connect a local repo to a remote, you give the remote a short nickname so you don't have to type the long URL every time. By convention, that nickname is **`origin`**.

---

### Definition

**`origin`:**

> The default name Git gives to the main remote repository your project is connected to. It's simply a shortcut for the remote's URL.

So instead of typing the full `https://github.com/...` URL repeatedly, you just say `origin`.

---

### Connecting Local to Remote

Inside your local project folder, link it to the GitHub remote:

```bash
# Connect your local repo to the remote, naming it "origin"
git remote add origin https://github.com/your-username/my-project.git

# Confirm the connection
git remote -v
```

Output of `git remote -v`:

```
origin  https://github.com/your-username/my-project.git (fetch)
origin  https://github.com/your-username/my-project.git (push)
```

✅ Your local and remote repositories are now linked.

---

## Changing the Remote URL

The nickname **`origin`** stays the same even when the repository URL changes — for example, after you rename your GitHub repository or your local folder. You do **not** need to remove the remote and add it again. Update the URL instead:

```bash
# See where origin points now
git remote -v

# Point origin at the new URL
git remote set-url origin https://github.com/your-username/new-repo-name.git

# Confirm the change
git remote -v
```

On GitHub, you can rename a repository anytime: open the repo → **Settings** → **General** → **Repository name** → type the new name → **Rename**. GitHub redirects the old URL for a while, but you should still update `origin` locally so your commands match the real name.

---

## Authenticating with GitHub

Before your first push, GitHub needs to know it's really you. You do **not** need SSH keys or a manually copied token for this course — use one of the simpler options below.

---

### Option 1 — GitHub CLI *(recommended, easiest)*

Install [GitHub CLI](https://cli.github.com/) (`gh`), then sign in once through your browser. Git will reuse that login automatically.

```bash
gh auth login
```

When prompted, choose:

1. **GitHub.com**
2. **HTTPS**
3. **Yes** — authenticate Git with your GitHub credentials
4. **Login with a web browser** — copy the code, press Enter, paste the code in the browser, and approve

After that, `git push` and `git pull` work without typing a token each time.

Check that it worked:

```bash
gh auth status
```

---

### Option 2 — Sign in when Git asks *(no extra setup on many computers)*

On some systems, the first time you run `git push`, a **browser window opens** and you sign in to GitHub there (via **Git Credential Manager**). Approve the login once — Git remembers it.

If that happens, you're done. No token to create or paste.

> If nothing opens and Git only asks for username/password in the terminal, use **Option 1** or **Option 3** below.

---

### Option 3 — Personal Access Token *(manual fallback)*

Use this only if Options 1 and 2 are not available. When you use HTTPS (the URL ending in `.git`), Git may ask for credentials in the terminal:

1. **Username:** your GitHub username
2. **Password:** **not** your GitHub account password — paste a **Personal Access Token (PAT)**

To create a token:

1. Log in to [github.com](https://github.com).
2. Go to **Settings → Developer settings → Personal access tokens**.
3. Create a token with permission to access **repositories**.
4. Copy the token and paste it when Git asks for a password.

> ⚠️ **Common mistake:** Using your GitHub login password when `git push` asks for a password. GitHub requires a token for HTTPS pushes when you type credentials manually.

Save the token somewhere safe — you won't see it again after you leave the page.

---

## `git push` — Sending Work to the Remote

**Pushing** uploads your local commits to the remote repository. This is how your work gets to GitHub.

---

### Definition

**Push:**

> Uploading commits from your local repository to a remote repository.

```bash
# The first push: send the "main" branch and remember the connection
git push -u origin main
```

- `-u origin main` links your local `main` branch to the remote `main` branch.
- After this first push, you only need to type `git push` from then on.

```bash
# Every push after the first one
git push
```

> ⚠️ **Common mistake:** Forgetting to **commit** before pushing. `git push` only sends **committed** snapshots. If your changes aren't committed (Lesson 2), there's nothing to push.

---

## `git pull` — Getting Work From the Remote

**Pulling** downloads changes from the remote and updates your local project. You use this when teammates have pushed work, or when you changed something directly on GitHub.

---

### Definition

**Pull:**

> Downloading changes from a remote repository and **merging** them into your current local branch.

```bash
git pull
```

A `git pull` is actually two steps combined:

1. **Download** the new commits from the remote.
2. **Merge** them into your current branch.

> 💡 **Good habit:** Run `git pull` before you start working each day, so you begin with the latest version and avoid conflicts.

---

## `git fetch` — Looking Before You Leap

**Fetching** downloads changes from the remote **but does not merge them** into your work. It lets you *see* what's new before deciding to combine it.

---

### Definition

**Fetch:**

> Downloading the latest changes from a remote repository **without** merging them into your local branch.

```bash
git fetch
```

After fetching, you can inspect what changed, and then merge when you're ready.

---

### Pull vs Fetch

This is a common point of confusion. Here's the key difference:

| **`git fetch`**                | **`git pull`**                              |
| ------------------------------ | ------------------------------------------- |
| Downloads changes              | Downloads changes                           |
| Does **not** change your files | **Merges** changes into your current branch |
| Safe — just "looks"            | Updates your working files immediately      |
| `fetch` = preview              | `pull` = `fetch` + `merge`                  |

> Simple rule: **`git pull` = `git fetch` + `git merge`.**

---

## The Complete Remote Workflow

Here's how the local commands you already know connect to the remote:

```bash
# --- One-time setup ---
git remote add origin https://github.com/your-username/my-project.git

# --- Daily work ---
git pull                      # 1. Get the latest from the remote
# ... edit files ...
git add .                     # 2. Stage your changes
git commit -m "Add feature"   # 3. Save a local snapshot
git push                      # 4. Upload your snapshot to GitHub
```

---

### The Full Picture

```
 Working Dir ──add──► Staging ──commit──► Local Repo ──push──► Remote (GitHub)
                                              ▲                      │
                                              └──────── pull ────────┘
```

This diagram extends the three-area model from Lesson 2, with the remote added on the end. Master this loop and you've mastered everyday Git.

---

## Exercise — Push to GitHub

> **Before you start:**
> 1. Complete **Exercise 1** in [Lesson 2](02-git-basics.md) — 100 commits in `lesson-2-practice`.
> 2. Complete **Exercise 2** in [Lesson 3](03-branching.md) — **5 branches**, at least **1 commit** on each, plus `git restore` and `git stash` practice.

Use the same project from Exercises 1 and 2 — do not start a new one.

**Goal:** Push your project to GitHub, then make **10 more commits** on `main` (messages **`101 -`** through **`110 -`**).

---

### Minimum practice counts

| **Command**               | **Minimum times** | **Notes**                                 |
| ------------------------- | ----------------- | ----------------------------------------- |
| `git remote add`          | **1**             | Connect local repo to GitHub.             |
| `git remote -v`           | **5**             | Confirm the remote URL.                   |
| `git push -u origin main` | **1**             | First push — uploads your `main` history. |
| `git push`                | **10**            | After each new commit on `main`.          |
| `git pull`                | **3**             | Download changes from GitHub.             |
| `git fetch`               | **3**             | Preview remote changes without merging.   |

---

### The workflow (repeat this)

**Connect and push — run once:**

```bash
cd lesson-2-practice
git switch main
git remote add origin https://github.com/your-username/my-project.git
git remote -v
git push -u origin main
```

**After each new commit on `main`:**

```bash
git status
git add <file>
git status
git commit -m "101 - what you changed"
git push
git remote -v
```

**Sync with GitHub:**

```bash
git pull
git status
git fetch
git status
```

---

### Steps

1. **Confirm Exercises 1 and 2 are done**
   ```bash
   cd lesson-2-practice
   git switch main
   git branch
   git status
   git log --oneline
   ```
   You should be on **`main`**, with a **clean** working tree, **5 feature branches**, and your last numbered commit starting with **`100 -`**.

2. **Create an empty repository on GitHub**
   - Log in to [github.com](https://github.com)
   - **New repository** → name it (for example `my-project`)
   - **Do not** add a README, `.gitignore`, or license
   - Copy the HTTPS URL

3. **Connect your local repo to GitHub**
   ```bash
   git remote add origin https://github.com/your-username/my-project.git
   git remote -v
   ```

4. **Push your full history on `main`**
   ```bash
   git push -u origin main
   ```
   Use your GitHub username and sign in when prompted — **GitHub CLI** or a **browser login** is enough; you only need a **Personal Access Token** if Git asks for a password in the terminal and nothing else works (see above).

5. **Verify on GitHub**
   - Open your repo in the browser
   - Check **Commits** on **`main`** — your Exercise 1 history should be there
   - Check **Code** — your files should be visible
   - Your **5 feature branches** from Exercise 2 stay local for now (that is normal)

6. **Practice `git pull` at least 3 times**
   - On GitHub, edit a text file and commit the change on the website
   - Locally:
     ```bash
     git pull
     git status
     ```
   - Confirm the change arrived. Repeat until you have used `git pull` **at least 3** times

7. **Make 10 commits on `main` and push**
   - Continue numbering from Exercise 1:
     ```bash
     git commit -m "101 - Added a new note"
     git commit -m "102 - Updated README"
     # ...
     git commit -m "110 - Tenth push practice commit"
     ```
   - After each commit (or every few commits):
     ```bash
     git push
     git remote -v
     ```

8. **Practice `git fetch` at least 3 times**
   ```bash
   git fetch
   git status
   ```

---

### Done When

- [ ] **Exercise 1** and **Exercise 2** are complete.
- [ ] **`lesson-2-practice`** is connected to GitHub (`git remote -v` shows `origin`).
- [ ] Your **`main`** history is visible on GitHub after the first push.
- [ ] You ran `git remote -v` **at least 5** times.
- [ ] You ran `git push` **at least 10** times (after new commits on `main`).
- [ ] You ran `git pull` **at least 3** times and `git fetch` **at least 3** times.
- [ ] Commits **`101 -`** through **`110 -`** are on `main` and visible on GitHub.

---

## Summary

- A **local repository** lives on your computer; a **remote repository** lives on a server like GitHub.
- Remotes provide backup, sharing, collaboration, and a public portfolio.
- **`origin`** is the conventional nickname for your project's main remote.
- **`git push`** uploads commits to the remote; **`git pull`** downloads and merges remote changes; **`git fetch`** downloads without merging.
- Remember: **`git pull` = `git fetch` + `git merge`**.
- Daily flow: **pull → edit → add → commit → push**.

---

*End of Lesson 4*

---
