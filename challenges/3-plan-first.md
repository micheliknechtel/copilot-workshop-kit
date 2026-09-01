# 🗺️ Challenge 3 — Plan First

> **20 points · ~15 minutes**

**Get the agent to tell you what it's going to do — before it does it. Then let it run
unsupervised.**

---

## The idea

Reviewing a plan takes a minute. Reviewing a wrong 400-line diff takes twenty — and you paid
for that diff either way.

**Plan mode** makes the agent propose an approach and wait. You correct the misunderstanding
while it's still a sentence, not a thousand lines of TypeScript.

**Autopilot** is the other end: once you trust the plan, let it work through the steps
without stopping to ask.

Together they're the real workflow: **think slow, then move fast.**

---

## Do it

### 1. Pick something bigger (2 min)

This time, deliberately choose a **larger** issue — one touching several files, or a feature
rather than a fix. Plan mode on a one-line bug is pointless.

### 2. Ask for the plan (4 min)

Start the session in **Plan mode** and describe the goal. You'll get an approach back instead
of code.

**Read it properly.** You're looking for:

- ❓ Did it understand the actual requirement, or a nearby one?
- 📁 Is it touching files you didn't expect? Ask why.
- 🧪 Does the plan include tests, or did it forget?
- 🪆 Is it doing more than you asked — a refactor smuggled into a bug fix?

### 3. Correct it (3 min)

Don't accept the first plan. Push back on at least one thing:

> That's more than I need. Skip the refactor in step 3 — just fix the bug and add a test.
> Also, don't touch the API layer.

**This is the whole point of the challenge.** Correcting at the plan stage is the cheapest
possible intervention.

### 4. Turn it loose (5 min)

Approve the plan and run with **Autopilot** so it executes without checking in at every step.

Watch it. Autopilot is fast and confident, which is exactly why you wanted the plan reviewed
first.

### 5. Review and ship (1 min)

Compare the result against the plan you approved. Did it do what it said?

---

## ✅ Scoring

| | Points |
|---|---|
| Plan reviewed, corrected, executed on Autopilot, PR open | **20** |
| Plan reviewed and executed, no correction needed | 12 |
| Plan generated, not executed | 5 |

### 🌟 Bonus

| | Points |
|---|---|
| Show the plan **before** and **after** your correction | **+5** |
| You caught a real misunderstanding at plan stage — say what the diff would have been | **+10** |
| Autopilot went somewhere you didn't want, and you show where you'd have intervened | **+5** |

> 💰 **That +10 is the biggest single bonus on the board.** Catching a wrong plan before it
> becomes a wrong diff is the most valuable thing in this hackathon. If it happens to you,
> demo it.

---

## ⚠️ Honest note on Autopilot

Autopilot is genuinely useful where you trust the scope and you have tests. It is not a way
to avoid thinking — it's a way to avoid *re-confirming* thinking you've already done.

Good judgement: plan reviewed + tests exist + scope is bounded → Autopilot.
Bad judgement: you're not sure what you want → Autopilot.

---

**Next →** [Two At Once](5-two-at-once.md) · [Give It Eyes](4-give-it-eyes.md) · [the board](../README.md#the-board)

*Adapted from [Lesson 4](https://github-samples.github.io/copilot-workshops/app/4-plan-autopilot-skills/).*
