# 📜 Challenge 2 — House Rules

> **15 points · ~15 minutes**

**Stop repeating yourself. Teach the agent your conventions once, and make it obey them.**

---

## The idea

You just spent Challenge 1 explaining context in your prompt. Every teammate will explain the
same context tomorrow, badly, in their own words.

`.github/copilot-instructions.md` is read **automatically on every request** in that
repository. Write it once, everyone benefits, forever.

> ⚠️ **The lab repo already has one.** The template ships `.github/copilot-instructions.md`
> plus several files under `.github/instructions/`. You are **not** starting from a blank
> page — you're **adding rules to an existing file** and proving they changed the agent's
> behaviour. Do not delete or rewrite what's already there.

---

## Do it

The order below matters. You capture the "before" **first**, because once the rules are in
the file you can't get an un-ruled run any more.

### 1. Capture a baseline (5 min)

1. Pick an issue you did **not** use in Challenge 1 — check the Issues tab.
2. Start a **new session** and give it a prompt as vague as you dare. Literally just:

   ```
   Fix issue 6
   ```

   (Substitute your issue number. The vagueness is the point — it's what lets the rules show up.)

3. When it finishes, save the diff and throw the work away:

   ```bash
   git diff > /tmp/before.diff
   git checkout .
   git clean -fd
   ```

Keep `/tmp/before.diff` open in a tab. That's your evidence.

> 💡 **Don't skip the reset.** If leftover changes are still on disk, run 2 will build on top
> of them and the comparison is worthless.

### 2. Write the rules (4 min)

Open `.github/copilot-instructions.md` and **append** a `## Never` section at the end.

> 💡 **The "Never" section earns its keep fastest.** It's what stops the agent handing you a
> 400-line diff where 380 lines are reformatting. That's the class of change nobody reviews
> properly.

Rules must be **specific and checkable**. A reviewer should be able to point at the diff and
say "that broke rule 3" without arguing about it.

```markdown
## Never

- Never reformat, reorder, or re-indent code in a file you weren't asked to change
- Never add a runtime dependency without asking first
- Never ship a bug fix without a regression test in the matching `*.test.ts`
- Never commit or push directly to `main`
```

| ❌ Ignored | ✅ Obeyed |
|---|---|
| `Write good code` | `Keep exported functions under 40 lines` |
| `Add tests` | `Every bug fix ships with a regression test in the matching *.test.ts` |
| `Don't make a mess` | `Never reformat a file you weren't asked to change` |

The left column is unfalsifiable, so the model has nothing to comply with. The right column
names a file, a number, or an action.

### 3. Prove it (5 min)

1. **Start a fresh session.** Instructions are loaded per request — a session already running
   may not pick up your edit.
2. Give it the **exact same prompt** as step 1: `Fix issue 6`
3. Compare:

   ```bash
   git diff > /tmp/after.diff
   diff /tmp/before.diff /tmp/after.diff
   ```

**You're done when at least one rule is visibly obeyed in `after.diff` and visibly not obeyed
in `before.diff`.** For example:

- `before.diff` reformats a file the issue never mentioned; `after.diff` leaves it alone
- `before.diff` has no test; `after.diff` adds one in the matching `*.test.ts`
- `before.diff` adds a dependency; `after.diff` asks first

That single contrast is worth the full 15 points. Commit the instructions file.

### 4. Tighten it (1 min)

Rule still ignored in run 2? Rewrite **that one rule** to be more specific — name the file,
the folder, the number — and run once more. Note what v1 said, what v2 said, and why v2
worked. That's a bonus on its own.

---

## ✅ Scoring

| | Points |
|---|---|
| Instructions committed, and before/after diffs showing a rule being obeyed | **15** |
| Instructions committed, no evidence it changed behaviour | 7 |

### 🌟 Bonus

| | Points |
|---|---|
| Show the two diffs side by side — the difference *is* the demo | **+5** |
| A rule you had to rewrite because v1 was ignored, and why v2 worked | **+5** |
| A rule that's genuinely specific to your real team, not this lab app | **+5** |

---

## 🎬 Demo tip

This is one of the best three-minute demos on the board: **same vague prompt, two diffs, side
by side.** The room instantly gets it, and everyone goes home and writes one.

---

## 🆘 Stuck?

| Symptom | Cause |
|---|---|
| Both diffs look identical | Rules too vague, or you reused the old session instead of starting a new one |
| Run 2 diff is enormous | You forgot `git checkout .` after run 1 — it stacked |
| Agent ignores the file entirely | Wrong path — it must be exactly `.github/copilot-instructions.md` |
| Nothing to compare | Issue was too trivial; pick one touching two or three files |

---

**Next →** [Plan First](3-plan-first.md) · [Not A Diff](6-not-a-diff.md) · [the board](../README.md#the-board)

*Adapted from [Lesson 3](https://github-samples.github.io/copilot-workshops/app/3-custom-instructions/).*
