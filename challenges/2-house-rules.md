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
> page — you're **adding rules to an existing file**. Don't delete what's already there.

---

## 🧭 Read this first — how sessions see your rules

This trips up almost everyone, so it's worth 30 seconds.

**In the Copilot app, every session gets its own branch and its own working copy of the
repo.** That has two consequences that decide whether this challenge works at all:

| | |
|---|---|
| 🔁 **Rules only reach a new session once they're on `main`.** | A new session branches from `main`. If your rules are sitting as an uncommitted edit in *another* session, the new one has never seen them. **Commit, merge to `main`, then start the next session.** |
| 📦 **The agent commits its work.** | So plain `git diff` shows **nothing**. To see what a session did, diff against the base branch: `git diff main...HEAD` |

> ❌ `git diff` → empty, every time. It shows unstaged changes only, and it never shows new
> files — which is exactly where a regression test would land.
>
> ✅ `git diff main...HEAD` → the actual change set.

**Using the CLI or an editor in a single checkout instead?** Then you're on one branch the
whole time. Substitute `git diff` for `git diff main...HEAD`, and instead of merging to
`main`, just save the file and start a new conversation.

---

## Do it

The order matters. You capture the "before" **first**, because once the rules are on `main`
you can't get an un-ruled run any more.

### 1. Capture a baseline (5 min)

1. Pick an issue you did **not** use in Challenge 1 — check the Issues tab.
2. Start a session and give it a prompt as vague as you dare. Literally just:

   ```
   Fix issue 6
   ```

   (Substitute your issue number. The vagueness is the point — it's what lets the rules show up.)

3. When it finishes, save the diff:

   ```bash
   git diff main...HEAD > /tmp/before.diff
   wc -l /tmp/before.diff        # sanity check — must not be 0
   ```

> 🛑 **`/tmp/before.diff` is empty?** You either ran plain `git diff`, or you ran it in a
> different session's folder than the one that did the work. Check you're in the right
> directory (`pwd`) and use the `main...HEAD` form.

Now **leave that session alone.** Don't reset it, don't delete it — it *is* your evidence.
The next run happens in a fresh session, which gets its own branch and folder.

### 2. Write the rules — and get them onto `main` (5 min)

Open `.github/copilot-instructions.md` and **append** a `## Never` section at the end.

> 💡 **The "Never" section earns its keep fastest.** It's what stops the agent handing you a
> 400-line diff where 380 lines are reformatting. That's the class of change nobody reviews
> properly.

Rules must be **specific and checkable**. A reviewer should be able to point at a diff and
say "that broke rule 3" without arguing about it.

```markdown
## Never

- Never reformat, reorder, or re-indent code in a file you weren't asked to change
- Never add a runtime dependency without asking first
- Never ship a bug fix without a regression test in the matching `*.test.ts`
```

| ❌ Ignored | ✅ Obeyed |
|---|---|
| `Write good code` | `Keep exported functions under 40 lines` |
| `Add tests` | `Every bug fix ships with a regression test in the matching *.test.ts` |
| `Don't make a mess` | `Never reformat a file you weren't asked to change` |

The left column is unfalsifiable, so there's nothing to comply with. The right column names a
file, a number, or an action.

**Then ship it to `main`** — this is the step that makes the whole challenge work:

```bash
git add .github/copilot-instructions.md
git commit -m "Add house rules"
```

Push it and merge the PR, or merge locally. Verify it landed:

```bash
git show main:.github/copilot-instructions.md | grep "## Never"
```

> 🛑 **No output?** Your rules aren't on `main` yet, and the next session will not see them.
> Fix that before continuing or step 3 will produce an identical diff and you'll think the
> rules failed.

### 3. Prove it (4 min)

1. **Start a brand-new session.** It branches from `main`, so it picks up your rules.
2. Give it the **exact same prompt** as step 1: `Fix issue 6`
3. Compare:

   ```bash
   git diff main...HEAD > /tmp/after.diff
   diff /tmp/before.diff /tmp/after.diff
   ```

**You're done when at least one rule is visibly obeyed in `after.diff` and visibly not obeyed
in `before.diff`.** For example:

- `before.diff` reformats a file the issue never mentioned; `after.diff` leaves it alone
- `before.diff` has no test; `after.diff` adds one in the matching `*.test.ts`
- `before.diff` adds a dependency; `after.diff` asks first

That single contrast is worth the full 15 points.

### 4. Tighten it (1 min)

Rule still ignored? Rewrite **that one rule** to be more specific — name the file, the folder,
the number — merge again, and rerun. Note what v1 said, what v2 said, and why v2 worked.
That's a bonus on its own.

---

## ✅ Scoring

| | Points |
|---|---|
| Rules merged to `main`, and before/after diffs showing a rule being obeyed | **15** |
| Rules merged, no evidence it changed behaviour | 7 |

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
| `before.diff` is 0 bytes | You ran plain `git diff`. The agent **commits** — use `git diff main...HEAD` |
| Both diffs look identical | Rules never reached `main`. Run the `git show main:...` check in step 2 |
| New test file missing from the diff | `git diff` never shows untracked files — another reason to diff against `main` |
| Agent ignores the file entirely | Wrong path — must be exactly `.github/copilot-instructions.md` |
| Rules present but still ignored | Too vague. See the ❌/✅ table and go to step 4 |
| Nothing meaningful to compare | Issue was too trivial; pick one touching two or three files |

---

**Next →** [Plan First](3-plan-first.md) · [Not A Diff](6-not-a-diff.md) · [the board](../README.md#the-board)

*Adapted from [Lesson 3](https://github-samples.github.io/copilot-workshops/app/3-custom-instructions/).*
