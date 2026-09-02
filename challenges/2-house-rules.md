# 📜 Challenge 2 — House Rules

> **15 points · ~15 minutes**

**Stop repeating yourself. Teach the agent your conventions once, and make it obey them.**

---

## The idea

In Challenge 1 you explained your context in the prompt. Tomorrow every teammate will explain
the same context again, badly, in their own words.

`.github/copilot-instructions.md` is read **automatically on every request**. Write it once,
everyone benefits, forever.

⚠️ **The lab repo already has one**, plus files under `.github/instructions/`. You're
**appending** to it — don't delete what's there.

> **The one thing that trips everyone up:** the agent **commits its work**, so plain
> `git diff` is always empty. Diff against the base instead: `git diff main...HEAD`.

Everything below happens in **one session**. You run the prompt, save the diff, throw the work
away, add your rules, and run the exact same prompt again. No merging to `main`, no second
session — the instructions file is read from your working copy on every request.

---

## Do it

Order matters — capture the "before" first, because once the rules exist you can't get an
un-ruled run any more.

### 1. Baseline (5 min)

Pick an issue you didn't use in Challenge 1, one that touches two or three files. Be as vague
as you dare:

```
Fix issue 6
```

The vagueness is the point — it's what lets the rules show up. When it's done, save the diff
and wipe the work:

```bash
git diff main...HEAD > /tmp/before.diff
wc -l /tmp/before.diff        # must not be 0

git reset --hard main         # throw away the agent's commits
git clean -fd                 # and any untracked files it left
```

You now have the evidence on disk and a clean tree to run again from.

### 2. Write the rules (5 min)

Append a `## Never` section to `.github/copilot-instructions.md`. This section earns its keep
fastest: it's what stops the agent handing you a 400-line diff where 380 lines are
reformatting.

```markdown
## Never

- Never reformat, reorder, or re-indent code in a file you weren't asked to change
- Never add a runtime dependency without asking first
- Never ship a bug fix without a regression test in the matching `*.test.ts`
```

Rules must be **checkable** — a reviewer should be able to point at a diff and say "that broke
rule 3" without arguing. `Write good code` is unfalsifiable; `Keep exported functions under 40
lines` names a number. Name a file, a folder, or an action.

**Don't commit it.** The agent reads the file from your working copy, and leaving it uncommitted
keeps it out of the next diff automatically.

### 3. Prove it (4 min)

Give the agent the **exact same prompt**: `Fix issue 6`

```bash
git diff main...HEAD > /tmp/after.diff
diff /tmp/before.diff /tmp/after.diff
```

Same command as step 1, so the two diffs are directly comparable.

**Done when one rule is visibly obeyed in `after.diff` and visibly not in `before.diff`** —
e.g. `before` reformats an unrelated file and `after` doesn't, or `before` has no test and
`after` adds one. That single contrast is the full 15 points.

> 💡 The agent still remembers run 1, which can flatter the result. If your tool has a
> `/clear` or "new conversation" command, use it before re-prompting — same session, same
> folder, fresh context.

### 4. Tighten it (1 min)

Rule still ignored? Rewrite **that one rule** to be more specific, reset, and rerun:

```bash
git reset --keep main         # drops the agent's commits, keeps your rules edit
git clean -fd
```

Note what v1 said, what v2 said, and why v2 worked — that's a bonus.

---

## ✅ Scoring

| | Points |
|---|---|
| A `## Never` section written + before/after diffs showing a rule being obeyed | **15** |
| Rules written, no evidence it changed behaviour | 7 |
| 🌟 The two diffs shown side by side | +5 |
| 🌟 A rule you rewrote because v1 was ignored, and why v2 worked | +5 |
| 🌟 A rule specific to your real team, not this lab app | +5 |

**Demo tip:** same vague prompt, two diffs, side by side. Best three-minute demo on the board.

---

## 🆘 Stuck?

| Symptom | Cause |
|---|---|
| `before.diff` is 0 bytes | Ran plain `git diff` — the agent commits, so use `main...HEAD` |
| `after.diff` contains your rules file | The agent committed it too — ignore that hunk |
| Both diffs identical | Agent never read the file — check the path is exactly `.github/copilot-instructions.md` |
| New test file missing | `git diff` never shows untracked files — diff against `main` |
| Rules present but ignored | Too vague — go to step 4 |
| Second run suspiciously good | It's remembering run 1 — clear the conversation and retry |

---

**Next →** [Plan First](3-plan-first.md) · [Not A Diff](6-not-a-diff.md) · [the board](../README.md#the-board)

*Adapted from [Lesson 3](https://github-samples.github.io/copilot-workshops/app/3-custom-instructions/).*
