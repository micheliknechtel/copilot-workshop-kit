# 🧑‍✈️ Facilitator guide

Two things decide whether this works: **pre-flight** and **protecting the build time**.
Everything else you can improvise.

---

## 🚨 One week out — the only truly blocking task

Send **[ADMIN.md](ADMIN.md)** to a **named** enterprise owner and get written confirmation.

Two policy switches control whether the Copilot app will sign in at all. If they're off,
nobody participates and there is no fix on the day.

Also: **have one person dry-run the template copy** into your target org. On Enterprise
Managed Users this can be blocked, and you want to discover that now, not at 0:12.

| When | Do |
|---|---|
| **T-7d** | ADMIN.md to a named owner. Template dry run. Decide the target org. |
| **T-5d** | Send [SETUP.md](SETUP.md) to attendees, org name filled in. |
| **T-2d** | Ask who's set up. Chase the silence. |
| **T-1d** | Written confirmation on both policies. |
| **T-30m** | Test the room wifi. Run one agent session yourself, end to end. |

---

## ⏱️ Run of show

| Time | Block | Notes |
|---|---|---|
| **0:00–0:10** | Kickoff | Teams of 2–3. Everyone opens the app and confirms sign-in **now** — find failures in minute 3, not minute 40. |
| **0:10–0:25** | Challenge 1, together | Everyone on the same challenge. Roam hard here. |
| **0:25–1:10** | Free play | Teams choose. This is the session. |
| **1:10–1:25** | Demos | 3 min each, **hard cut** |
| **1:25–1:30** | Awards | Fast and loud |

### If you're running late

Take it from demos (2 min each), never from build time. Build time is the product.

---

## 👟 During free play

**Walk constantly.** The failures are visible on screens, not in raised hands. Most people
won't tell you they're stuck.

**Watch for these four:**

| You see | Say |
|---|---|
| Everyone on the biggest model | *"Try that again on the small one. Bet you the diff's the same."* |
| A team watching a session flail for 10 min | *"Kill it. Re-prompt with the filenames. Faster and cheaper."* |
| A team stuck on the proxy for Challenge 4 | *"Drop it, take Challenge 5. Tell the room it was blocked — that scores."* |
| A team that's finished and gone quiet | *"Go do Challenge 6 on your own repo. Bonus points for real code."* |

**Let someone fail publicly, kindly.** An agent producing a confidently wrong diff teaches the
room more than any successful demo. When you spot one, ask them to save it for demos.

**Don't defend the product.** If someone says it got something wrong, agree — then ask what
they'd have put in the prompt instead. That's the skill you're actually teaching.

---

## 🏆 Judging

Points come from the challenge sheets. Add up to **10 bonus** per team at demo time:

| | |
|---|---|
| 🎬 It actually runs — demoed, not described | 0–3 |
| 🔁 Reusable by another team | 0–3 |
| 🧠 They show a prompt they rewrote, and why | 0–2 |
| 💸 They know what it cost | 0–2 |

Track it on [SCORECARD.md](SCORECARD.md).

### Give all four awards

🥇 Overall · 💸 Most Efficient · 🔧 Most Useful · 💥 **Best Failure**

**Best Failure is not a joke prize.** Judge it seriously and announce it with the same energy
as the winner. It's what makes people honest at the next one, and it's free.

---

## 🎯 Closing — five minutes, decisions not summary

Skip the recap. Get commitments with names on them:

- **Who** adds `copilot-instructions.md` to our top 5 repos this month?
- **Which team** tries parallel sessions on real work next sprint?
- **Who** owns checking our Copilot client policies are set the way we want?
- **When** do we do this again, on our own repos?

Then point them at the [full official workshop](https://github-samples.github.io/copilot-workshops/app/)
for the unhurried version.

---

## 🔥 Contingencies

| If | Then |
|---|---|
| **Policies are off** | Plan B: you drive one screen, room picks the issue, model and critiques the diff. Prepare this even if you don't need it. |
| **Template copy blocked (EMU)** | Use your pre-mirrored internal repo. Have the URL on a slide. |
| **Node missing on several laptops** | Pair up. Two per laptop works fine and is arguably better. |
| **npm blocked** | Kill Challenge 4 for the room. Announce it early so nobody burns time. |
| **Someone hits a budget cap** | Pair them with a neighbour. Note it — it's a real finding. |
| **Room is quiet** | Ask three teams for their credit number out loud. The spread is usually 5× and it starts an argument. |
| **Everything is broken** | Do Challenge 1 as a single guided demo, then Challenge 6 — canvases need almost nothing to work. |

---

## 📦 What everyone should leave with

- [ ] At least one PR from an agent session
- [ ] A `copilot-instructions.md` they wrote
- [ ] Their own credit number, and a theory about it
- [ ] One habit they're changing on Monday
