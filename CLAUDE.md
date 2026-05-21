# CLAUDE.md — CartierOS Proposal System

## Project Overview

AI-powered sales proposal generator. Before a prospect gets on a demo call, this system pulls live business data (Google rating, review count, domain status), feeds it to Claude, and outputs a personalized PDF proposal that looks like a $5,000 agency deliverable — generated in minutes.

This repo is part of the larger CartierOS ecosystem and is triggered through the Jarvis Agent Core.

---

## Repository Structure

```
cartier-proposal-system/
├── README.md                  # Public-facing project description
├── roofing-one-pager.html     # Niche landing/sales page for roofing operators
└── CLAUDE.md                  # This file
```

This is a lean repo. The actual generation logic lives in the n8n workflow and the Claude API prompt layer — not in code files here. This repo serves as the documentation hub and niche asset store for the proposal system.

---

## Tech Stack

| Layer | Tool |
|---|---|
| AI Writing | Claude API (Anthropic) — custom prompt per prospect |
| Data Ingestion | Atlas pipeline — Google Maps data (rating, reviews, domain) |
| Orchestration | n8n workflow — triggered manually or by Jarvis command |
| Output Format | PDF — professional branded layout |
| Delivery | Hermes email system or shared link pre-call |

---

## Proposal Architecture

Each proposal is built in five layers:

1. **Live Business Data** — Google rating, review count, domain status, industry, city, revenue-at-risk estimate
2. **Custom Narrative** — Problem section tied to their specific gaps, solution mapped to their industry, social proof
3. **30-Day Roadmap** — Days 1–2 onboarding → Days 3–5 website + lead system live → Days 7–30 optimization
4. **Tiered Pricing** — Foundation / CartierOS Core / Pro, framed around ROI
5. **Personalized CTA** — Close tied directly to the business name and identified pain

---

## Prompt Structure

```
System:  You are a senior sales strategist at CartierCreative...
Context: [business name], [industry], [city], [rating], [reviews],
         [domain status], [owner name if known]
Task:    Write a personalized growth proposal following this structure:
         [problem] → [gaps] → [solution] → [roadmap] → [pricing] → [CTA]
Tone:    Direct. Confident. Specific. Never generic.
```

**Tone rules**: No filler. No generic phrases. Every sentence should reference something specific about that prospect's business. Avoid: "in today's digital landscape", "we understand your challenges", "take your business to the next level".

---

## Niche Assets

The repo stores niche-specific sales pages and one-pagers as HTML files:

- `roofing-one-pager.html` — Roofing operator niche page

**Convention for new niche files**: `[industry]-one-pager.html` (e.g., `plumbing-one-pager.html`, `hvac-one-pager.html`). Keep each file self-contained (inline CSS, no external dependencies) so it can be emailed or linked directly.

---

## Development Workflows

### Adding a New Niche One-Pager

1. Copy the closest existing niche HTML file as a starting point
2. Replace industry-specific copy, pain points, and social proof
3. Keep the pricing section consistent with the current tier structure
4. Name the file `[industry]-one-pager.html`
5. Commit with message: `Add [industry] niche one-pager`

### Updating the Proposal Prompt

The Claude prompt lives in the n8n workflow (not in this repo). Document any prompt changes in a commit message or PR description that references the specific prospect feedback or conversion data that motivated the change.

### Tracking Active Proposals

The active proposals table in `README.md` is the source of truth for pipeline status. Update it when:
- A proposal is sent (add row with ⏳)
- A demo is booked (update to ⏳ Demo complete — pending close)
- A deal closes (update to ✅ Closed — active client)
- A deal is lost (update to ❌ with brief reason)

---

## Integration Points

- **CartierOS**: This system feeds into the main [CartierOS](https://github.com/cartiercreative8-art/cartier-os) deployment pipeline
- **Jarvis Agent Core**: Proposals are triggered via [Jarvis](https://github.com/cartiercreative8-art/jarvis-agent-core) — either by manual command or automated trigger
- **Atlas Pipeline**: Data ingestion is upstream of this system; Atlas handles all Google Maps scraping and normalization before the proposal prompt receives it

---

## Key Conventions for AI Assistants

- **Do not genericize** copy. Every piece of text added to niche pages or prompt templates must be specific and actionable.
- **Do not add dependencies** to HTML one-pagers. They must remain self-contained single-file deliverables.
- **Do not fabricate data** in example proposals or README tables. Use only real prospect outcomes.
- **Pricing tiers** (Foundation / CartierOS Core / Pro) must remain consistent across all niche assets and proposal templates.
- **Commit scope**: One niche asset or one logical change per commit. Don't bundle unrelated niche pages.
- **Branch**: Develop on feature branches; merge to `main` only when output is ready to send or deploy.
