# 🛡️ ADMIN.md — for the Copilot administrator

**Send this to a named enterprise owner one week before the hackathon.**

Three items. The first is genuinely blocking — without it, nobody can take part and there is
no workaround on the day.

---

## 1. 🚨 Enable both client policies — blocking

The Copilot app is a desktop client, and administrators control which Copilot clients users
may run. **There are two separate switches**, and GitHub's docs are explicit that one does not
imply the other:

> "Disabling Copilot CLI does not disable the GitHub Copilot app. The app is governed by its
> own policy."

**Enterprise → AI controls → Copilot → Configure features & clients → Clients:**

- [ ] **GitHub Copilot app** — enabled
- [ ] **Copilot CLI** — enabled

### Watch out for

- **"Let organizations decide" is not "enabled."** If the enterprise delegates, the client
  must be on in the org that grants the user their Copilot seat. Setting **Enabled everywhere**
  at enterprise level is the reliable option.
- Users need an **assigned seat**, not just enterprise membership.
- For `/delegate` to the cloud coding agent, the **Copilot cloud agent** policy must be on too.

📖 [Administering Copilot CLI for your enterprise](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/copilot-cli/administer-copilot-cli-for-your-enterprise)

---

## 2. Allow a spread of models

Several challenges compare results across model tiers. Under the same **AI controls → Copilot**
area, please enable at minimum:

- [ ] One **small / fast** model
- [ ] One **mid-tier** model
- [ ] One **frontier** model
- [ ] **Auto model selection**, if available

---

## 3. Enterprise Managed Users — please dry-run this 🚨

*Skip if you're certain you aren't an EMU enterprise.*

Managed user accounts are restricted on GitHub.com:

> "Managed user accounts can contribute only to private and internal repositories within
> their enterprise and their own private repositories. On GitHub.com, they have **read-only
> access** to the wider GitHub community."

Attendees are asked to create their own copy of a **public** template
(`github-samples/tailspin-toys`) via **Use this template**.

**Please have one EMU user try this end to end, a week ahead**, targeting an org owned by your
enterprise.

**If it's blocked**, the fallback is simple:

1. A non-EMU user creates one copy from the template
2. Mirror or import it into an org inside your enterprise
3. Attendees copy from **that internal repo** instead

Either way: **decide the exact target org in advance** and tell us the name, so it goes in the
invitation. "Create it anywhere" reliably produces twenty repos in twenty wrong places.

📖 [Abilities and restrictions of managed user accounts](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/understanding-iam-for-enterprises/abilities-and-restrictions-of-managed-user-accounts)

---

## 4. Budgets — avoid a mid-session hard stop

If Copilot budgets are set to **prevent further usage**, an intensive hands-on session can
reach them. When a hard cap triggers, agentic features stop instantly, mid-task, with no
grace period.

- [ ] Check current enterprise and per-user budgets
- [ ] Confirm nobody's already close
- [ ] Consider temporarily softening per-user caps for the day
- [ ] Be reachable during the session

> 💡 **Worth considering beyond this event:** a hard cap at *enterprise* level is an outage
> wearing a cost-control costume — one team's spike stops every developer. A more defensible
> posture is **alerting at enterprise level, hard caps per user**, where the blast radius is
> one person who can simply ask for more.

📖 [Managing your budget](https://docs.github.com/en/billing/tutorials/set-up-budgets)

---

## 5. Network

Corporate proxies break this in predictable places:

- [ ] Copilot endpoints reachable —
      [allowlist reference](https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/copilot-allowlist-reference)
- [ ] `github.com` and `raw.githubusercontent.com` reachable
- [ ] **npm registry reachable** — one challenge downloads Playwright at runtime via `npx`
- [ ] Custom CA certificates installed if you TLS-inspect

---

## 6. Developer tooling on laptops

The lab app is a Node project and the agent runs its tests locally.

- [ ] **Node.js 22+** and **git** installable by attendees

On locked-down laptops this often needs a ticket. **Start early — it's the most common cause
of a wasted first half hour.** (Docker + the repo's dev container is an alternative, if that's
easier in your environment.)

---

## ✅ Sign-off

- [ ] Copilot app policy on
- [ ] Copilot CLI policy on
- [ ] Model policy spans at least two tiers
- [ ] EMU template dry run done, or fallback repo prepared
- [ ] Target org name confirmed: `________________________`
- [ ] Budgets checked
- [ ] Network verified, including npm
- [ ] Node 22+ and git available

**Please confirm in writing.** Shared ownership of a pre-flight checklist means no ownership.
