# Lesson 9 – GitHub Actions Introduction

> You've mastered collaborating with people. Now let's make the **computer** do some of the work for you. This lesson introduces **automation** on GitHub — running tasks like testing automatically, every time you push.

---

## What You'll Learn

By the end of this lesson, students will be able to:

1. Understand the basic concepts of **CI/CD**.
2. Explain what **GitHub Actions** is.
3. Read and understand a simple **workflow file**.
4. Create an **automation** that runs when you push code.
5. Name common **events** and actions like **`checkout`** you'll see on real projects.
6. Use a **repository variable** (`vars`) in a workflow.
7. Find **failed workflow logs** and understand **status checks** on Pull Requests.

---

## Why Automate? The Idea of CI/CD

Imagine that every time someone pushes code, a human has to manually run all the tests, check the formatting, and build the project. That's slow, boring, and easy to forget. **Automation** lets the computer do these repetitive checks instantly and reliably.

The professional name for this idea is **CI/CD**.

---

### Definition

**CI/CD (Continuous Integration / Continuous Delivery):**

> A practice where code changes are **automatically** tested and prepared for release every time they are pushed, catching problems early and speeding up delivery.

Let's break the two halves apart in plain language:

| **Term**                     | **What It Means in Simple Words**                              |
| ---------------------------- | -------------------------------------------------------------- |
| **CI** (Continuous Integration) | Automatically **test and check** new code as it's added.    |
| **CD** (Continuous Delivery)    | Automatically **prepare and release** that code to users.   |

---

### Why CI/CD Helps

- **Catches bugs early** — tests run on every push, not just before release.
- **Saves time** — no more running checks by hand.
- **Builds confidence** — if the checks pass, the team trusts the change.
- **Keeps `main` healthy** — broken code is caught before it's merged.

> Think of CI as a **robot reviewer** 🤖 that tirelessly checks every change, day and night, and never forgets a step.

---

## What is GitHub Actions?

**GitHub Actions** is GitHub's built-in tool for automation. It lets you run tasks automatically in response to events in your repository — like a push, a pull request, or a schedule.

---

### Definition

**GitHub Actions:**

> A built-in GitHub feature that automatically runs tasks (called **workflows**) in response to repository events, such as pushing code or opening a pull request.

The best part: it's **built into GitHub**, so there's nothing extra to install. You just add a special file to your repository.

---

### Key Vocabulary

GitHub Actions has a few terms that fit together like building blocks:

| **Term**    | **What It Is**                                                    |
| ----------- | ----------------------------------------------------------------- |
| **Workflow**| The whole automated process (defined in one file).                |
| **Event**   | The trigger that starts a workflow (e.g., a `push`).              |
| **Job**     | A group of steps that run together.                               |
| **Step**    | A single task within a job (e.g., "run the tests").               |
| **Runner**  | The virtual computer GitHub uses to execute the job.              |

```
Event (push)  ──►  Workflow  ──►  Job  ──►  Step, Step, Step...
```

---

## Workflow Files

A workflow is described in a **YAML file** stored in a special folder in your repository: **`.github/workflows/`**.

---

### Definition

**Workflow File:**

> A YAML file inside `.github/workflows/` that tells GitHub Actions **when** to run and **what** steps to perform.

YAML is a simple, human-readable format. The most important thing to know is that **indentation (spaces) matters** — it defines the structure.

---

### Where the File Lives

```
my-project/
├── .github/
│   └── workflows/
│       └── hello.yml        ← your workflow file
├── README.md
└── index.html
```

---

## A Simple Example

### Step 1 — Add a repository variable for your name

On GitHub, open your repo → **Settings** → **Secrets and variables** → **Actions** → **Variables** tab → **New repository variable**.

| **Name** | **Value** (example) |
| -------- | ------------------- |
| `STUDENT_NAME` | `Sharafdin` |

Use your own name as the value. This stores the name **in the repo settings on GitHub** — not hard-coded in the workflow file — so you can change it anytime without editing the YAML.

### Step 2 — Create the workflow file

Create `.github/workflows/hello.yml` in the same repo:

```yaml
name: My First Workflow

on: push

jobs:
  say-hello:
    runs-on: ubuntu-latest
    steps:
      - name: Get the code
        uses: actions/checkout@v4

      - name: Greet and count files
        env:
          STUDENT_NAME: ${{ vars.STUDENT_NAME }}
        run: |
          COUNT=$(find . -type f -not -path './.git/*' | wc -l)
          echo "Hello $STUDENT_NAME, your files count are $COUNT"
```

- **`${{ vars.STUDENT_NAME }}`** reads the repository variable you set on GitHub.
- **`env:`** passes it into the shell as `$STUDENT_NAME` for the `echo` command.

The workflow uses **`uses`** to download your repo, then **`run`** to count files and print a message with your name.

### Step 3 — Commit and push

From your project root:

```bash
mkdir -p .github/workflows
# Create hello.yml with the YAML above, then:
git add .github/workflows/hello.yml
git commit -m "Add first GitHub Actions workflow"
git push
```

> 💡 If the variable is missing, the greeting prints `Hello , your files count are …` with a blank name — double-check **Settings → Variables** and that the name is exactly `STUDENT_NAME`.

---

### More Events You Can Trigger

Our example uses `on: push` — run every time code is pushed. That is the most common trigger when you're learning, but workflows can start from **many events**:

| **Event** | **Runs when…** | **Typical use** |
| --------- | -------------- | --------------- |
| `push` | Code is pushed to a branch | Run checks after every commit |
| `pull_request` | A PR is opened or updated | Show ✅/❌ on the PR before merge ([Lesson 6](06-pull-requests-and-code-reviews.md)) |
| `schedule` | On a timer (cron syntax) | Nightly builds, weekly reports |
| `workflow_dispatch` | You click **Run workflow** in the Actions tab | Manual runs on demand |
| `release` | A GitHub Release is published | Deploy or publish notes when you ship a version |

**Example — run on push and Pull Request:**

```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
```

**Example — run every Monday at 9:00 UTC:**

```yaml
on:
  schedule:
    - cron: '0 9 * * 1'
```

This is a **GitHub Actions cron schedule**. It tells GitHub **when to automatically run the workflow**.

The cron expression has **5 fields**:

```text
┌──────── Minute (0-59)
│ ┌────── Hour (0-23)
│ │ ┌──── Day of month (1-31)
│ │ │ ┌── Month (1-12)
│ │ │ │ ┌─ Day of week (0-7)
│ │ │ │ │
0 9 * * 1
```

For this example:

- `0` → At minute **0**
- `9` → At **09:00**
- `*` → Every day of the month
- `*` → Every month
- `1` → **Monday**

So this means:

> **Run the workflow every Monday at 09:00 UTC.**

#### Common cron examples

| **Cron** | **Meaning** |
| -------- | ----------- |
| `0 0 * * *` | Every day at 00:00 UTC |
| `0 9 * * 1` | Every Monday at 09:00 UTC |
| `0 */6 * * *` | Every 6 hours |
| `*/15 * * * *` | Every 15 minutes |
| `0 12 1 * *` | 12:00 UTC on the 1st of every month |

#### Important note

GitHub Actions uses **UTC**, not your local timezone.

For example, if you're in Somalia (UTC+3):

```yaml
cron: '0 9 * * 1'
```

runs at:

- **09:00 UTC**
- **12:00 PM (noon) Somalia time** every Monday.

You only need `push` for your first workflow. As your projects grow, you'll combine events — for example `pull_request` to guard `main` and `schedule` for periodic checks.

---

### `run` vs `uses`

The hello workflow above uses both keywords:

| **Keyword** | **What it does** |
| ----------- | ---------------- |
| `run` | Runs a **command** in the shell (`echo`, `find`, `npm test`) |
| `uses` | Runs a **shared action** from GitHub's marketplace or your org |

**Step 1 — `uses: actions/checkout@v4`**

The runner starts as a **fresh, empty machine**. It does not have your repo files until you download them. `actions/checkout@v4` copies your repository onto the runner.

**Step 2 — `run:` with a shell script**

After checkout, your files are on the runner — so `find` can count them and `echo` can print your greeting.

Think of **`run`** as "do it yourself in the terminal" and **`uses`** as "borrow a tool the community already built." **Checkout is almost always the first step** when a workflow needs your project files.

**Other actions you'll see on real projects** (awareness only — no need to use them yet):

| **Action** | **Purpose** |
| ---------- | ----------- |
| `actions/checkout@v4` | Download the repository onto the runner |
| `actions/setup-node@v4` | Install a specific Node.js version (JavaScript projects) |
| `actions/setup-python@v5` | Install a specific Python version |
| `actions/upload-artifact@v4` | Save build output (logs, zip files) from a workflow run |

---

### Watching It Run

1. Go to your repository on GitHub.
2. Click the **Actions** tab.
3. You'll see your workflow running (a yellow dot 🟡), then succeeding (a green check ✅) or failing (a red X ❌).
4. Click into the run to expand each step and read the logs — on success you'll see something like `Hello Sharafdin, your files count are 5` in the **Greet and count files** step (using whatever name you set in `STUDENT_NAME`).

🎉 You've just automated a task that runs in the cloud on every push.

---

### When a Workflow Fails

Broken YAML or a failing command shows a red ❌ on the Actions tab. To find the problem:

1. Open the **failed run** (red X).
2. Click the **failed step** (also marked with ❌).
3. Read the log — the error is usually near the bottom (wrong indentation, typo in a command, missing file, etc.).
4. Fix the workflow file locally, commit, push — GitHub runs it again automatically.

You can also click **Re-run jobs** on a failed run if you fixed something outside the repo (rare when learning) or want to retry without a new commit.

---

### Status Checks on Pull Requests

When a workflow uses `on: pull_request`, its result appears **on the PR page** as a **status check** — the same ✅ or ❌ you see on professional repos:

```
Pull Request #2 — Add contact section
  ✅ My First Workflow — All checks have passed
```

Reviewers (and you) see whether automation passed **before** merging into `main` — the same idea as [Lesson 6](06-pull-requests-and-code-reviews.md) reviews, but run by a robot. If a check fails, the PR can still stay open; fix the branch, push again, and the check re-runs.

---

### Common Beginner Mistakes

⚠️ Watch out for these when writing your first workflows:

- **Wrong folder.** The file **must** be inside `.github/workflows/`. A typo here means nothing runs.
- **Broken indentation.** YAML relies on spaces, not tabs. Misaligned lines cause errors.
- **Wrong file extension.** Use `.yml` or `.yaml`.
- **Expecting it offline.** Actions run on GitHub's servers, so the workflow only runs **after you push**.
- **Skipping checkout when you need your files.** The runner starts empty — without `actions/checkout@v4`, commands like `find` or `ls` won't see your repo.
- **Variable name typo.** The workflow expects `STUDENT_NAME` — it must match exactly in Settings → Variables.

---

## Summary

- **CI/CD** is the practice of automatically testing and delivering code on every change, catching problems early.
- **GitHub Actions** is GitHub's built-in automation tool that runs **workflows** in response to events like a push.
- Key terms: a **workflow** contains **jobs**, jobs contain **steps**, and they run on a **runner**.
- Workflows are **YAML files** stored in `.github/workflows/`, where indentation matters.
- **`on:`** sets the trigger — `push` is enough to start; later you'll use `pull_request`, `schedule`, and others.
- **`run`** executes a shell command; **`uses`** runs a shared action (e.g. `actions/checkout@v4` to download your repo).
- **`${{ vars.NAME }}`** reads a **repository variable** set under Settings → Secrets and variables → Actions.
- On failure, open the failed **step** in the Actions tab and read the log near the bottom.
- Workflows on **`pull_request`** show as **status checks** on the PR before merge.
- Create the file, push it, and watch it run under the repository's **Actions** tab.

---

*End of Lesson 9*

---
