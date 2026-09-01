# Facilitator guide

Read this before anything else. The two things that decide whether the session works are
**pre-flight** and **protecting the hands-on block**. Everything else is recoverable.

---

## The one-week countdown

| When | Do this |
|---|---|
| **T-7 days** | Send [docs/0-admin-setup.md](docs/0-admin-setup.md) to an enterprise owner. Get a **named** person to own it. |
| **T-7 days** | Have one EMU user dry-run the template copy. Decide the target org. |
| **T-5 days** | Send [docs/1-attendee-setup.md](docs/1-attendee-setup.md) to attendees, with the org name filled in. |
| **T-2 days** | Ask for a show of hands: who is fully set up? Chase the gaps. |
| **T-1 day** | Confirm both policy switches are on, in writing. |
| **T-30 min** | Test the room network yourself. Run one agent session end to end. |

> 🚨 **If you cannot get written confirmation on the two policy switches, assume Plan B.**
> See below.

---

## Plan A vs Plan B

**Plan A — everyone builds.** Requires: policies on, template copy working, Node 22+
installed, network open. This is the version you want.

**Plan B — you build, they watch and direct.** You drive one screen. The room chooses the
issue, chooses the model, critiques the diff, and predicts the cost before you reveal it.

**Assume Plan B unless pre-flight is explicitly confirmed.** Plan B is not a failure mode —
a well-run Plan B with an engaged room beats twenty people staring at a login error. What
kills a session is discovering at 0:58 that you needed Plan B and having no version of it
ready.

**Prepare both. Decide at T-1 day.**

---

## Run of show — 90 minutes

| Time | Block | Notes |
|---|---|---|
| **0:00–0:08** | **Why now** | Two things changed: agentic usage is metered, and the fast model tier is being replaced. Frame both as opportunities to spend better, not as bad news. |
| **0:08–0:33** | **Token optimization** | [docs/4-token-optimization.md](docs/4-token-optimization.md). Lead with *completions are not billed* — it resets the room's assumption immediately. Then the top three levers. |
| **0:33–0:43** | **Model migration** | [docs/5-model-migration.md](docs/5-model-migration.md). Short. Better and cheaper, plus one real action: find hard-coded model IDs. |
| **0:43–0:58** | **Copilot app demo** | [docs/6-copilot-app-tour.md](docs/6-copilot-app-tour.md). Live. Land parallel sessions. |
| **0:58–1:23** | **HANDS ON** 🔒 | [docs/2-hands-on.md](docs/2-hands-on.md). **Protect this block.** |
| **1:23–1:30** | **Close** | Decisions and owners, not a summary. |

### Where to steal time when you run late

You will run late. Take it in this order:

1. ✂️ Model migration → 5 minutes. It's genuinely simple.
2. ✂️ Trim the demo to sessions + parallel + one skill.
3. ✂️ Compress "why now" to three minutes.
4. ❌ **Never take it from hands-on.** And never, ever cut the credit check-in — it is the
   three minutes people remember.

---

## Closing the session

Don't summarise. Get decisions, with names attached:

- **Who** owns confirming the client policies are correctly set?
- **Who** runs the search for hard-coded model IDs before 10 September?
- **Who** lands `copilot-instructions.md` in the top five repositories?
- **What is our budget posture** — alerting where an outage is unacceptable, hard caps
  per user?
- **When do we reconvene** to look at usage data?

Then offer the full-day format below.

---

## Facilitation notes

**Set model expectations in the first two minutes.** If people start on frontier models
because that's the habit, your credit check-in shows a much less interesting spread.

**Walk the room during hands-on.** The failures are visible on screens, not in raised hands.
Most people won't tell you they're stuck.

**Let someone fail publicly, kindly.** An agent producing a confidently wrong diff is the
best teaching moment available and it cannot be scripted.

**Don't defend the product.** If someone says it got something wrong, agree, and ask what
they'd have put in the prompt instead. That's the skill you're there to build.

**On roadmap questions:** answer only from public sources. If you don't have one:
*"I can't commit to timing, but I can find out and come back to you — and if you'd like early
access to what's next, I can put your name forward."* Say it once, warmly, and move on.

---

## Contingencies

| If… | Then |
|---|---|
| Policies are off | Plan B. You drive; the room directs. |
| Template copy blocked for EMU | Use the pre-mirrored internal repo. Have the URL ready. |
| Node not installed on several laptops | Pair people up. Two per laptop works fine. |
| Network blocks npm | Skip Playwright MCP entirely. Don't debug proxies live. |
| Someone hits a budget cap | Pair them with a neighbour. Note it — it's a real finding. |
| Running 15 minutes late | Cut migration and demo hard. Start hands-on at 0:58 regardless. |
| Room is quiet | Go to the credit check-in early. Numbers get people talking. |

---

# The full-day format

If the 90 minutes lands, this is the natural follow-up: one day, guided morning, real work
in the afternoon.

## Morning — guided (3 hours)

Work through the [official workshop](https://github-samples.github.io/copilot-workshops/app/)
on the lab repository. Lessons 1–5 comfortably fill a morning; 6–8 if the room moves quickly.

Run a **credit check-in after every lesson**, not just at the end. By lesson four people are
predicting their own numbers, which is the point.

## Afternoon — real repositories (3.5 hours)

Teams of 3–4, on their **own** code. Four tracks:

| Track | Brief |
|---|---|
| 🧹 **Kill the toil** | Find the most repetitive task on your team's backlog and automate it with an agent or a skill. |
| 💰 **The cheap agent** | Take a task you'd normally give a frontier model. Achieve the same result on the smallest model you can, using instructions and prompt scoping. Report both costs. |
| 🏛️ **Legacy meets agent** | Point an agent at your least-loved service. Documentation, test backfill, dependency audit — anything that makes it less frightening. |
| 🚀 **Ship a surface** | Build something with the app that isn't a diff: a canvas, a skill, an MCP integration your team would actually use. |

## Judging — 30 minutes

Three minutes per team. Score out of 20:

| Criterion | Points |
|---|---|
| **Real problem** — would you have done this anyway? | 5 |
| **Working result** — it runs, it's reviewable | 5 |
| **Reusable** — can another team pick this up tomorrow? | 5 |
| **Cost awareness** — do you know what it cost and why? | 5 |

**Award "Most Credit-Efficient" alongside the overall winner.** Weight it equally. It is the
award that changes behaviour after everyone goes home, and it costs you nothing to add.

## Leave-behinds

Every attendee should leave with:

- [ ] Their own copy of the lab repository
- [ ] At least one merged pull request from an agent session
- [ ] A `copilot-instructions.md` they wrote themselves
- [ ] Their own consumption number, and an explanation for it
- [ ] One habit they've committed to changing
