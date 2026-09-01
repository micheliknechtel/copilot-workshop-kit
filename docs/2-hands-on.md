# 2 — Hands on: ship a real PR with an agent

**Duration:** 25 minutes
**Prerequisite:** [1-attendee-setup.md](1-attendee-setup.md) completed
**Based on:** [Lesson 2 of the official workshop](https://github-samples.github.io/copilot-workshops/app/2-first-agent-session/)

---

## The goal

In 25 minutes, every person in the room takes a real issue from a real backlog, gives it to
an agent, reviews what came back, and opens a pull request — then reads what it cost.

The pull request is not the point. **The point is developing judgement about when to reach
for an agent, and what that reach costs.**

---

## Minute by minute

### 0:00–0:03 · Pick an issue

Open your copy of the lab repository and look at the **Issues** tab. The template seeded a
backlog for you.

Pick one that is:

- ✅ Small and well described
- ✅ Touches two or three files at most
- ❌ Not the most interesting or ambitious one on the list

> 💡 The instinct is to grab the hardest issue to see if the agent can cope. Resist it. In
> 25 minutes you learn far more from a task you can fully review than from one you can't.

---

### 0:03–0:06 · Start a session

In the Copilot app, create a session against your repository and paste in the issue.

Two habits worth forming right now:

**Be specific about scope.** Compare:

> ❌ "Fix issue 4"

> ✅ "Fix issue 4. The bug is in the cart total calculation. Change only
> `src/lib/cart.ts` and its test file. Don't refactor anything else."

The second version costs less **and** produces a smaller diff you can actually review.

**Pick your model deliberately.** Start on a **small, fast model**. You can always escalate.
Starting on a frontier model for a two-file bug fix is the most common and most expensive
habit in the room.

---

### 0:06–0:14 · Let it work — and watch

While the agent runs, **read what it's doing**. Specifically watch for:

- 🔍 Which files it opens before editing anything
- 🔄 Whether it re-reads the same file repeatedly (a signal your prompt was under-specified)
- ✅ Whether it runs the tests itself
- 🔁 Whether it gets stuck in a retry loop

> ⏱️ **If it's still going at 8 minutes, stop it.** A long-running agent session that has
> lost the plot burns credits at exactly the moment it's producing least value. Stopping and
> re-prompting with better constraints is nearly always cheaper than waiting.

---

### 0:14–0:20 · Review like it's a colleague's work

Read the diff properly. You are looking for the classic agent failure modes:

| Look for | Why it matters |
|---|---|
| Changes outside the scope you asked for | Review burden, unintended regressions |
| Tests that assert the bug rather than the fix | Passes CI, fixes nothing |
| A plausible-looking function that isn't called | Dead code, invisible in a green build |
| Dependencies added you didn't ask for | Supply-chain and licence surprises |

Then run the tests yourself:

```bash
npm test
```

If something's wrong, **don't fix it by hand.** Tell the agent what's wrong and let it
correct itself — a correction round is much cheaper than a fresh session, and it teaches you
how to steer.

---

### 0:20–0:23 · Open the pull request

Push the branch and open the PR. Then do one thing that costs nothing and matters a lot:

**In the PR description, write down which model you used and roughly how long the session took.**

Do this every time for a fortnight and your team will have real data about which model tier
is right for which class of work. Nobody has this data because nobody writes it down.

---

### 0:23–0:25 · The credit check-in 💰

**Everybody stop. Everybody look.**

Open your Copilot usage view and read your own consumption for the last hour.
See [3-measuring-credits.md](3-measuring-credits.md) for exactly where.

Then say the number out loud around the room.

You'll see a spread — often 5× or more between the cheapest and most expensive person, for
essentially the same task. Two questions worth putting to the room:

1. **What did the cheapest person do differently?** (Almost always: a smaller model, a
   tighter prompt, or stopping a run that had gone astray.)
2. **Was the most expensive result better?** (Usually not.)

> 🎯 **This three-minute block is the most valuable part of the session.** It is also the
> first thing to get cut when you run late. Cut the demo instead.

---

## If you finish early

- Try the **same issue again** on a different model tier and compare cost and diff quality
- Add a `.github/copilot-instructions.md` to your repo and re-run — see
  [Lesson 3](https://github-samples.github.io/copilot-workshops/app/3-custom-instructions/)
- Explore Plan mode and Autopilot —
  [Lesson 4](https://github-samples.github.io/copilot-workshops/app/4-plan-autopilot-skills/)

## If you got stuck

That's a valid result and worth reporting. Where people get stuck is usually:

| Symptom | Likely cause |
|---|---|
| App won't sign in | Enterprise client policy — [0-admin-setup.md](0-admin-setup.md) |
| Can't create repo from template | EMU restriction — ask for the fallback repo |
| `npm install` fails | Proxy or missing Node 22+ |
| Agent can't run tests | Node not on PATH — open a fresh terminal |
| Agent stops mid-task | Budget hard cap reached — find an admin |

---

## What to take away

Three things, in order of how much money they save you:

1. **Choose the smallest model that can do the job.** Escalate only when it fails.
2. **Scope your prompt to specific files.** Vague scope is expensive twice — once in tokens,
   once in review time.
3. **Stop runs that have lost the plot.** Sunk cost is real, and waiting is not free.
