# 🎨 Challenge 6 — Not A Diff

> **15 points · ~10 minutes**

**Ship something useful that isn't a code change.**

---

## The idea

Everything so far ended in a pull request. But plenty of the work that actually unblocks a
team isn't code — it's the migration plan, the inventory, the comparison table, the thing
that lets someone make a decision on Monday.

**Canvases** are interactive side panels — documents, spreadsheets, previews — that the agent
creates and edits alongside the conversation. Not all output is a diff.

---

## Do it

### 1. Pick something your team would actually want (2 min)

Not a toy. Ideas that land well:

| Build | Prompt shape |
|---|---|
| 📋 **Onboarding doc** | *"Read this repo and write the doc a new joiner needs on day one — architecture, how to run it, where the traps are."* |
| 🔍 **Dependency audit** | *"List every dependency, what it's used for, and which look stale or risky."* |
| 🗺️ **Migration plan** | *"We want to replace X with Y. Give me a phased plan with the risky steps flagged."* |
| 📊 **Backlog triage** | *"Read all open issues. Group them by area, estimate effort, flag anything that's actually a duplicate."* |
| 🧪 **Test coverage map** | *"Which parts of this codebase have no tests, and which of those matter most?"* |

### 2. Build it in a canvas (5 min)

Ask the agent to produce it as a canvas rather than pasting into chat. Then **iterate on it
live** — that's the part worth demoing:

> Add a column for how risky each step is.

> Cut the ones that don't need doing this quarter.

> Turn the last section into a checklist I can paste into an issue.

### 3. Make it land somewhere (3 min)

A canvas nobody sees is a canvas that didn't happen. Commit it to the repo, paste it into an
issue, or drop it in your team channel.

---

## ✅ Scoring

| | Points |
|---|---|
| A canvas artefact that's genuinely useful, and it's landed somewhere | **15** |
| Canvas created, not shared or committed | 8 |

### 🌟 Bonus

| | Points |
|---|---|
| It's about **your real codebase**, not the lab app | **+10** |
| You iterated it live in the demo — show it changing | **+5** |
| Someone from another team says they want it | **+5** |

---

## 🎬 Demo tip

**Don't read your document out.** Show it, then change it live in front of the room. The
editing is the demo; the document is just the excuse.

---

## Why this one matters more than its points suggest

Fifteen points is the lowest score on the board, and this is often the challenge people
remember.

Most of the resistance to agents in a team isn't from engineers who don't want help writing
code. It's from people who look at it and think *"that's not my job."* Tech leads, architects,
staff engineers — people whose output is decisions, not diffs.

This is the challenge that speaks to them.

---

**Next →** [the board](../README.md#the-board)

*Adapted from [Lesson 7](https://github-samples.github.io/copilot-workshops/app/7-canvases/).*
