# Bonus 5 — Gists and Wiki

> **Gists** share small snippets without a full repo. A **Wiki** adds extra documentation pages to a repository — useful when the README is not enough.

**Prerequisites:** [Lesson 2](../lessons/02-git-basics.md), [Lesson 7](../lessons/07-gitignore-and-project-organization.md)

---

## Gists

### Public vs secret

| **Type** | **Who sees it** |
| -------- | --------------- |
| **Public** | Anyone with the URL |
| **Secret** | Only people you share the URL with — **not encrypted** |

Never put passwords, tokens, or keys in any gist.

### Create a gist

1. [gist.github.com](https://gist.github.com) → **New gist**
2. Description, filename (`notes.md`), paste content
3. **Create public gist** or **Create secret gist**
4. Copy and share the URL

Multiple files: click **Add file**. Gists keep revision history like repos.

---

## Wiki

A **Wiki** is a set of linked documentation pages on a repo — setup guides, FAQs, long docs that would clutter the README.

### Enable a wiki

1. Open your repo → **Settings** → **General**
2. Under **Features**, check **Wikis**
3. Save — a **Wiki** tab appears on the repo

### Create a page

1. Repo → **Wiki** tab → **Create the first page** (or **New Page**)
2. Title the page (e.g. `Installation`, `FAQ`)
3. Write in Markdown → **Save Page**
4. Add more pages and link between them with `[FAQ](FAQ)`

Anyone with **write access** to the repo can edit wiki pages in the browser. Each save creates a revision you can compare or revert.

### Wiki vs README vs Gist

| **Use…** | **When…** |
| -------- | --------- |
| **README** | First thing visitors see — install, quick start, project overview |
| **Wiki** | Longer docs: deployment, architecture, contributor guides, FAQs |
| **Gist** | Standalone snippet or note — not tied to one repo's docs tab |

Bootcamp assignments need **repos** with a good **README**. Wikis and gists are optional extras for bigger or shared projects.

---

## Quick comparison

| | **Gist** | **Wiki** | **Repo README** |
| --- | -------- | -------- | --------------- |
| Lives on | gist.github.com | Repo **Wiki** tab | Repo homepage |
| Best for | Cheat sheet, quick share | Multi-page project docs | Project intro |
| Git workflow | No | No (edit on GitHub) | Yes — commit like any file |

Showcase full projects on your profile — [Bonus 8](08-github-profile.md).

---

*End of Bonus 5 — Gists and Wiki*

---
