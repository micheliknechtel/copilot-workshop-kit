# 📜 Challenge 2 — House Rules

> **15 points · ~10 minutes**

**Stop repeating yourself. Teach the agent your conventions once, and make it obey them.**

---

## The idea

You just spent Challenge 1 explaining context in your prompt. Every teammate will explain the
same context tomorrow, badly, in their own words.

A `.github/copilot-instructions.md` file is read **automatically on every request** in that
repository. Write it once, everyone benefits, forever.

---

## Do it

### 1. Write the file (4 min)

Create `.github/copilot-instructions.md`. Keep it short — a wall of text gets ignored, by
models and humans alike.

```markdown
# Project
Astro + TypeScript. Unit tests run with Vitest via `npm run test:unit`.

# Conventions
- Prefer named exports over default exports
- Every bug fix ships with a regression test
- Keep functions under 40 lines

# Never
- Never add a dependency without asking first
- Never reformat a file you weren't asked to change
- Never touch anything under `src/generated/`
```

> 💡 **The "Never" section earns its keep fastest.** It's what stops the agent handing you a
> 400-line diff where 380 lines are reformatting. That's the class of change nobody reviews
> properly.

### 2. Prove it works (5 min)

The point is evidence, not vibes.

1. Pick a **second** issue
2. Run it, using a prompt **as vague as you dare** — `Fix issue 6`, nothing more
3. Check the diff against your rules

Did it use named exports? Did it write a regression test? Did it leave the formatting alone?

### 3. Tighten it (1 min)

Find a rule it ignored? Rewrite that rule to be more specific and run again.

Vague rules get ignored. `Write good code` does nothing. `Every bug fix ships with a
regression test in the matching .test.ts file` does something.

---

## ✅ Scoring

| | Points |
|---|---|
| Instructions file committed, and a diff that visibly follows a rule | **15** |
| File committed, no evidence it changed behaviour | 7 |

### 🌟 Bonus

| | Points |
|---|---|
| Show the same prompt before vs after — the diff difference is the demo | **+5** |
| A rule you had to rewrite because v1 was ignored, and why v2 worked | **+5** |
| A rule that's genuinely specific to your real team, not this lab app | **+5** |

---

## 🎬 Demo tip

This is one of the best three-minute demos on the board: **same vague prompt, two diffs, side
by side.** The room instantly gets it, and everyone goes home and writes one.

---

**Next →** [Plan First](3-plan-first.md) · [Not A Diff](6-not-a-diff.md) · [the board](../README.md#the-board)

*Adapted from [Lesson 3](https://github-samples.github.io/copilot-workshops/app/3-custom-instructions/).*
