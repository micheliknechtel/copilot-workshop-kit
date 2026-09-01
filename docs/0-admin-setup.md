# 0 — Admin setup ⚠️ blocking

**Audience:** enterprise owner or Copilot administrator
**When:** at least one week before the session
**Time needed:** about 30 minutes, plus one dry run

If these items are not done, the session cannot run. There is no workaround on the day.

---

## 1. Enable the two client policies 🚨

The Copilot app is a desktop application built on Copilot CLI. On **Copilot Business** and
**Copilot Enterprise**, administrators control which Copilot clients users may run.

**These are two separate switches.** GitHub's documentation is explicit:

> "Disabling Copilot CLI does not disable the GitHub Copilot app. The app is governed by its
> own policy."

So check **both**:

1. Go to your enterprise → **AI controls**
2. In the sidebar, click **Copilot**
3. Under "Features & clients," click **Configure features & clients**
4. In the **Clients** section, confirm:
   - [ ] **GitHub Copilot app** — enabled
   - [ ] **Copilot CLI** — enabled

### Gotchas

- **"Let organizations decide" is not the same as enabled.** If the enterprise policy is set
  to delegate, the client must be enabled in at least one organization that grants the user
  their Copilot licence. Setting **Enabled everywhere** at enterprise level is the reliable option.
- **"Enabled/Disabled everywhere" overrides all organization settings.**
- Users need an **assigned Copilot seat**, not just enterprise membership.
- If you want `/delegate` to the Copilot cloud agent to work, **both** the Copilot CLI policy
  **and** the Copilot cloud agent policy must be enabled.

📖 [Administering Copilot CLI for your enterprise](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/copilot-cli/administer-copilot-cli-for-your-enterprise)

---

## 2. Enable a spread of models

The hands-on exercises compare cost and quality across model tiers. Under the same
**AI controls → Copilot** area, ensure the model policy enables at minimum:

- [ ] A **small/fast** model (e.g. MAI-Code-1.1-Flash, Haiku-class)
- [ ] A **mid-tier** model
- [ ] One **frontier** model
- [ ] **Auto model selection**, if available

Without at least two tiers, [docs/4-token-optimization.md](4-token-optimization.md)'s
central exercise cannot run.

---

## 3. Enterprise Managed Users (EMU) — run a dry run 🚨

**Skip this section only if you are certain you are not an EMU enterprise.**

Managed user accounts are significantly restricted on GitHub.com:

> "Managed user accounts can contribute only to private and internal repositories within
> their enterprise and their own private repositories. On GitHub.com, they have **read-only
> access** to the wider GitHub community."

> "Managed user accounts **cannot create public content** or collaborate outside your enterprise."

The workshop asks attendees to create their own copy of a **public** template repository
(`github-samples/tailspin-toys`) using **Use this template**.

**Do not assume this works.** Have **one EMU user attempt it end to end at least a week
ahead**, creating the copy into an org **owned by your enterprise** (not a personal namespace).

**If it is blocked**, the fallback is straightforward:

1. A non-EMU user creates one copy from the template
2. Mirror or import that repository into an org inside your enterprise
3. Attendees copy or fork from **that internal repository** instead

Either way, **decide the exact target org name in advance** and put it in the invitation.
"Create it wherever" reliably produces twenty people in twenty wrong places.

📖 [Abilities and restrictions of managed user accounts](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/understanding-iam-for-enterprises/abilities-and-restrictions-of-managed-user-accounts)

---

## 4. Budgets — don't let a hard stop end the session

If your organisation sets Copilot **budgets** with a *prevent further usage* action, an
intensive hands-on day can reach them. When a hard cap triggers, agentic features stop
immediately, mid-task, with no grace period.

- [ ] Check current budgets at **enterprise** and **per-user** level
- [ ] Confirm nobody is already near their cap
- [ ] For a full-day event, **temporarily raise or soften** the per-user caps
- [ ] Have an admin reachable during the session

### General recommendation, beyond this workshop

A hard cap at **enterprise** level is an outage, not a cost control — one team's spike stops
every developer. Prefer:

- **Enterprise level:** alerting, so you get visibility
- **Per-user level:** hard caps, where the blast radius is one person

---

## 5. Network access

Corporate proxies block workshop steps in predictable places.

- [ ] Copilot endpoints reachable — see the
      [Copilot allowlist reference](https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/copilot-allowlist-reference)
- [ ] `github.com` and `raw.githubusercontent.com` reachable
- [ ] **npm registry reachable** — the Playwright MCP lesson downloads at runtime via `npx`
- [ ] Custom CA certificates installed if you TLS-inspect
- [ ] A network contact available **during** the session

---

## 6. Developer tooling on managed laptops

The lab application is a Node.js project and the agent runs its test suite locally.

- [ ] **Node.js 22 or newer**
- [ ] **git**

On locked-down corporate laptops, installing a developer runtime often requires a request
ticket. **Start this early — it is the most common cause of a wasted first hour.**

Alternative: the lab repo ships a **dev container**, which bundles Node — but that requires
Docker, which may be equally restricted. Verify one of the two paths works.

---

## Final admin sign-off

- [ ] Copilot app policy enabled
- [ ] Copilot CLI policy enabled
- [ ] Model policy spans at least two tiers
- [ ] EMU template dry run completed (or fallback repo prepared)
- [ ] Target org name decided and communicated
- [ ] Budgets checked and softened if needed
- [ ] Network paths verified, including npm
- [ ] Node.js 22+ and git confirmed installable

**One person should own this list and confirm it in writing.** Shared ownership of a
pre-flight checklist means no ownership.
