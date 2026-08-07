# Bonus 7 — Tags and Releases

> Mark milestones with a **tag** (`v1.0.0`) and publish a **GitHub Release** with notes and a download.

**Prerequisites:** [Lesson 4](../lessons/04-remote-repositories.md), [Lesson 10](../lessons/10-putting-it-all-together.md)

---

## How versions work

| **Concept** | **Moves?** | **Use** |
| ----------- | ---------- | ------- |
| **Commit** | Fixed | Daily work |
| **Branch** | Yes | Active development |
| **Tag** | Fixed | Name one commit as a version |
| **Release** | Fixed | GitHub page for that tag |

Flow: merge on `main` → **tag** the ready commit → **release** on GitHub. Tags stay put; `main` keeps moving.

---

## Semantic versioning

`vMAJOR.MINOR.PATCH`:

| **Bump** | **When** | **Example** |
| -------- | -------- | ----------- |
| **PATCH** | Bug fix | `v1.0.0` → `v1.0.1` |
| **MINOR** | New feature, compatible | `v1.0.0` → `v1.1.0` |
| **MAJOR** | Breaking change | `v1.0.0` → `v2.0.0` |

Capstone milestone: **`v1.0.0`** is enough.

---

## Tag and push

```bash
git switch main
git pull
git tag -a v1.0.0 -m "First public version"
git push origin v1.0.0
```

Prefer **annotated** tags (`-a -m`) over lightweight (`git tag v1.0.0`) — they store author and date.

Verify: GitHub → **Code** → tags dropdown.

---

## GitHub Release

1. **Releases** → **Create a new release**
2. Tag: `v1.0.0`
3. Title and description (what changed)
4. **Publish release**

Use release notes or `CHANGELOG.md` to list changes per version.

---

## Common mistakes

| **Mistake** | **Fix** |
| ----------- | ------- |
| Tag on wrong commit | Check `git log`; `git tag -d v1.0.0` and re-tag |
| Tag not on GitHub | `git push origin v1.0.0` |

---

*End of Bonus 7 — Tags and Releases*

---
