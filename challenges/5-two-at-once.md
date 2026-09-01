# ⚡ Challenge 5 — Two At Once

> **25 points · ~15 minutes · 🔥 Hard**

**Run two agents on two issues at the same time. Then combine their work.**

---

## The idea

This is the challenge that changes how people think about the tool.

One agent working while you watch is a faster autocomplete. **Three agents working while you
review the first one's output is a different job.** You stop being the person typing and start
being the person deciding.

Then you hit the real problem: two agents, two branches, overlapping work. **Agent Merge**
exists for exactly that.

---

## Do it

### 1. Pick two issues that don't fight (2 min)

Choose **two independent** issues from the backlog. Ideally they touch different areas.

> 💡 **Or, if you're feeling brave:** pick two issues that *do* overlap. It's a harder demo
> and a much more interesting one — real teams have this problem constantly.

### 2. Start both (2 min)

Launch a session for issue A. **Don't wait for it.** Launch a session for issue B.

Pause and notice what just happened: you have two engineers working and you are supervising
both.

### 3. Supervise, don't spectate (6 min)

While they run, do the job that's actually yours:

- 👀 Review A's diff as soon as it's ready — don't wait for both
- 🛑 Stop whichever one is flailing and re-prompt it with tighter scope
- 🔀 Notice if they're heading for the same file

> ⏱️ **Two confused agents burn twice as fast.** The supervision is not optional — the whole
> value here is catching the wrong one early.

### 4. Bring the work together (5 min)

Now combine them. Depending on what happened:

- **No overlap?** Merge both PRs. Easy, and still a valid result.
- **They touched the same files?** Use **Agent Merge** — see
  [Lesson 6](https://github-samples.github.io/copilot-workshops/app/6-agent-merge/) — and let
  the agent reconcile the two branches rather than resolving conflicts by hand.
- **One went badly wrong?** Say so at demo time. That's Best Failure material and it scores.

---

## ✅ Scoring

| | Points |
|---|---|
| Two parallel sessions, both producing reviewable work, both merged | **25** |
| Two sessions run, one useful result | 15 |
| Two started, chaos ensued, you can explain why | 10 |

### 🌟 Bonus

| | Points |
|---|---|
| You used **Agent Merge** to reconcile a real conflict | **+10** |
| You stopped one mid-flight and can explain the signal that told you to | **+5** |
| Three or more in parallel, and you still knew what was going on | **+5** |

---

## 🎬 Demo tip

**Show the screen with both sessions running.** It's the most visually convincing thing
anyone will demo today — much more persuasive than a finished diff, because it shows the
change in *your* role, not the tool's.

---

## ⚠️ Honest note

Parallel agents multiply your throughput *and* your review burden. Two PRs you don't
understand is worse than one you do.

The skill isn't launching lots of sessions. **It's knowing which one to kill.**

---

**Next →** [Not A Diff](6-not-a-diff.md) · [Give It Eyes](4-give-it-eyes.md) · [the board](../README.md#the-board)

*Adapted from [Lesson 6](https://github-samples.github.io/copilot-workshops/app/6-agent-merge/).*
