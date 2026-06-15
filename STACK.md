# STACK.md — How the pieces fit

This is the architecture, not the code. No keys, no customer data, no employee names. If you run a small business and you're wondering what a serious Claude Code setup actually looks like under the hood, this is it.

## The shape of it

Everything runs from one workstation plus a handful of cloud workers. There is no agency, no dev team, no platform subscription doing the heavy lifting. It is Claude Code, a pile of skills, a file-based memory system, and direct API access to the tools my business already pays for.

```
        Claude Code (the operator)
                  |
   orchestrator + skills + file memory
                  |
   +------+-------+--------+---------+
   |      |       |        |         |
 Market  Ops    Sales   Finance   Content
   |      |       |        |         |
  Ad     HCP    Phone   Accounting  Blog
  APIs   API   + booking  pipeline  Podcast
  WP     KPI    agent     (6 agents) Shorts
  SEO    dash                        Social
```

## Foundation

- **Claude Code** is the operator. I talk to it like a chief of staff. It reads, decides, edits, ships, and reports.
- **Skills** are the muscle. Each repeatable job (audit ads, write a blog post, publish a podcast, run the books) is a skill it loads on demand. Most came from upstream authors (see [SKILLS.md](./SKILLS.md)); the HVAC-specific ones I built.
- **File-based memory** is the spine. Durable facts, decisions, pricing rules, and playbooks live in plain markdown so nothing important dies when a session ends. The rule is simple: if it should outlive the conversation, it gets written down.
- **An orchestrator** drives WordPress and the heavier batch jobs so a single instruction can fan out across hundreds of pages.

## Marketing layer

- **Google Ads + Meta** run through the official APIs, not screenshots. Audits, bidding fixes, negative-keyword hygiene, and budget moves happen programmatically against live data.
- **WordPress** is edited through the REST API. Meta descriptions, schema, FAQ accordions, internal links, and content all ship without touching the admin UI.
- **SEO + GEO.** Traditional SEO plus answer-engine optimization, because more of my customers ask an AI before they call. Owned crawler for site audits, owned AI-citation tracker for visibility.
- **Content + social + podcast** all generate in one consistent voice so the brand sounds like me everywhere.

## Operations layer

- **Housecall Pro** is the system of record for the field: customers, jobs, estimates, invoices. Both the public API and the private API are wired, with the gotchas documented so a UI change does not silently break a pipeline.
- **Dispatch, tech feedback, and KPI reporting** run on top of that data. Daily and weekly reports land without anyone pulling them.
- **Cloud workers** (Cloudflare) handle the always-on jobs: webhooks, conversion bridges, snapshot builders, and the KPI proxy that feeds the dashboards.

## Sales layer

- **AI booking.** A customer can talk to an AI on the site, and a confirmed booking writes straight into Housecall Pro: customer, job, appointment, confirmation. Direct API, not a widget handoff.
- **DaveAI** is the overflow phone agent for the calls my crew cannot get to. HVAC-specific intent routing, in my voice, with the pricing rules baked in.
- **Follow-up.** Estimates and leads get worked automatically, with the human handoffs kept human on purpose.

## Finance layer

- **A 6-agent accounting pipeline:** data prep, categorize, reconcile, report, insights, tax prep. Built around Housecall Pro being the authoritative ledger, because for a service business the field data is the truth, not the bookkeeping software.
- It produces a reconciled picture, an insights report, and a CPA-ready handoff packet.

## HVAC-specific layer

This is the part no upstream skill could give me, because it only matters if you run an HVAC shop:

- **Pricing engine** across Trane, Mitsubishi, RunTru, and ACiQ, plus extended-warranty math and the Oklahoma utility-rebate stack.
- **Quote system** that builds real estimates with correct line items.
- **Refrigerant logic** for the R-454B and R-32 transition.
- **Rebate routing** by ZIP and utility, because the same town can sit in two different rebate programs.

## Principles I built on

- **Build, do not rent.** Where a SaaS wanted a monthly fee for something Claude Code could do against an API I already pay for, I built it.
- **One source of truth.** The field system (Housecall Pro) is the ledger. Everything reconciles back to it.
- **Memory over cleverness.** A decision written down once beats re-deriving it every session.
- **One voice everywhere.** Site, ads, social, podcast, phone agent. It all sounds like me because the brand voice is a rule, not a vibe.
- **Humans stay human.** AI drives demand and removes busywork. People close the jobs and answer the hard calls.

## What is deliberately not here

Keys, tokens, customer records, employee compensation, the live worker code, and anything that would expose my crew or my customers. This repo is the blueprint and the receipts. It is not a turnkey clone of my business, and the HVAC layer is tuned for Hartzell's, not for yours.
