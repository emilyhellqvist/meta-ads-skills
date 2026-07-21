---
name: meta-ads-audit-ecommerce
description: "When the user wants to audit an ecommerce Meta Ads account — ROAS by product/campaign, Catalog health, Advantage+ Shopping campaign structure, or dynamic retargeting setup. Triggers on 'audit my ecommerce Meta ads account', 'Advantage+ shopping audit', 'catalog health check', 'ROAS by product', 'DPA retargeting audit', 'why is my product feed rejecting items', or 'ecommerce account review'. For the general-purpose audit framework see meta-ads-account-audit; for the lead-gen equivalent see meta-ads-audit-leadgen."
metadata:
  version: 1.0.0
---

# Meta Ads — Ecommerce Account Audit

You are auditing a Meta Ads account for an ecommerce or DTC business. The audit needs to answer: is spend actually profitable (not just ROAS-positive on paper), is the catalog feeding the algorithm clean data, is the account using Advantage+ Shopping appropriately, and is retargeting structured to recover abandoners without wasting spend on people who already bought.

## Audit Layer 1: ROAS & Profitability

Platform-reported ROAS is not profit. Convert it: break-even ROAS = `1 ÷ gross margin %`. A 40% margin business needs a 2.5x ROAS just to break even before ad spend is profitable — report both the raw ROAS and the margin-adjusted profitability.

| Vertical | Typical blended ROAS range (directional) | Watch for |
|---|---|---|
| Apparel/fashion | 2–4x | Heavy return-rate impact on true profit |
| General merchandise | 3–6x | Wide variance by AOV |
| Beauty/consumables | 3–5x | LTV/repeat-purchase matters more than first ROAS |
| High-ticket/furniture | 1.5–3x | Longer consideration window skews attribution |

Break down ROAS by campaign *and* by product/product set — a strong blended number often hides a handful of loss-making SKUs propped up by a few winners.

## Audit Layer 2: Catalog Health

Checklist (Commerce Manager → Catalog → Diagnostics):
- Feed errors and warnings count, and trend over time (not just current snapshot)
- Missing GTIN/MPN/brand — these fields directly affect Advantage+ Shopping's ability to match products to intent signals; missing identifiers suppress reach on affected items
- Availability field freshness — stale sync means ads keep running on out-of-stock items, wasting spend and hurting UX
- Price accuracy vs. live site price — mismatches risk disapproval and erode trust when caught
- Image quality and aspect ratio compliance for the placements in use
- Item ID stability across feed updates — changing IDs resets any ad-level social proof and retargeting history tied to that item

## Audit Layer 3: Advantage+ Shopping Campaigns (ASC) vs. Manual

**Use ASC when:** the goal is combined prospecting + retargeting in one automated structure, the catalog is broad enough for the algorithm to find patterns, and tight manual control isn't a priority. This is Meta's current recommended default for most catalog advertisers.

**Use manual/Standard Shopping when:** strict CPA/ROAS control by segment is required, brand-specific placement restrictions apply, the funnel needs deliberate sequential logic (cold → warm → retargeting with distinct messaging) that ASC's automation can't replicate, or precise customer exclusions are needed beyond ASC's built-in "existing customers" toggle.

**Red flag:** running ASC and a manual Shopping campaign on the same catalog simultaneously — they compete against each other in auction for the same buyers, functionally the same problem as audience overlap.

## Audit Layer 4: Dynamic Retargeting

- Segment by funnel depth: product-view abandoners vs. add-to-cart abandoners vs. checkout-initiated abandoners — different intent, different messaging, different bid tolerance.
- Attribution window per segment: 1-day and 7-day windows are common; longer windows (14-day+) risk showing ads for items already purchased elsewhere or no longer relevant.
- Creative: Collection ads and carousel formats generally outperform single-image DPA for catalog retargeting because they show more of the assortment.
- Frequency cap retargeting separately from prospecting — retargeting pools are smaller and fatigue faster.

## Audit Layer 5: Seasonality & Inventory

- Don't launch new campaigns or make major structural edits in the days immediately before a peak period (Black Friday/Cyber Monday) — the learning phase reset will hit right when volume matters most.
- Pace budget against actual inventory availability; exclude out-of-stock items from the catalog feed rather than letting them serve and disappoint.
- Build in a post-peak review to catch stale creative and audiences that were scaled aggressively for the peak and left untouched afterward.

## Output Template

```
ECOMMERCE AUDIT SCORECARD (weight × score, 0–100 total)
Profitability (margin-adjusted ROAS)      [ ] × 30%
Catalog health                             [ ] × 20%
Campaign structure (ASC vs manual fit)     [ ] × 20%
Retargeting setup                          [ ] × 15%
Seasonality/inventory readiness            [ ] × 15%
TOTAL: [ ]
Fix Immediately: [ ]
Fix This Month: [ ]
Ongoing: [ ]
```

## Common Mistakes

- Trusting platform-reported ROAS without a margin adjustment.
- Running Advantage+ Shopping and manual Shopping on the same catalog at once, causing self-competition.
- Feed errors silently suppressing the best-selling SKUs without anyone noticing.
- Retargeting windows too long, showing ads for items already purchased.
- No exclusion of recent purchasers from prospecting campaigns, wasting spend on people already converted.

## Related Skills

- meta-ads-account-audit — the general framework this specializes
- meta-ads-audience-overlap — diagnosing ASC vs. manual self-competition
- meta-ads-attribution / meta-ads-conversion-tracking — verifying ROAS numbers are trustworthy
- meta-ads-creative-formats — Collection/Carousel/DPA creative choices
- meta-ads-budget-pacing — pacing spend against inventory and seasonality
- meta-ads-bidding — ROAS goal and Cost Cap strategy for ecommerce
