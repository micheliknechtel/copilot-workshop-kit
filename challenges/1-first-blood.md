# 🔴 Challenge 1 — First Blood

> **20 points · ~15 minutes · Everyone does this one**

**Take a real issue from your backlog, give it to an agent, and open a pull request.**

---

## Why this one is mandatory

Everything else builds on it. And the first agent session is where most people's mental model
changes — from "faster autocomplete" to "I can delegate this."

---

## Do it

### 1. Pick an issue (2 min)

Open the **Issues** tab in your repo. Pick one that is:

- ✅ Small, and clearly described
- ✅ Touching two or three files at most
- ❌ **Not** the most ambitious one on the list

> 💡 The instinct is to grab the hardest issue to test the agent. Resist it. You learn far
> more in 15 minutes from a change you can fully review than one you can't.

### 2. Start a session — and scope it (3 min)

In the Copilot app, start a session against your repo.

**Two habits to form right now:**

**Name the files.** Compare:

> ❌ `Fix issue 4`

> ✅ `Fix issue 4 — the cart total is wrong. It's in src/lib/cart.ts in calculateTotal().
> Change that file and its test only. Don't refactor anything else.`

The second is cheaper *and* gives you a diff you can actually review.

**Start on a small model.** You can always escalate. Starting on a frontier model for a
two-file bug fix is the most expensive habit in the room, and it's the default one.

### 3. Watch it work (5 min)

Don't tab away. Watch for:

- 🔍 Which files it opens before it edits anything
- 🔄 Whether it re-reads the same file over and over → your prompt was too vague
- 🧪 Whether it runs the tests itself
- 🔁 Whether it's stuck retrying the same failing thing

> ⏱️ **Still going at 8 minutes? Stop it.** A confused session burns money fastest exactly
> when it's producing least. Stopping and re-prompting beats waiting, almost every time.

### 4. Review it like a colleague's PR (3 min)

| Look for | Why |
|---|---|
| Changes outside what you asked for | Review burden, surprise regressions |
| A test that asserts the bug instead of the fix | Green CI, broken code |
| A plausible function nothing calls | Dead code hiding in a passing build |
| New dependencies you didn't ask for | Supply chain surprise |

Then run them yourself:

```bash
npm run test:unit
```

**Something wrong? Don't fix it by hand.** Tell the agent what's wrong and let it correct
itself. A correction round is cheap, and steering is the skill you're here to build.

### 5. Ship it (2 min)

Push the branch, open the PR. In the description, note **which model you used** and **roughly
how long it took**.

---

## ✅ Scoring

| | Points |
|---|---|
| PR open, tests passing | **20** |
| PR open, tests failing but you can explain why | 12 |
| Session ran, no PR | 5 |

### 🌟 Bonus

| | Points |
|---|---|
| Show the prompt you rewrote, and why v2 worked better | **+5** |
| You stopped a run that had gone wrong, and explain how you spotted it | **+5** |
| Same issue done twice on two model tiers, with both costs | **+5** |

---

## 🆘 Stuck?

| Symptom | Cause |
|---|---|
| App won't sign in | Admin policy — see [ADMIN.md](../ADMIN.md) |
| `npm install` fails | Proxy, or Node older than 22 |
| Agent can't run tests | Node not on PATH — open a fresh terminal |
| Agent stops mid-task | Budget cap — grab a facilitator |

---

**Done? →** Pick your next from the [board](../README.md#the-board).

*Adapted from [Lesson 2](https://github-samples.github.io/copilot-workshops/app/2-first-agent-session/).*
