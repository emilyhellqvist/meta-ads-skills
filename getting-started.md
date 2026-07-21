# Meta Ads AI Agent — Getting Started Guide

This guide walks you through setting up an AI agent that can read your live Meta Ads data (Facebook & Instagram) and apply deep optimization expertise to it. Once set up, you can ask natural language questions like *"Why did my CPM jump this week?"* and get data-backed, expert answers — without pulling a single export.

---

## What you get

When this is set up, your AI agent (Claude, Cursor, or similar) will be able to:

**Query your live Meta Ads data**
- Pull campaign, ad set, and ad performance, audiences, placements, and spend — across any date range
- Ask in plain English: no Ads Manager exports, no dashboards

**Apply expert-level analysis**
- 21 specialized optimization skills that give the AI deep Meta Ads domain knowledge
- Skills cover: account audits, audience strategy, creative fatigue, relevance diagnostics, bidding, attribution, audience overlap, anomaly detection, and more

**Work across your full account structure**
- Supports individual ad accounts and multi-account Business Managers
- Run the same analysis across multiple clients in one session (depending on connector)

**Example things you can do on day one:**
```
Run a full account audit and prioritize the top 5 things to fix.
```
```
Which ad sets are spending budget but have zero conversions in the last 30 days?
```
```
My CPA went up 40% this week — diagnose what happened.
```
```
Which audiences are overlapping and cannibalizing each other in auction?
```
```
Which ad sets are showing creative fatigue and need a refresh?
```

---

## How it works

The setup has three layers:

```
Your Meta Ads Account
        ↓
  Data Connector (Meta's official MCP / Windsor / Supermetrics)
        ↓
  AI Agent (Claude / Cursor) + Meta Ads Skills
```

1. **Data connector** — bridges your live Meta Ads data to the AI agent via MCP (Model Context Protocol), an open standard that lets AI tools query external data sources
2. **AI agent** — the tool you use to talk to the AI (Claude, Cursor, etc.)
3. **Skills** — a set of knowledge files installed into the agent that give it expert-level Meta Ads frameworks on top of your live data

---

## Step 1 — Choose your data connector

Three options:

| Connector | Best for | Setup time | Cost |
|-----------|----------|------------|------|
| [**Meta's official Ads MCP**](setup/meta-ads-mcp.md#option-a) | Direct OAuth to your own account, no third-party cost | 15–20 min | Free |
| [**Windsor**](setup/windsor-mcp.md) | Fastest setup, works today even if the official MCP isn't rolled out to your account yet | 10–15 min | Paid (free trial) |
| [**Supermetrics**](setup/supermetrics-mcp.md) | Already on Supermetrics, or want 200+ platforms in one workspace | 10–20 min | Existing plan |

**Not sure which to pick?** Try the official MCP first — check Business Manager for an "Ads AI Connectors" option. Meta is rolling it out in phases, so if it's not there yet, use Windsor to get moving today and switch later if you want.

Full walkthroughs with exact steps live in [setup/meta-ads-mcp.md](setup/meta-ads-mcp.md), [setup/windsor-mcp.md](setup/windsor-mcp.md), and [setup/supermetrics-mcp.md](setup/supermetrics-mcp.md).

### Sanity check

Once connected, ask your agent:
```
What are my top 10 Meta Ads campaigns by spend in the last 30 days?
```
If you get campaign names and spend back, the connection works.

---

## Step 2 — Install the Meta Ads Skills

Once your data connector is working, install the skills. This gives your agent deep Meta Ads expertise — not just data access, but the frameworks and playbooks to do something useful with it.

Run this in your terminal:

```bash
npx skills add emilyhellqvist/meta-ads-skills
```

This installs 21 skills covering:

| Area | Skills included |
|------|----------------|
| Account health | Account audit, anomaly detection |
| Audiences | Audience targeting, audiences, audience overlap, exclusions |
| Creative | Ad copy, creative formats, creative fatigue |
| Performance | Relevance diagnostics, placement mining, segmentation |
| Bidding & budget | Bidding, budget pacing |
| Measurement | Conversion tracking, attribution, UTM generator |
| Testing | Experiments |
| Automation | Automated rules |
| Audits | Ecommerce audit, lead gen audit |

### Verify skills are loaded

```
List the Meta Ads skills you have available.
```

```
Run a quick account audit — what are the top 3 things I should fix first?
```

---

## Keeping your ad account safe

This is the section every "AI + Meta Ads" setup skips, and it's the one that matters most. In early-to-mid 2026, a wave of Meta ad account bans hit performance marketers who had connected AI agents to their accounts — including long-running accounts spending six and seven figures a month. It was never "using AI" that got accounts banned. The pattern behind almost every reported case was the same:

- Autonomous agents pointed straight at the Marketing API with raw personal access tokens, no human in the loop
- High-volume, bursty API calls — an agent retrying aggressively on every error, which reads to Meta's anomaly detection as bot or fraud activity
- Ungated write access — the agent publishing creative, shifting budgets, or editing campaigns with no review step
- Unofficial developer apps — every call routed through someone else's shared app, so if that app got flagged, every account using it caught the fallout

**How to avoid it:**

1. **Use an authorized connection.** Prefer Meta's official Ads MCP or a reviewed partner with Meta Business Partner status (Windsor, Supermetrics). These authenticate via OAuth against your own account — there's no shared developer app to get flagged.
2. **Don't let the agent hammer the API.** Cap consecutive write actions, and don't let it retry blindly on errors or 429 responses.
3. **Keep a human in the loop for anything that spends money.** Default to read-only analysis. Treat budget/bid/campaign changes as drafts you approve, not autonomous actions. Test any new connector on one small, reversible action before trusting it near real budgets.
4. **Apply Meta's AI Content Label.** Since March 2026, any ad creative where AI generated the visual subject or wrote the copy needs the label. "Undisclosed AI Content" is a leading ad-rejection reason, and repeated strikes escalate to account suspension.

Full detail on all four is in the standalone **[Ultimate Meta Ads Skills for Claude Desktop — Setup Guide](https://github.com/emilyhellqvist/meta-ads-skills)** security section — worth reading in full before connecting anything to a production account.

---

## Troubleshooting

### The official MCP shows `is_ads_mcp_enabled: false`
- Your account hasn't reached Meta's phased rollout yet — there's no manual override or support ticket that speeds it up
- Check Business Manager for an "Ads AI Connectors" option; recheck every few days
- Use Windsor or Supermetrics in the meantime

### Connector not showing up in your agent
- Restart the agent after any config file change
- Check the config file for JSON syntax errors (missing commas, unclosed brackets)
- On Claude Desktop, go to Help → Restart Claude to force a reload

### "Needs Login" not clearing (Windsor / Cursor)
- Refresh the MCP server in your agent's settings after completing OAuth in the browser
- Try disconnecting and reconnecting the server from the settings panel

### No data returned
- Confirm your Meta Ads account is connected and has data in the date range you specified
- Check that the right ad account(s) are selected in your connector dashboard
- Try a broader date range — some accounts have delayed data

### Authentication errors (Supermetrics)
- The API key must be prefixed: `Authorization: Api-Key your-key` — not just the key alone
- Regenerate the key in hub.supermetrics.com if in doubt

### Write actions are rejected (official MCP)
- Confirm the `ads_management` scope was granted during OAuth
- Some accounts are read-only by design until you explicitly grant write scope — check Business Manager permissions

### Requests are slow or throttled (429 errors)
- You've hit Meta's Marketing API rate limit — space out bulk changes rather than retrying immediately
- Aggregate requests at the highest level that answers your question (campaign-level beats ad-level) to use fewer calls

### Skills not loading
- Run `npx skills add emilyhellqvist/meta-ads-skills` again to reinstall
- Check you're running a recent version of Node.js (`node -v` should return v18+)

---

## Limitations

Understanding what this setup **cannot** do is as important as knowing what it can.

| Limitation | Detail |
|------------|--------|
| **Write actions are live** | Pausing a campaign or changing a budget takes effect immediately — there's generally no draft mode or one-click undo |
| **No real-time alerts** | The agent responds to questions — it doesn't proactively monitor your account |
| **Freshness delay** | Same-day data and attribution can be incomplete for hours or days |
| **Attribution gaps** | iOS 14.5+ restrictions, modeled conversions, and view-through windows may not match in-platform totals |
| **Advantage+ opacity** | Asset-level breakdowns and audience segmentation inside Advantage+ campaigns can be limited |
| **Breakdown limits** | Some breakdown combinations (e.g. age + placement together) are blocked by the API |
| **Platform policy still applies** | The MCP doesn't bypass ad review, spending limits, or Meta's standard policy enforcement |
| **Rate limits** | The API is subject to Meta's standard throttling regardless of which connector you use |

---

## Resources

| Resource | Link |
|----------|------|
| GitHub — All skills and setup guides | [github.com/emilyhellqvist/meta-ads-skills](https://github.com/emilyhellqvist/meta-ads-skills) |
| Detailed official MCP setup | [setup/meta-ads-mcp.md](setup/meta-ads-mcp.md) |
| Detailed Windsor setup | [setup/windsor-mcp.md](setup/windsor-mcp.md) |
| Detailed Supermetrics setup | [setup/supermetrics-mcp.md](setup/supermetrics-mcp.md) |
| Meta Ads AI Connectors (official docs) | [facebook.com/business/help/1456422242197840](https://www.facebook.com/business/help/1456422242197840) |
| Meta AI Content Label policy | [transparency.meta.com — AI disclosures](https://transparency.meta.com/policies/other-policies/meta-AI-disclosures) |
| Meta Marketing API rate limits | [developers.facebook.com — rate limiting](https://developers.facebook.com/docs/marketing-api/overview/rate-limiting/) |
| Windsor.ai | [windsor.ai](https://windsor.ai) |
| Supermetrics Hub | [hub.supermetrics.com](https://hub.supermetrics.com) |
