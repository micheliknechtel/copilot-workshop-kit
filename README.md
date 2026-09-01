# Copilot App Workshop Kit

**Everything a facilitator and attendees need to run a 90-minute GitHub Copilot app session — or scale it to a full-day hackathon.**

This kit does **not** replace the official GitHub workshop. It wraps it. The teaching
material is GitHub's, maintained by GitHub, and lives here:

👉 **https://github-samples.github.io/copilot-workshops/app/**

What this kit adds is the part the official workshop doesn't cover: **enterprise pre-flight,
facilitation timing, and cost awareness.** Those three things are what make the difference
between a session that works and a session that spends its first hour on installers.

---

## Start here

| You are… | Read this | When |
|---|---|---|
| 🧑‍✈️ **Facilitating** | [FACILITATOR.md](FACILITATOR.md) | Now |
| 🛡️ **A platform / Copilot admin** | [docs/0-admin-setup.md](docs/0-admin-setup.md) | **T-1 week — blocking** |
| 💻 **Attending** | [docs/1-attendee-setup.md](docs/1-attendee-setup.md) | Before you arrive |

> ⚠️ **The admin checklist is a hard dependency.** Two enterprise policy switches control
> whether the Copilot app will even sign in. If they're off, nobody can participate and there
> is no workaround on the day. Send [docs/0-admin-setup.md](docs/0-admin-setup.md) to an
> enterprise owner **one week ahead**.

---

## The 90-minute agenda

| Time | Block | Material |
|---|---|---|
| 0:00–0:08 | Why now — what changed in billing and models | [docs/4-token-optimization.md](docs/4-token-optimization.md) · [docs/5-model-migration.md](docs/5-model-migration.md) |
| 0:08–0:33 | Token optimization: getting more per credit | [docs/4-token-optimization.md](docs/4-token-optimization.md) |
| 0:33–0:43 | Model roadmap and migration | [docs/5-model-migration.md](docs/5-model-migration.md) |
| 0:43–0:58 | The Copilot app — live demo | [docs/6-copilot-app-tour.md](docs/6-copilot-app-tour.md) |
| **0:58–1:23** | **Hands on — ship a PR with an agent** | **[docs/2-hands-on.md](docs/2-hands-on.md)** |
| 1:23–1:30 | Close, decisions, next steps | [FACILITATOR.md](FACILITATOR.md) |

Scaling up? [FACILITATOR.md](FACILITATOR.md) also contains a **full-day format** —
guided morning on the official workshop, afternoon on your own repositories.

---

## The one rule

Every exercise ends with the same question:

> **What did that cost you in credits?**

Cost is normally something finance tells engineers about after the fact. Reading your own
consumption immediately after your own agent session turns it into something you own. It is
the single highest-leverage habit in this kit, it takes three minutes, and it is the thing
most often skipped.

See [docs/3-measuring-credits.md](docs/3-measuring-credits.md).

---

## What's in here

```
README.md                      You are here
FACILITATOR.md                 Run of show, timing, Plan A/B, full-day format
docs/
  0-admin-setup.md             ⚠️ Enterprise policies, EMU, network — do this first
  1-attendee-setup.md          Laptop prerequisites for participants
  2-hands-on.md                The 25-minute hands-on block, step by step
  3-measuring-credits.md       How to read what a session actually cost
  4-token-optimization.md      Ten levers for getting more outcome per credit
  5-model-migration.md         MAI-Code-1-Flash → 1.1-Flash, and how to find hard-coded IDs
  6-copilot-app-tour.md        Demo script for the app: agents, skills, plugins, canvases
```

---

## Licence & attribution

This kit is MIT licensed — see [LICENSE](LICENSE).

The official workshop it links to is
[`github-samples/copilot-workshops`](https://github.com/github-samples/copilot-workshops),
© GitHub, also MIT. The lab application is
[`github-samples/tailspin-toys`](https://github.com/github-samples/tailspin-toys).
If you fork or re-host either, retain their licence files. The simplest and safest approach
is to **link to the official site rather than re-host it**.

Figures in this kit reflect publicly documented GitHub behaviour at the time of writing.
Billing mechanics change — always confirm current values against
[GitHub Docs](https://docs.github.com/copilot) before quoting numbers to a room.
