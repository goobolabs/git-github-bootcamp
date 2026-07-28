# Lesson 1 – Introduction to Git & GitHub

> In Lesson 0 we learned *why* version control exists. Now we meet the two tools at the heart of this bootcamp: **Git** and **GitHub** — what they are, how they differ, and how to set them up.

---

## What You'll Learn

By the end of this lesson, students will be able to:

1. Explain what **Git** is and what it does.
2. Explain what **GitHub** is and how it relates to Git.
3. Clearly describe the **difference between Git and GitHub**.
4. **Install Git** on their computer.
5. **Configure Git** with their identity for the first time.

---

## What is Git?

**Git** is the version control tool we introduced in Lesson 0. It lives on **your computer** and tracks every change you make to your project.

When you use Git, you take "snapshots" of your project at different points in time. Each snapshot is saved with a message describing what changed. Later, you can browse those snapshots, compare them, or return to any one of them.

---

### Definition

**Git:**

> A free, open-source, distributed version control system that runs on your computer and records the complete history of changes to a project.

The key word is **distributed**: your machine has the full project and its entire history, so Git works even with no internet connection.

---

### What Git Does For You

- Tracks every change to your files over time.
- Lets you return to any previous version.
- Lets you work in separate "branches" without breaking the main project.
- Lets multiple people combine their work safely.

> Git is a **tool**, like a hammer. It does its job on your computer whether or not you ever go online.

---

## What is GitHub?

If Git lives on your computer, where do teammates and the world see your project? That's where **GitHub** comes in.

**GitHub** is a website that **hosts Git projects in the cloud**. You push your project from your computer up to GitHub, and from there others can view it, download it, and collaborate with you.

---

### Definition

**GitHub:**

> A cloud-based platform that hosts Git repositories online, adding collaboration features like pull requests, issues, code review, and project sharing.

GitHub is owned by Microsoft and is the most popular place to store and share code. It's where most open-source software in the world lives.

---

### What GitHub Adds On Top of Git

| **Feature**        | **What It Provides**                                        |
| ------------------ | ---------------------------------------------------------- |
| Remote hosting     | A safe online home for your project.                       |
| Collaboration      | Many people can contribute to the same project.            |
| Pull Requests      | A way to propose and review changes            |
| Issues             | A place to track bugs, tasks, and ideas        |
| Profile/portfolio  | A public showcase of your work to employers and peers.     |
| Automation         | Run tests and tasks automatically with Actions |

> Think of it like this: **Git** is the engine; **GitHub** is the garage, showroom, and parking lot where the cars are stored and shown off.

---

## Git vs GitHub

This is the single most common point of confusion for beginners, so let's make it crystal clear.

---

### The Core Difference

| **Git**                              | **GitHub**                               |
| ------------------------------------ | ---------------------------------------- |
| A **tool** (software)                | A **website / service**                  |
| Runs on **your computer**            | Runs in the **cloud**                    |
| Works **offline**                    | Needs the **internet**                   |
| Tracks versions of your project      | **Hosts** your Git project online        |
| Created in 2005 by Linus Torvalds    | Launched in 2008, now owned by Microsoft |
| Can be used **without** GitHub       | **Needs Git** to be useful               |

---

### A Simple Analogy

- **Git** is like a **camera** 📷 — it takes snapshots of your project over time.
- **GitHub** is like **Instagram** 🌐 — an online place to store those snapshots and share them with others.

You can take photos with a camera and never post them online. Likewise, you can use Git on your own without ever touching GitHub. But most teams *do* share, which is why we learn both together.

⚠️ **Common mistake:** Saying "I uploaded my code to Git." You upload code to **GitHub** (or a similar host). Git itself is the tool you used to track it.

---

### Are There Alternatives to GitHub?

Yes. GitHub is the most popular, but it's not the only host:

- **GitLab**
- **Bitbucket**

All of them host **Git** projects. In this bootcamp we focus on GitHub because it is the industry standard.

---

## Installing Git

Before we can use Git, we need to install it. The steps depend on your operating system.

---

### Step 1: Check If Git Is Already Installed

Open your terminal (Command Prompt, PowerShell, or a terminal app) and run:

```bash
git --version
```

If you see something like `git version 2.43.0`, Git is already installed and you can skip ahead to configuration. If you see an error like "command not found," follow the steps below.

---

### Step 2: Install Git

| **Operating System** | **How to Install**                                                       |
| -------------------- | ------------------------------------------------------------------------ |
| Windows              | Download the installer from [git-scm.com](https://git-scm.com) and run it. |
| macOS                | Run `brew install git` (with Homebrew), or download from git-scm.com.    |
| Linux (Debian/Ubuntu)| Run `sudo apt install git`.                                              |
| Linux (Fedora)       | Run `sudo dnf install git`.                                              |

After installing, **close and reopen your terminal**, then run `git --version` again to confirm it worked.

---

## Configuring Git

The first time you use Git, you must tell it **who you are**. Git attaches your name and email to every snapshot you create, so your changes can be identified later.

This is a **one-time setup** per computer.

---

### Setting Your Identity

Run these two commands, replacing the values with your own name and email:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

- `--global` means this applies to **all** your projects on this computer.
- Use the **same email** you use (or will use) for GitHub, so your work is linked to your account.

---

### Checking Your Configuration

To see everything Git has stored about you:

```bash
git config --list
```

You should see your `user.name` and `user.email` in the output.

> ⚠️ **Common mistake:** Forgetting to configure your name and email. If you skip this, Git may refuse to save your first snapshot, or it will be labeled with the wrong identity.

---

### Creating a GitHub Account

To use GitHub later in this bootcamp, you'll need a free account:

1. Go to [github.com](https://github.com).
2. Click **Sign up** and choose a username (this becomes part of your public profile, so pick something professional).
3. Verify your email address.

We'll connect Git to this account later when we start pushing code online.

---

## Summary

- **Git** is a free, distributed version control **tool** that runs on your computer.
- **GitHub** is a **website** that hosts Git projects online and adds collaboration features.
- Git ≠ GitHub: Git is the engine, GitHub is the online home — you can use Git without GitHub.
- Install Git from [git-scm.com](https://git-scm.com) and confirm with `git --version`.
- Configure Git once with `git config --global user.name` and `user.email` so your work is properly labeled.
- Create a free GitHub account now; we'll connect it later.

---

*End of Lesson 1*

---
