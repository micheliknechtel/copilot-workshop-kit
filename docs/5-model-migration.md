# 5 — Model migration: MAI-Code-1-Flash → 1.1-Flash

Everything in this document is publicly announced. Sources are linked.

---

## What's happening

| | |
|---|---|
| **MAI-Code-1-Flash** | Generally available June 2026 · **deprecated 10 September 2026** |
| **MAI-Code-1.1-Flash** | Launched **11 August 2026** · available on all paid Copilot plans |

📖 [Upcoming deprecation of MAI-Code-1-Flash](https://github.blog/changelog/2026-08-11-upcoming-deprecation-of-mai-code-1-flash/)

---

## What 1.1-Flash improves

- **Native vision** — it can work with images directly, so screenshots, mockups, and diagrams
  become usable input
- **Stronger coding performance** compared to 1-Flash
- **Better instruction following** — it stays inside the scope you gave it more reliably,
  which matters more for cost than it might first appear
- **Better tool use** — fewer wasted turns in agentic sessions
- **Lower cost per token** than the model it replaces

That combination is unusual and worth stating plainly: **it is both better and cheaper.**
This is not a migration you have to be talked into.

> 💡 The instruction-following improvement has a direct cost consequence. A model that
> respects "change only these two files" produces smaller diffs, fewer correction rounds, and
> less review burden. Quality improvements at the fast end of the range tend to show up on
> the bill as well as in the code.

---

## What you actually have to do

For nearly everyone: **choose the new model in the picker.** That's it.

There is no SDK to upgrade, no configuration format change, no integration work.

---

## Where it can bite: hard-coded model identifiers

The one genuine migration risk is **model IDs written down somewhere** — in code, config, or
automation that will keep requesting a model that is going away.

Common places to check:

| Location | What to look for |
|---|---|
| `.github/workflows/` | Model IDs in agentic or Copilot-related workflow steps |
| Prompt files and skills | Pinned model in frontmatter |
| Internal tooling / scripts | Anything calling a model API with a literal string |
| Documentation and runbooks | Instructions telling people to pick a specific model |
| Team templates | Defaults copied repo to repo, which spread silently |

### Finding them

Across a large estate, a code search is the fastest first pass:

```
org:<your-org> "mai-code-1-flash"
```

Then narrow by file type:

```
org:<your-org> "mai-code-1-flash" path:.github/workflows
org:<your-org> "mai-code-1-flash" extension:yml
org:<your-org> "mai-code-1-flash" extension:json
```

> 🤖 **This is an excellent agent task** — and a good demo. It's mechanical, well-specified,
> spread across many repositories, and easy to verify. Exactly the shape of work to hand to
> the coding agent rather than doing by hand.

---

## A sensible migration checklist

- [ ] **Search the estate** for hard-coded `mai-code-1-flash` references
- [ ] **Triage**: which are live automation, which are stale documentation?
- [ ] **Update workflows and automation first** — these fail silently and at the worst moment
- [ ] **Update prompt files, skills, and templates**
- [ ] **Update documentation and runbooks** so the next person doesn't reintroduce it
- [ ] **Check enterprise model policy** allows 1.1-Flash for the relevant users
- [ ] **Tell your developers** — one message, before the deprecation date, not after
- [ ] **Re-run the search** to confirm you're clean

---

## Talking to your developers about it

Keep it short. Something like:

> MAI-Code-1-Flash is being retired on 10 September. Its replacement, MAI-Code-1.1-Flash,
> is already available — it's better at coding, follows instructions more closely, handles
> images, and costs less per token. Switch in the model picker. If you've pinned the old
> model anywhere in a workflow or prompt file, update it before the date.

---

## Beyond this migration

Two habits make the next model transition much less work than this one:

1. **Don't pin model IDs unless you have a specific reason.** Prefer the picker default or
   auto model selection. Pinning is a commitment to maintain something.
2. **Keep a single place that records where models *are* pinned**, when you must pin. The
   expensive part of a migration is never the change — it's the search.
