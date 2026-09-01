# 👁️ Challenge 4 — Give It Eyes

> **25 points · ~15 minutes · 🔥 Hard**

**Connect a real browser to the agent so it can load your app, click things, and see what it
broke.**

---

## The idea

Everything so far, the agent did blind. It changed code, ran tests, and inferred the rest.

**MCP servers** connect the agent to systems outside the repository. The Playwright MCP server
gives it a real browser — so it can load your running app, interact with it, take screenshots,
and check its own work the way you would.

The moment it goes from *"tests pass"* to *"I loaded the page and the button works"* is the
moment this stops feeling like autocomplete.

---

## ⚠️ Read this first

This challenge **downloads Playwright at runtime via `npx`**. On a corporate network that is
the single most likely thing to fail today.

**Try it for 3 minutes. If npm is blocked, stop and pick another challenge.** Do not spend
your hackathon debugging a proxy — you'll get no points and no fun. Tell a facilitator and
move on; "we tried and the network blocked it" is a legitimate finding worth reporting at
demo time.

---

## Do it

### 1. Get the app running (3 min)

```bash
npm run dev
```

Note the URL it prints — usually `http://localhost:4321`. Load it in your own browser and
confirm it works. **The agent can't see a site that isn't up.**

### 2. Add the Playwright MCP server (4 min)

Follow [Lesson 5](https://github-samples.github.io/copilot-workshops/app/5-playwright-mcp/)
for the current configuration.

Confirm the agent can see the new tools before you go further. If it can't, no amount of
prompting will help.

### 3. Give it something visual to do (6 min)

Now use the eyes. Good tasks:

- 🐛 **Find a UI bug** — *"Load the site, go to the products page, and check the cart total
  updates when I change quantity. Tell me what you see."*
- 📸 **Verify your own fix** — take a fix from Challenge 1 and have it confirm the fix in the
  browser, not just in tests
- ♿ **Accessibility pass** — *"Load the homepage and list anything a screen reader user would
  struggle with."*

> 💡 **The best prompts here ask it to look and report, not to fix.** Get it observing
> accurately before you get it changing things.

### 4. Close the loop (2 min)

The full circle: **it finds the bug in the browser → fixes the code → reloads the page →
confirms the fix.** If you get that, you've got the demo of the day.

---

## ✅ Scoring

| | Points |
|---|---|
| Agent browses the running app and reports something true about it | **25** |
| MCP connected, agent can see the tools, no useful task completed | 12 |
| Genuine attempt, blocked by network — say so clearly at demo | 8 |

### 🌟 Bonus

| | Points |
|---|---|
| It found a UI issue you didn't already know about | **+10** |
| Full loop: found → fixed → verified in the browser | **+10** |
| Screenshot in the PR description | **+5** |

---

## 🆘 Troubleshooting

| Symptom | Try |
|---|---|
| `npx` hangs or fails | Corporate proxy. Stop, pick another challenge. |
| Agent can't see the browser tools | Restart the app after config change |
| Browser opens, page blank | Is `npm run dev` still running? Right port? |
| Times out loading | It may be using the wrong localhost port — say it explicitly |

---

**Next →** [Two At Once](5-two-at-once.md) · [Not A Diff](6-not-a-diff.md) · [the board](../README.md#the-board)

*Adapted from [Lesson 5](https://github-samples.github.io/copilot-workshops/app/5-playwright-mcp/).*
