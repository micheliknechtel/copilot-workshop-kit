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

## 🧭 Read this first — two things that decide whether this works

### 1. The agent is not repeatable, so "compare two diffs" proves nothing

Run the same vague prompt twice with **no rule changes at all** and you get two different
diffs. Here are two real runs of the same issue in the lab repo:

| | Run A | Run B |
|---|---|---|
| Files touched | 8 | 13 |
| `src/pages/index.astro` | **deleted** | **modified** |
| New route file | `[...page].astro` | `page/[page].astro` |
| Extra files | — | `src/lib/pagination.ts`, `GameList.astro`, `pagination.test.ts` |

Nothing was ruled. The diffs still diverge wildly.

So `diff before.diff after.diff` is **guaranteed** to show a large difference whether or not
your rule worked. There is nothing to conclude from it. This challenge therefore uses a
different pass condition:

> 🎯 **You pick one rule, and one shell command whose output is empty when the rule is
> obeyed.** Pass = that command prints something before the rule, and nothing after. No
> eyeballing, no judgement call.

And to know which behaviour is *stable* enough to rule against, you run the baseline
**twice** and only target what **both** runs did. Anything only one run did is noise.

### 2. Rules only reach a new session once they're on `main`

**In the Copilot app, every session gets its own branch and its own working copy.**

| | |
|---|---|
| 🔁 **A new session branches from `main`.** | Rules sitting as an uncommitted edit — or on another session's branch — have never been seen by it. Merge to `main` first. |
| 📦 **The agent commits its work.** | So plain `git diff` prints nothing. Use `git diff origin/main...HEAD`. |

> ❌ `git diff` → empty, every time. It shows unstaged changes only, and never shows new
> files — which is exactly where a new test lands.
>
> ✅ `git fetch origin && git diff origin/main...HEAD` → the actual change set.

Two traps worth 30 seconds each:

- **You cannot `git checkout main` inside a session** — it fails with
  `fatal: 'main' is already used by worktree at …`. Merge your rules with a PR on
  github.com, not locally.
- **`git show main:…` reads your *local* `main`, which merging on github.com does not
  move** — and `git fetch` only moves `origin/main`. Always verify against `origin/main`.

**Using the CLI or a single checkout instead?** You're on one branch throughout. Replace
`origin/main...HEAD` with `git diff`, and instead of merging, just save the file and start a
new conversation.

---

## Do it

### 1. Capture two baselines (6 min)

Pick an issue you did **not** use in Challenge 1. It needs to be big enough to touch three or
more files — a one-line fix gives you nothing to rule against. In the lab repo, issue 6
(pagination) is a known-good pick and is the worked example below; substitute your own number
if you already used it.

Run it **twice, in two separate fresh sessions**, with the same deliberately vague prompt:

```
Fix issue 6
```

In each session, save what it did:

```bash
git fetch origin
git diff --name-status origin/main...HEAD > /tmp/baseA.txt   # session 1
git diff --name-status origin/main...HEAD > /tmp/baseB.txt   # session 2
```

> 🛑 **File empty?** You ran plain `git diff`, or you're in the wrong session's folder. Check
> `pwd` and use the `origin/main...HEAD` form.

Leave both sessions alone — they are your evidence.

### 2. Find the stable behaviour (2 min)

Only what **both** runs did is worth ruling against:

```bash
comm -12 <(sort /tmp/baseA.txt) <(sort /tmp/baseB.txt)
```

In the lab repo this typically shows both runs editing `README.md`, adding a component under
`src/components/`, and adding a spec under `e2e-tests/`.

> 🚦 **Gate: you need at least three lines here.** Fewer means the issue was too small or too
> open-ended to have a stable core — go back to step 1 and pick a bigger issue. For reference,
> issue 6 yields 6 stable entries out of 15 total across both runs.

> ⚠️ **Skip anything the shipped instructions already demand.** The lab repo's
> `copilot-instructions.md` already orders the agent to update the README, update the
> instructions file, and add tests — and issue 6's own acceptance criteria demand Vitest and
> Playwright coverage explicitly. A rule contradicting those is a coin flip, not a demo.
> Target **file scope** instead — nothing else mandates it.

### 3. Write one rule, and its assertion (3 min)

Append a `## Never` section to `.github/copilot-instructions.md`. Rules must be **specific
and checkable** — a reviewer should point at a diff and say "that broke rule 2" without
arguing.

```markdown
## Never

- Never create a new file under `src/components/` — extend an existing component instead
- Never add a runtime dependency to `package.json` without asking first
- Never modify a file under `e2e-tests/` unless the issue names end-to-end behaviour
```

Now pair your rule with the command that decides it:

| Rule | Assertion — must print **nothing** when obeyed |
|---|---|
| No new files under `src/components/` | `git diff --name-status origin/main...HEAD \| grep '^A.*src/components/'` |
| No new runtime dependency | `git diff origin/main...HEAD -- package.json \| grep '^+ *"'` |
| Don't touch `e2e-tests/` | `git diff --name-only origin/main...HEAD \| grep '^e2e-tests/'` |

**Run your assertion against both baseline sessions now.** It must print something in
**both**. If it only fires in one, that behaviour was noise — go back to step 2 and pick
another.

| ❌ Ignored | ✅ Obeyed |
|---|---|
| `Write good code` | `Keep exported functions under 40 lines` |
| `Add tests` | `Every bug fix ships with a regression test in the matching *.test.ts` |
| `Don't make a mess` | `Never create a new file under src/components/` |

The left column is unfalsifiable, so there is nothing to comply with. The right column names
a file, a folder, a number, or an action.

### 4. Ship the rules to `main` — alone (2 min)

> 🛑 **The single most common failure: shipping the rules and the issue fix in the same
> branch.** Then nothing ever lands on `main` by itself, no later session ever sees the
> rules, and every run looks the same. The rules PR must touch
> **`.github/copilot-instructions.md` and nothing else.**

```bash
git add .github/copilot-instructions.md
git commit -m "Add house rules"
git push -u origin HEAD
```

Open the PR, merge it on github.com, then verify it actually landed:

```bash
git fetch origin
git show origin/main:.github/copilot-instructions.md | grep "## Never"
```

> 🛑 **No output?** It isn't on `main` yet and the next session will not see it. Note this
> checks `origin/main` — checking plain `main` prints nothing even on success.

If your main checkout is a separate folder, refresh it so new sessions branch from the rules:

```bash
git -C /path/to/your/main/checkout pull
```

### 5. Prove it (2 min)

1. **Start a brand-new session.** It branches from `main`, so it picks up your rules.
2. Give it the **exact same prompt** as step 1: `Fix issue 6`
3. Run your assertion one last time:

```bash
git fetch origin
git diff --name-status origin/main...HEAD | grep '^A.*src/components/'   # your assertion
```

**You're done when the assertion printed something in both baseline runs and prints nothing
here.** That's the full 15 points — a binary result, not an opinion.

### 6. Tighten it (bonus)

Assertion still firing? Rewrite **that one rule** to be more specific — name the folder, the
file, the number — merge again, rerun. Note what v1 said, what v2 said, and why v2 worked.

---

## ✅ Scoring

| | Points |
|---|---|
| Rules merged to `main` alone, and an assertion that fires on both baselines and not after | **15** |
| Rules merged, no assertion evidence that behaviour changed | 7 |

### 🌟 Bonus

| | Points |
|---|---|
| Show the assertion output before and after — the flip *is* the demo | **+5** |
| A rule you had to rewrite because v1 was ignored, and why v2 worked | **+5** |
| A rule that's genuinely specific to your real team, not this lab app | **+5** |
| A candidate rule you **rejected** because it fired on only one baseline | **+5** |

---

## 🎬 Demo tip

Two terminal lines: the assertion firing on the baseline, and the same command silent after
the rules. Three minutes, no diff-reading, and the room instantly gets it.

---

## 🆘 Stuck?

| Symptom | Cause |
|---|---|
| Baseline file is 0 bytes | You ran plain `git diff`. The agent **commits** — use `git diff origin/main...HEAD` |
| Both runs look nothing alike | Expected. That's why you baseline twice and target only the overlap |
| Assertion fires on one baseline only | Noise, not a convention. Pick another behaviour from step 2 |
| Every run identical, rules seem ignored | Rules never reached `main` alone. Rerun the `git show origin/main:…` check |
| `git checkout main` fails | You're in a session worktree. Merge via PR on github.com instead |
| `git show main:…` empty after merging | Local `main` is stale and `git fetch` doesn't move it — check `origin/main` |
| Agent ignores the file entirely | Wrong path — must be exactly `.github/copilot-instructions.md` |
| Rule obeyed but it was already mandated | The shipped instructions already required it. Target file scope instead |

---

**Next →** [Plan First](3-plan-first.md) · [Not A Diff](6-not-a-diff.md) · [the board](../README.md#the-board)

*Adapted from [Lesson 3](https://github-samples.github.io/copilot-workshops/app/3-custom-instructions/).*
