# 4 — Token optimization: ten levers

Everything here is about the same goal: **more outcome per credit.** Not less Copilot — more
value from the same spend.

The levers are ordered by impact. If you only do three, do the first three.

---

## 1. Right-size the model 🥇

**Impact: very high. Effort: none.**

The single largest driver of cost variance is model choice, and the default habit is to reach
for the most capable model available regardless of task.

Most day-to-day engineering work does not need a frontier model:

| Task | Start with |
|---|---|
| Rename, format, small refactor | Smallest available |
| Bug fix in known files | Small / fast |
| Write tests for existing code | Small / fast |
| Implement a described feature | Mid-tier |
| Design an approach across many modules | Frontier |
| Debug something genuinely subtle | Frontier |

**Escalate on failure, don't start at the top.** A failed cheap attempt followed by a
successful expensive one still frequently costs less than starting expensive — and you learn
where the boundary actually is.

Enable **auto model selection** if it's available to you; it does a reasonable job of this
without anyone having to think about it.

---

## 2. Scope your prompts to files 🥈

**Impact: very high. Effort: minimal.**

> ❌ "Fix the checkout bug"

> ✅ "Fix the checkout bug. It's in `src/lib/cart.ts` in `calculateTotal()` — tax is applied
> before the discount instead of after. Change that file and `cart.test.ts` only."

The second prompt saves an exploration phase where the agent reads a dozen files trying to
work out what you meant. **You already knew. Telling it is free.**

Rule of thumb: if you can name the file, name the file.

---

## 3. Stop runs that have lost the plot 🥉

**Impact: high. Effort: attention.**

Watch for the agent re-reading the same files, retrying the same failing command, or writing
increasingly speculative code. These are all the same signal: **it doesn't have what it needs
and more time will not supply it.**

Stopping and re-prompting with better context is nearly always cheaper than waiting for a
confused session to finish.

Set yourself a personal ceiling — five minutes, or three failed test runs — and hold to it.

---

## 4. Use repository custom instructions

**Impact: high, and it compounds. Effort: an hour, once.**

A `.github/copilot-instructions.md` file is read automatically on every request in that
repository. Put the things you'd otherwise re-explain every session:

```markdown
# Project context
Astro + TypeScript. Tests use Vitest.

# Conventions
- Prefer named exports
- No new dependencies without asking
- Every bug fix gets a regression test

# Don't
- Don't reformat files you weren't asked to change
- Don't modify anything under `src/generated/`
```

That last section prevents entire classes of expensive, unreviewable diffs. Written once,
paid for on every subsequent session, by everyone on the team.

📖 [Adding repository custom instructions](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)

---

## 5. Plan before you build

For anything non-trivial, ask for a **plan first**, review it, then execute.

Reviewing a plan takes a minute. Reviewing a wrong 400-line diff takes twenty, and you pay
for the diff whether you keep it or not. Catching a misunderstanding at the plan stage is the
cheapest correction available.

---

## 6. One task per session

Long sessions carry their entire history forward. A session that has done three unrelated
things is paying to re-transmit two irrelevant ones.

Start a fresh session per logical task. It's also much easier to review.

---

## 7. Reuse work with skills and prompt files

If someone writes an excellent prompt for a recurring job — a security review pass, a
migration to a new API, a test-generation standard — that prompt should not live in one
person's history.

Skills and prompt files turn a good prompt into shared infrastructure. Instead of twenty
people iterating their way to a decent prompt at twenty separate costs, one person does it
once.

---

## 8. Delegate long jobs to the cloud agent

Well-specified, self-contained, slow work — dependency bumps, mechanical migrations, test
backfill — can be handed to the coding agent rather than occupying an interactive session.
It works while you do something else and returns a PR.

Best for tasks where you can describe **done** precisely.

---

## 9. Know where the free tier ends

**Completions and next edit suggestions are not billed as credits.** Agentic features are.

There is a real category of task where a developer types with completions helping and finishes
faster than an agent session would have started. Knowing which is which is a skill, and it's
worth naming out loud rather than assuming people will work it out.

---

## 10. Make consumption visible weekly

**Impact: high over time. Effort: fifteen minutes a week.**

Everything above is a habit, and habits need feedback. Export usage weekly and put it
somewhere the team sees it.

Not to shame anyone — to make the range visible. When someone sees they used four times the
team median, they ask why, and that question is the whole mechanism.

Pair it with a denominator, however rough: credits per merged PR, per issue closed, per
week per active developer. A number with no denominator can only ever go "up" or "down,"
which tells you nothing about whether it was worth it.

---

## A 30-day starting point

| Week | Do this |
|---|---|
| **1** | Measure only. Export usage, find your distribution, don't change behaviour yet. |
| **2** | Land `copilot-instructions.md` in your top 5–10 repositories. |
| **3** | Introduce model right-sizing. Ask people to start small and escalate. |
| **4** | Publish the first weekly usage view with a denominator. Review what changed. |

Then choose your budget posture deliberately — alerting where an outage would be
unacceptable, hard caps where the blast radius is one person.
