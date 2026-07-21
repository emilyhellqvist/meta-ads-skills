# Meta Ads Skills

**21 Meta Ads (Facebook & Instagram) optimization skills for AI agents.**

Connect your live Meta Ads data to Claude, Cursor, or any MCP-compatible agent — then install skills that give it deep optimization expertise. Ask natural language questions, get expert-level analysis back.

```
"Run a full account audit and tell me the top 5 things to fix."
"Which ad sets are spending money with zero conversions this month?"
"My CPA went up 40% this week — what happened?"
"Which audiences are overlapping and competing against each other in auction?"
```

---

## Quickstart

**Step 1 — Connect your Meta Ads account** (pick one):

| Connector | Best for | Time |
|-----------|----------|------|
| [Meta's official Ads MCP](setup/meta-ads-mcp.md) | No third-party cost, direct OAuth to your own account | 15–20 min |
| [Windsor MCP](setup/windsor-mcp.md) | Fastest setup, works if the official MCP isn't rolled out to you yet, 325+ platforms | 10–15 min |
| [Supermetrics MCP](setup/supermetrics-mcp.md) | Already on Supermetrics, 200+ platforms | 10–20 min |

New here? The **[Getting Started Guide](getting-started.md)** walks through each option, plus a dedicated section on keeping your ad account from getting flagged.

**Step 2 — Install the skills:**

```bash
npx skills add emilyhellqvist/meta-ads-skills
```

---

## Skills

All 21 skills are task and optimization focused — deep playbooks for doing specific jobs, not generic campaign overviews.

| Skill | What it does |
|-------|-------------|
| [`meta-ads-account-audit`](skills/meta-ads-account-audit/SKILL.md) | Full account audit, prioritize fixes by financial impact, first-30-days takeover plan |
| [`meta-ads-audience-targeting`](skills/meta-ads-audience-targeting/SKILL.md) | Audience research, Core/Custom/Lookalike strategy, intent mapping, audience architecture |
| [`meta-ads-exclusions`](skills/meta-ads-exclusions/SKILL.md) | Eliminate wasted spend, build exclusion audiences, prevent audience cannibalization |
| [`meta-ads-placement-mining`](skills/meta-ads-placement-mining/SKILL.md) | Mine placement & platform breakdowns (Feed, Reels, Stories, Audience Network) for efficiency wins |
| [`meta-ads-ad-copy`](skills/meta-ads-ad-copy/SKILL.md) | Write primary text, headlines, and descriptions — intent-matched frameworks by funnel stage |
| [`meta-ads-creative-formats`](skills/meta-ads-creative-formats/SKILL.md) | Format strategy (static, video, carousel, collection), CTA selection, format-to-placement fit |
| [`meta-ads-creative-fatigue`](skills/meta-ads-creative-fatigue/SKILL.md) | Detect creative fatigue (frequency, CTR decay, rising CPM), set refresh cadence |
| [`meta-ads-relevance-diagnostics`](skills/meta-ads-relevance-diagnostics/SKILL.md) | Diagnose Quality / Engagement / Conversion Rate Ranking, fix root causes, reduce CPMs |
| [`meta-ads-bidding`](skills/meta-ads-bidding/SKILL.md) | Lowest Cost, Cost Cap, Bid Cap, ROAS goal — when to use each, portfolio bid strategy |
| [`meta-ads-budget-pacing`](skills/meta-ads-budget-pacing/SKILL.md) | CBO vs ABO, budget pacing, fixing under/overspend |
| [`meta-ads-audiences`](skills/meta-ads-audiences/SKILL.md) | Custom Audiences, Lookalikes, Advantage+ audience, exclusions |
| [`meta-ads-segmentation`](skills/meta-ads-segmentation/SKILL.md) | Device, placement, demo, and day-of-week analysis — bid and budget splits |
| [`meta-ads-attribution`](skills/meta-ads-attribution/SKILL.md) | Attribution windows, Conversions API vs Pixel, iOS 14.5+ modeled conversions |
| [`meta-ads-conversion-tracking`](skills/meta-ads-conversion-tracking/SKILL.md) | Pixel + Conversions API setup, Aggregated Event Measurement, event prioritization |
| [`meta-ads-experiments`](skills/meta-ads-experiments/SKILL.md) | A/B testing via Meta Experiments, statistical significance, creative/audience tests |
| [`meta-ads-anomaly-detection`](skills/meta-ads-anomaly-detection/SKILL.md) | Diagnose performance drops and spikes, proactive monitoring setup |
| [`meta-ads-automated-rules`](skills/meta-ads-automated-rules/SKILL.md) | Automated Rules and Marketing API automation — budget, bid, and pause automation |
| [`meta-ads-audience-overlap`](skills/meta-ads-audience-overlap/SKILL.md) | Find audiences competing against each other in auction, calculate cost, fix via exclusion/consolidation |
| [`meta-ads-audit-ecommerce`](skills/meta-ads-audit-ecommerce/SKILL.md) | ROAS audit, catalog health, Advantage+ Shopping structure, cart abandonment, seasonality |
| [`meta-ads-audit-leadgen`](skills/meta-ads-audit-leadgen/SKILL.md) | CPL audit, lead quality signals, Instant Forms vs website leads, offline conversion import |
| [`meta-ads-utm-generator`](skills/meta-ads-utm-generator/SKILL.md) | Build UTM templates, dynamic value insertion, naming conventions, GA4 channel grouping |

Skills are interconnected — `meta-ads-placement-mining` feeds `meta-ads-exclusions`, `meta-ads-conversion-tracking` is a prerequisite for `meta-ads-bidding`, and `meta-ads-attribution` directly affects how automated bidding performs.

---

## How it works

```
Meta Ads Account
      ↓
Data Connector  ←  Meta's official Ads MCP / Windsor / Supermetrics
      ↓
AI Agent        ←  Claude / Cursor / Windsurf / Gemini CLI
      ↓
Skills          ←  npx skills add emilyhellqvist/meta-ads-skills
```

The data connector gives the agent access to your live account data. The skills give it the domain expertise to do something useful with it.

---

## A note on account safety

Meta ad accounts have been banned in 2026 for how AI agents connected to them — not for using AI itself. Before you point this at a production account, read the **[security section of the Getting Started Guide](getting-started.md#keeping-your-ad-account-safe)**.

---

## Compatible with

Claude · Cursor · Windsurf · Gemini CLI · Codex · Any MCP-compatible agent

---

## License

MIT
