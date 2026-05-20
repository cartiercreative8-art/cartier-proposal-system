# CartierOS Proposal System — AI Sales Automation

> AI-generated, prospect-personalized sales proposals. Pulls live business data per target, writes a custom narrative, and outputs a professional PDF. Built to close deals.

---

## What It Is

Before a prospect gets on a demo call, they receive a custom-built proposal with their business name, real data pulled from Google, a revenue-at-risk calculation, and a tailored 30-day roadmap.

This is not a template with a name swapped in. Every proposal is built around that specific business — their rating, their review count, their domain status, their gaps. It looks like a $5,000 agency deliverable. It's generated in minutes.

---

## What Goes Into Each Proposal

```
1. LIVE BUSINESS DATA
   └ Google rating + review count (pulled via Atlas)
   └ Domain status (active / expired / none)
   └ Industry + service area
   └ Revenue-at-risk estimate (missed leads × avg job value)

2. CUSTOM NARRATIVE
   └ Problem section: written around their specific gaps
   └ Solution section: mapped to their industry and pain points
   └ Social proof: relevant case studies and results

3. 30-DAY ROADMAP
   └ Days 1–2: Onboarding
   └ Days 3–5: Website + lead system live
   └ Days 7–30: Optimization + monitoring

4. PRICING
   └ Tiered options (Foundation / CartierOS Core / Pro)
   └ ROI framing: one missed job pays for the full year

5. CALL TO ACTION
   └ Personalized close tied to their business name
```

---

## Example Output

**Prospect:** DeWalt Plumbing Services — Colorado Springs, CO  
**Data pulled:** 4.2★ · 6 reviews · No website  
**Revenue-at-risk:** $10K+ per missed lead estimated  
**Proposal generated:** ~3 minutes  
**Outcome:** Demo booked same day — pending close

---

## Tech Stack

- **AI Writing:** Claude API (Anthropic) — custom prompt per prospect
- **Data Source:** Atlas pipeline — Google Maps data
- **Output:** PDF (professional branded layout)
- **Delivery:** Email via Hermes · or shared link pre-call
- **Orchestration:** n8n workflow — triggered manually or by Jarvis command

---

## Prompt Architecture

The proposal prompt is structured in layers:

```
System:  You are a senior sales strategist at CartierCreative...
Context: [business name], [industry], [city], [rating], [reviews],
         [domain status], [owner name if known]
Task:    Write a personalized growth proposal following this structure:
         [problem] → [gaps] → [solution] → [roadmap] → [pricing] → [CTA]
Tone:    Direct. Confident. Specific. Never generic.
```

---

## Active Proposals Sent

| Prospect | Industry | Outcome |
|---|---|---|
| Jeremy Halladay — Measure Once Handyman | Handyman | ✅ Closed — active client |
| Joe Castro — Super Handyman Co. | Handyman | System built, partners declined |
| Paul DeWalt — DeWalt Plumbing Services | Plumbing | ⏳ Demo complete — pending close |

---

## Part of CartierOS

The proposal system feeds into the full [CartierOS](https://github.com/cartiercreative8-art/cartier-os) deployment pipeline and is triggered through [Jarvis Agent Core](https://github.com/cartiercreative8-art/jarvis-agent-core).
