# 6 — Copilot app tour (demo script)

**Duration:** 15 minutes
**Audience:** the room, watching you
**Goal:** by the end, everyone understands what the app is, when to reach for it, and what
each capability costs them.

Full reference: [GitHub Copilot app documentation](https://docs.github.com/copilot)

---

## Before you start ✅

- [ ] Copilot app open, signed in, **on a projector-legible font size**
- [ ] A repository loaded that you know well
- [ ] At least one session already run, in case live generation goes sideways
- [ ] Notifications, personal messages, and anything confidential **closed**
- [ ] Model picker visible

---

## 1. What the app is (2 min)

Frame it before you click anything:

> The Copilot app is a desktop application for working with coding agents. It's not the
> inline completion experience you already know from your editor — that keeps working exactly
> as it does. This is for the class of work where you want to hand over a whole task and
> review the result.

The concrete difference worth landing:

| In your editor | In the app |
|---|---|
| Assists you while you type | Works through a task while you do something else |
| You hold the context | The session holds the context |
| Not billed as credits | Billed as credits |
| Minutes | Minutes to hours |

---

## 2. Sessions and agents (4 min)

**Show, don't describe:**

1. Create a session against a real issue
2. Point at the model picker — *"this is the most expensive decision on this screen"*
3. Start it, and **narrate what it's doing** as it reads files

Things worth calling out as they happen:

- 🔍 **It explores before it edits.** That exploration is real cost, and a specific prompt
  shortens it.
- 🧪 **It runs the tests itself** and reacts to failures.
- 🛑 **You can stop it.** Demonstrate this deliberately — most people don't realise stopping
  is a legitimate, and often correct, move.

**Show parallel sessions.** Two or three tasks progressing at once is the moment the model
usually clicks for people — it stops being "faster autocomplete" and becomes "delegation."

---

## 3. Plan mode and Autopilot (3 min)

**Plan mode** — ask for an approach before any code is written. Review the plan, correct the
misunderstanding, *then* execute.

> Say this out loud: reviewing a plan takes a minute. Reviewing a wrong 400-line diff takes
> twenty — and you paid for the diff either way.

**Autopilot** — the agent proceeds through steps without stopping to ask. Powerful, and worth
being honest about: use it where you trust the scope and the tests, not where you're
exploring.

---

## 4. Skills and plugins (3 min)

**Skills** package a good prompt into something reusable and shareable.

The framing that lands:

> Someone on your team will write an excellent prompt for reviewing a service for security
> issues. Right now that prompt lives in their session history and dies there. Twenty other
> people will iterate their way to something similar, badly, at twenty separate costs. A
> skill is how one person's good work becomes everyone's default.

**Plugins and MCP servers** connect the agent to systems beyond the repository — issue
trackers, browsers, internal APIs.

If you demo the Playwright MCP server (workshop
[Lesson 5](https://github-samples.github.io/copilot-workshops/app/5-playwright-mcp/)),
**test it on the venue network first** — it downloads via `npx` at runtime and proxies block
it regularly.

---

## 5. Canvases (2 min)

Canvases are interactive side-panel surfaces — documents, spreadsheets, previews, browsers —
that the agent can create and edit alongside the conversation.

The point to make: **not all output is a diff.** Migration plans, inventories, comparison
tables, and architecture notes are legitimate outputs, and they're often the deliverable that
actually unblocks a decision.

---

## 6. Bringing it back to cost (1 min)

Close the demo on the through-line, not on features:

> Everything you just watched is metered. That's not a warning — completions are still flat
> rate and still free at the point of use. But the moment you delegate a task, you're
> spending, and the difference between spending well and spending badly is roughly five times.
>
> Three habits cover most of it: start on a small model and escalate, name the files you mean,
> and stop a run that's lost the plot.

Then move straight into [2-hands-on.md](2-hands-on.md).

---

## Questions you'll be asked

**"Does this replace the editor extension?"**
No. Different jobs. Completions stay where they are and stay unmetered.

**"Can it access our internal systems?"**
Through MCP servers and plugins, yes — subject to whatever authentication and network policy
you put in front of them.

**"How do we stop it doing something we don't want?"**
Repository custom instructions for guidance, branch protection and required reviews for
enforcement. **Agent output is a pull request; treat it exactly like any other pull request.**

**"What does a typical task cost?"**
Resist inventing a number. Say: *"That's what the next 25 minutes is for — you'll measure your
own."*

**"When is X coming?"**
If you don't have a public source, don't speculate. *"I can't commit to timing, but I can
find out and come back to you — and if you'd like early access to what's next, I can put your
name forward."*
