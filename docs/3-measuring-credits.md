# 3 — Measuring what a session costs

Cost is usually something finance mentions to engineering after the fact. This document is
about closing that loop to about three minutes, so the person who spent it is the person who
sees it.

---

## How Copilot billing works

Since **1 June 2026**, agentic Copilot features are billed in **credits**, in addition to
per-seat licensing.

| | |
|---|---|
| **1 credit** | $0.01 USD |
| **Copilot Business** | 1,900 credits per user per month included |
| **Copilot Enterprise** | 3,900 credits per user per month included |
| **Pooling** | Included credits pool across the organisation |
| **Rollover** | None — unused credits expire monthly |
| **Overage** | Billed at $0.01/credit, if a budget permits it |

### What is *not* billed 🎉

**Code completions and next edit suggestions are not billed as credits.**

This matters more than anything else in this document. The everyday inline experience — the
thing most developers use most of the time — is covered by the seat. Credits are consumed by
**agentic** work: agent sessions, coding agent, code review, Spaces, and similar.

So the practical framing is not "Copilot costs more now." It is:

> **Completions are flat-rate. Agents are metered. Learn which one a task deserves.**

### Promotional allowances

Higher promotional allowances (3,000 for Business, 7,000 for Enterprise) applied to existing
customers during an introductory period that **ended on 1 September 2026**. If your
consumption baseline was set during that window, your effective included capacity has since
reduced. Check whether your planning assumptions still hold.

📖 [About billing for GitHub Copilot](https://docs.github.com/en/copilot/concepts/billing)
· [Requests and credits](https://docs.github.com/en/copilot/concepts/billing/copilot-requests)

---

## Where to look

**As an individual:**

Settings → **Billing and licensing** → **Usage**. Filter to Copilot, narrow the date range to
today, and you'll see your own consumption.

**As an administrator:**

Enterprise or organisation → **Billing and licensing** → **Usage**. From here you can:

- Break consumption down by product and by user
- Export detailed usage as CSV for your own analysis
- Set **budgets** with alerting or hard-stop actions

📖 [Viewing your Copilot usage](https://docs.github.com/en/copilot/how-tos/manage-and-track-spending/monitor-premium-requests)

---

## The check-in ritual

Run this at the end of every hands-on block. It takes three minutes.

1. Everyone opens their own usage view
2. Everyone filters to **today**
3. Everyone says their number out loud
4. Ask the two questions:
   - **What did the cheapest person do differently?**
   - **Was the most expensive result actually better?**

The spread across a room doing the same task is routinely **5× or more**. That gap is the
entire lesson, and it lands far harder coming from the person sitting two seats away than
from a slide.

---

## Budgets: alerting versus hard stops ⚠️

Budgets can either **notify** or **prevent further usage**. The difference is significant and
often misunderstood.

A hard stop at **enterprise** level means one team's unusual week can halt agentic Copilot
for every developer in the company, instantly, mid-task, with no grace period. That is an
availability incident wearing a cost-control costume.

**A more defensible pattern:**

| Level | Action | Why |
|---|---|---|
| **Enterprise** | Alert | You want visibility, not an outage |
| **Organisation** | Alert | Find the team that changed behaviour |
| **Per user** | Hard cap | Blast radius is one person, and they can ask for more |

Set the per-user cap somewhere a normal heavy week won't reach — then anyone who does hit it
has genuinely unusual usage, which is exactly the conversation you wanted to have.

📖 [Managing your budget](https://docs.github.com/en/billing/tutorials/set-up-budgets)

---

## Establishing your own baseline

Before optimising anything, spend a week measuring. Four questions worth answering with your
own CSV export:

1. **What is our actual monthly consumption**, and is it trending up, flat, or down?
2. **How is it distributed?** Typically a small number of users drive most consumption —
   find out whether those are power users delivering value or scripts left running.
3. **Which features consume it?** Agent sessions, coding agent, and code review have
   different profiles.
4. **How does it map to output?** Credits per merged PR is crude, but it's a start, and it's
   far better than credits with no denominator at all.

> ⚠️ **Watch the units.** Confirm whether a figure you've been handed is a **single month**
> or **cumulative since billing began**. The conclusion inverts completely depending on the
> answer, and it is very easy to get wrong. Ask before you act.
