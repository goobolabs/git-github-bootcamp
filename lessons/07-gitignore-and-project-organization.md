# Lesson 7 – .gitignore and Project Organization

> You can now create, branch, share, and review projects. This lesson is about keeping them **clean and safe**: which files to *exclude* from Git, how to document your project, and how to protect secrets.

---

## What You'll Learn

By the end of this lesson, students will be able to:

1. Use a **`.gitignore`** file to keep unwanted files out of Git.
2. Use **`git rm`** and **`git mv`** to remove or rename files in your repository.
3. Write a useful **README** file.
4. Organize a repository with a **clear structure**.
5. **Protect secrets** so passwords and keys never end up online.

---

## Ignoring Files with .gitignore

Not everything in your project folder belongs in Git. Some files are temporary, auto-generated, huge, or **secret**. Committing them clutters your history or, worse, leaks sensitive data.

A **`.gitignore`** file tells Git which files and folders to **ignore** — to pretend they aren't there.

---

### Definition

**.gitignore:**

> A special text file that lists the files and folders Git should ignore, so they are never tracked, staged, or committed.

The file is named exactly `.gitignore` (with the leading dot) and usually lives in the **root** of your repository.

---

### Why Ignore Files?

| **Type of File**          | **Example**              | **Why Ignore It**                          |
| ------------------------- | ------------------------ | ------------------------------------------ |
| Secrets                   | `.env`, `config.key`     | Must never be public.                      |
| Dependencies              | `node_modules/`          | Huge and re-downloadable; no need to store.|
| Build/output files        | `dist/`, `build/`        | Auto-generated from your source code.      |
| System/editor junk        | `.DS_Store`, `.vscode/`  | Specific to your machine, not the project. |
| Logs and temp files       | `*.log`, `tmp/`          | Noise that changes constantly.             |

> The rule of thumb: **commit your source code, ignore everything that can be regenerated, downloaded, or must stay secret.**

---

### What a .gitignore Looks Like

Create a file named `.gitignore` in your project root and list patterns inside it:

```gitignore
# Dependencies
node_modules/

# Environment / secret files
.env

# Build output
dist/
build/

# Logs
*.log

# Operating system files
.DS_Store

# Editor settings
.vscode/
```

| **Pattern**       | **What It Ignores**                                   |
| ----------------- | ----------------------------------------------------- |
| `node_modules/`   | A folder and everything inside it.                    |
| `.env`            | One specific file.                                    |
| `*.log`           | Every file ending in `.log` (the `*` means "any").    |
| `# comment`       | A note for humans; Git ignores lines starting with `#`.|

---

### A Crucial Warning About Timing

⚠️ **Common mistake:** `.gitignore` only ignores files that are **not already tracked**. If you commit `secret.env` first and add it to `.gitignore` *afterwards*, Git keeps tracking it.

The lesson: **create your `.gitignore` early**, ideally right after `git init`, before committing anything you'd regret. (Sites like [gitignore.io](https://gitignore.io) can generate one for your language.)

If you already committed a file by mistake, stop tracking it with:

```bash
git rm --cached secret.env
```

Then add `secret.env` to `.gitignore` and commit. The file stays on your computer — Git just stops tracking it.

---

## Managing Files in Git

Git has commands to **delete files** and **rename files** properly. To undo uncommitted edits or unstage a file, use **`git restore`** (Lesson 3).

---

### `git rm` — Remove a File from the Repository

When you delete a file from your project, tell Git explicitly:

```bash
# Delete the file AND stage the deletion for the next commit
git rm old-notes.txt
git commit -m "Remove old notes file"
```

To **stop tracking** a file but keep it on your disk (common with `.env`):

```bash
git rm --cached .env
```

---

### `git mv` — Rename or Move a File

Renaming with `git mv` keeps Git's history connected to the file:

```bash
git mv notes.txt journal.txt
git commit -m "Rename notes to journal"
```

This is cleaner than manually renaming and running `git add` on both paths.

---

## README Files

When someone visits your repository, the first thing they see is the **README**. It's the front door of your project.

---

### Definition

**README:**

> A documentation file (usually `README.md`) that explains what a project is, how to use it, and anything a newcomer needs to know.

It's written in **Markdown** (the same format as these lessons), and GitHub automatically displays it on the repository's main page.

---

### What a Good README Contains

A helpful README usually answers these questions:

| **Section**       | **Answers the Question...**           |
| ----------------- | ------------------------------------- |
| Title & summary   | What is this project?                 |
| Features          | What can it do?                       |
| Installation      | How do I set it up?                   |
| Usage             | How do I run or use it?               |
| Contributing      | How can others help? (optional)       |
| License           | How may it be used? (optional)        |

---

### Example README

```markdown
# Weather App

A simple web app that shows the current weather for any city.

## Features

- Search weather by city name
- Displays temperature and conditions
- Clean, mobile-friendly design

## Installation

```bash
git clone https://github.com/your-username/weather-app.git
cd weather-app
```

## Usage

Open `index.html` in your browser and type a city name.
``

> 💡 A clear README is what separates a project that looks professional from one that looks abandoned. It's often the **first thing** an employer reads on your GitHub.

---

## Repository Structure

A tidy repository is easy to understand and navigate. As projects grow, **organization** keeps them from becoming a mess.

---

### A Clean Example Structure

```
my-project/
├── .gitignore          ← files Git should ignore
├── README.md           ← project documentation
├── src/                ← your source code
│   ├── index.html
│   ├── style.css
│   └── app.js
├── assets/             ← images, fonts, icons
│   └── logo.png
└── docs/               ← extra documentation (optional)
```

---

### Principles of Good Organization

- **Group related files** into folders (`src/`, `assets/`, `docs/`).
- **Keep the root clean** — only essential files like `README.md` and `.gitignore` at the top.
- **Use clear, lowercase names** without spaces (`user-profile.js`, not `User Profile.js`).
- **Be consistent** — pick a convention and stick to it across the project.

> A newcomer should be able to open your repo and **guess where things are** without asking.

---

## Protecting Secrets

This is the most important safety topic in the whole bootcamp. **Secrets** are sensitive values like passwords, API keys, and access tokens. If they end up on a public GitHub repo, anyone in the world can find and abuse them.

---

### Definition

**Secret:**

> Any sensitive piece of information — such as a password, API key, or token — that must never be exposed publicly or committed to a repository.

---

### How Secrets Leak (and How to Prevent It)

The usual mistake is hard-coding a secret directly into your code:

```js
// ❌ NEVER do this
const apiKey = "sk_live_1234567890_SECRET";
```

The safe approach is to keep secrets in a separate `.env` file that is **ignored by Git**:

```
# .env  (this file is in .gitignore — never committed)
API_KEY=sk_live_1234567890_SECRET
```

```js
// ✅ Read the secret from the environment instead
const apiKey = process.env.API_KEY;
```

Then make absolutely sure `.env` is listed in `.gitignore`:

```gitignore
.env
```

---

### The Secret-Safety Checklist

| ✅ **Do**                                        | ❌ **Don't**                                  |
| ------------------------------------------------ | --------------------------------------------- |
| Keep secrets in `.env` files                     | Hard-code passwords or keys in your code      |
| Add `.env` to `.gitignore` *before* committing   | Commit `.env` "just this once"                |
| Share an `.env.example` (with blank values)      | Push real credentials to a public repo        |
| Rotate (replace) a key if it ever leaks          | Assume "private repo" means it's safe forever |

> ⚠️ **Critical:** Once a secret is pushed to GitHub, **consider it compromised** — even if you delete it later, it may already be copied or cached. The only real fix is to **revoke the key and create a new one.** Prevention beats cleanup.

---

## Summary

- **`.gitignore`** lists files Git should ignore — secrets, dependencies, build output, and system junk.
- Create your `.gitignore` **early**, because it won't ignore files Git already tracks. Use **`git rm --cached`** if you committed a file by mistake.
- **`git rm`** deletes files from the repo; **`git mv`** renames or moves them.
- A **README** is your project's front door: it explains what the project is and how to use it.
- Organize repositories with clear folders (`src/`, `assets/`) and a clean root.
- **Never commit secrets.** Keep them in `.env` files that are ignored by Git.
- A leaked secret should be treated as compromised — revoke it and issue a new one.

---

*End of Lesson 7*

---
