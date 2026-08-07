# Bonus 6 — Open Source Licenses

> Public code is **copyrighted by default**. A **LICENSE** file tells others what they may do with it.

**Prerequisites:** [Lesson 8](../lessons/08-open-source-workflows.md), [Bonus 3](03-open-source-contributing.md)

---

## No license ≠ open to reuse

| **Situation** | **Simple explanation** |
| ------------- | ---------------------- |
| Public repo, no LICENSE | *"You can look, but you don't have clear permission to copy or use it."* |
| LICENSE file present | *"The rules are written — read the file before you reuse."* |

Always check before copying code into your project.

---

## Common software licenses

| **License** | **Type** | **Typical use** |
| ----------- | -------- | --------------- |
| **MIT** | Permissive | Libraries, personal projects |
| **Apache 2.0** | Permissive | Corporate OSS (+ patent grant) |
| **GPL v3** | Copyleft | Must share derivatives under GPL |

### Simple explanations

**MIT** — *"Use my code for almost anything — just keep my name on it."*
Anyone can copy, change, and sell your code. They must include your copyright notice and the license text. Most popular for small open-source projects.

**Apache 2.0** — *"Like MIT, plus extra legal protection on patents."*
Same freedom as MIT for everyday use. Adds explicit patent rights so contributors cannot later sue users over patents in the code. Common in companies and big OSS projects (e.g. Apache, Google).

**GPL v3** — *"If you share a modified version, you must share the source under the same license."*
Others can use and change your code, but if they **distribute** a modified app or library, they must open-source their changes too. Keeps software free; stricter for closed-source products that embed GPL code.

**Permissive vs copyleft (one line):**
- **Permissive** (MIT, Apache) → "Take it, use it, even in paid closed apps — just credit me."
- **Copyleft** (GPL) → "Take it, but if you ship changes, ship the source too."

New developers often pick **MIT** for portfolio repos. Guide: [choosealicense.com](https://choosealicense.com/).

---

## Creative Commons — for content, not code

For **writing, courses, images** — not application source code.

| **License** | **Simple explanation** |
| ----------- | ---------------------- |
| **CC BY** | Share and remix — just **credit** the author. |
| **CC BY-SA** | Same as BY, but derivatives must use the **same license**. |
| **CC BY-NC-SA** | Credit required, **non-commercial** only, share-alike. *(This bootcamp.)* |

This bootcamp uses **[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)** — you may share and adapt for **non-commercial** use with credit; your versions must use the same license. See [LICENSE](../LICENSE).

| **Use for…** | **Pick…** |
| ------------ | --------- |
| Docs, tutorials, courses | Creative Commons |
| Apps, libraries, scripts | MIT or Apache 2.0 |

---

## Add a LICENSE on GitHub

**New repo:** choose **Add a license** when creating (e.g. MIT).

**Existing repo:** Add file → name `LICENSE` → **Choose a license template** → commit.

Pick a license **before** your first release ([Bonus 7](07-tags-and-releases.md)).

---

*End of Bonus 6 — Open Source Licenses*

---
