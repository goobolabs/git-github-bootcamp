# Assignment: GitHub Actions

**Due:** Tuesday, August 4, 2026 — 12:00 PM (Africa/Mogadishu / EAT)

**Goal:** Add a simple GitHub Actions workflow to your **`git-github-practice`** repository and show that it runs successfully when you push.

---

## Prerequisites

Complete these before you submit:

| **Lesson / work** | **What you need from it** |
| ----------------- | ------------------------- |
| [Assignment 1](assignment-1.md) | Your `git-github-practice` repo on GitHub |
| [Lesson 9](../lessons/09-github-actions-introduction.md) | Workflow file, repository variable, and Actions tab |

This assignment builds on the **same repo** from Assignment 1. You are not creating a new project.

---

## What you are submitting

Add GitHub Actions to **`git-github-practice`**. Before you submit, confirm:

- [ ] Repository variable **`STUDENT_NAME`** is set (Settings → Secrets and variables → Actions → Variables)
- [ ] Workflow file **`.github/workflows/hello.yml`** exists and matches [Lesson 9](../lessons/09-github-actions-introduction.md)
- [ ] You pushed the workflow to GitHub
- [ ] At least **one successful run** (green ✅) appears in the **Actions** tab
- [ ] The log shows your name in the greeting (for example, `Hello Sharafdin, your files count are …`)
- [ ] You have the **workflow run URL** to paste in your submission (see below)

**Workflow run URL:** Open **Actions** → click your successful run → copy the link from your browser. It looks like:

`https://github.com/your-username/git-github-practice/actions/runs/12345678901`

---

## What to add (quick checklist)

Follow [Lesson 9](../lessons/09-github-actions-introduction.md):

1. On GitHub, add variable **`STUDENT_NAME`** with your name as the value.
2. Create `.github/workflows/hello.yml` locally with the lesson example.
3. Commit and push:

   ```bash
   git add .github/workflows/hello.yml
   git commit -m "Add GitHub Actions hello workflow"
   git push
   ```

4. Open the **Actions** tab, confirm the workflow passed, and copy the **run URL** from your browser (click the run → copy the address bar).

That is all — no extra jobs, events, or secrets required for this assignment.

---

## How to submit

Follow the [submissions guide](../submissions/README.md):

1. **Fork** this bootcamp repository (if you have not already).
2. Create `submissions/<your-github-username>/assignment-2/`.
3. Add `submission.md` with your repo URL and confirmation (see template below).
4. **Commit and push** to your fork.
5. Open a **Pull Request** to this repository.
   - PR title: `Assignment 2 Submission - <Your GitHub Username>` (for example, `Assignment 2 Submission - sharafdin`)

### `submission.md` template

Create `submissions/your-username/assignment-2/submission.md`:

```md
# Assignment 2 — GitHub Actions

- **Name:** Your Full Name
- **GitHub username:** your-username
- **Repository URL:** https://github.com/your-username/git-github-practice
- **Actions run URL:** https://github.com/your-username/git-github-practice/actions/runs/12345678901

## Confirmation

- [ ] `STUDENT_NAME` variable is set on GitHub
- [ ] `.github/workflows/hello.yml` is in the repository
- [ ] At least one workflow run shows a green check in Actions
- [ ] Workflow log shows my name in the greeting
- [ ] Actions run URL above opens a successful run on my repo
```

Replace the placeholders with your real details before opening your PR.

---

## Evaluation criteria

| **Criterion** | **What we check** |
| ------------- | ----------------- |
| Repository | Same **`git-github-practice`** repo from Assignment 1 |
| Variable | **`STUDENT_NAME`** exists under Actions → Variables |
| Workflow file | **`.github/workflows/hello.yml`** present with `on: push`, `checkout`, and greet step |
| Successful run | At least **one green** workflow run on GitHub |
| Actions run URL | Valid link to a **successful** run (for example `…/actions/runs/30714957271`) |
| Greeting | Log output includes your name from the variable |
| Submission | PR includes `submissions/<username>/assignment-2/submission.md` with repo URL and run URL |

---

## Common mistakes

| **Mistake** | **Fix** |
| ----------- | ------- |
| Workflow file in wrong folder | Must be **`.github/workflows/hello.yml`** |
| Variable name typo | Use exactly **`STUDENT_NAME`** in Settings and in the YAML |
| Blank name in log | Set the variable on GitHub before expecting the greeting |
| No green check yet | Push the workflow file — Actions only run **after** push |
| Wrong or missing run URL | Open **Actions** → click the green run → copy the URL from the address bar |
| Link to repo instead of run | Use the **run** URL (`…/actions/runs/…`), not only the repo homepage |
| Wrong repo in submission | Use **`git-github-practice`**, not the bootcamp fork |
| Submission folder name wrong | Folder must exactly match your GitHub username (case-sensitive) |
| Changing others' submissions | Only edit **your** folder under `submissions/<your-username>/` |

---

*Assignment 2 — Git & GitHub Bootcamp*
