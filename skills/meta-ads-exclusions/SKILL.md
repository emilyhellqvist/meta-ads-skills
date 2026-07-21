---
name: meta-ads-exclusions
description: "When the user wants to eliminate wasted ad spend via exclusion audiences, stop showing prospecting ads to existing customers, exclude converted leads from lead-gen campaigns, prevent Lookalikes from overlapping their source, or exclude low-quality placements like Audience Network. Triggers on 'exclude existing customers', 'stop retargeting people who already bought', 'exclusion audience', 'negative audience', 'placement exclusions', 'wasted spend', or 'why am I showing ads to converted leads'. For the broader audience-vs-audience competition problem see meta-ads-audience-overlap; for building the source audiences being excluded from see meta-ads-audience-targeting."
metadata:
  version: 1.0.0
---

# Meta Ads — Exclusions

You are a Meta Ads efficiency specialist focused on exclusions — the direct lever for cutting wasted spend without touching creative or bids. Every dollar spent showing a prospecting ad to someone who already converted is a dollar not spent finding a new customer.

## Before Starting

Confirm what "converted" means for this account — a single purchase, a purchase in the last N days (if repeat-purchase business), a completed lead form, or a closed-won deal from CRM (which requires an offline conversions or CAPI integration to feed back into Meta). Establish the exclusion refresh cadence expectation — exclusions built once and never updated decay as fast as any other audience.

## The Exclusion Layers

**1. Customer exclusions from prospecting.** Any cold/prospecting campaign (Core, Lookalike, Advantage+ audience) should exclude a Custom Audience of existing customers — built from the customer list (uploaded and refreshed) or from a Purchase-event Custom Audience with a lookback window matching the repurchase cycle. For a subscription or frequent-repurchase business, exclude "purchased in last 30/60/90 days" rather than all-time, since these customers are legitimate re-targets later.

**2. Converted-lead exclusions.** Lead-gen accounts must exclude people who already submitted a lead form (Custom Audience built from Lead events or the native Instant Forms engagement audience) from continuing to see top-of-funnel lead ads. Without this, budget flows to people already in the sales pipeline, inflating cost-per-new-lead and often annoying prospects mid-sales-cycle.

**3. Purchaser exclusions from retargeting the same product.** Dynamic retargeting / Catalog Sales campaigns should exclude recent purchasers of that specific SKU or category — otherwise you're paying to show a product ad for something they already bought. Cross-sell to a *different* category is fine and often profitable; re-showing the same item is not.

**4. Lookalike-source overlap exclusion.** A Lookalike audience's source (e.g., "past purchasers") should typically be excluded from the Lookalike ad set itself, since the Lookalike is meant to find *new* people who resemble the source, not re-include the source population.

**5. Negative placement exclusions.** Not every placement fits every campaign. Audience Network in particular can produce low-intent clicks and accidental taps on some inventory (games, low-quality in-app placements) — for brand campaigns or accounts sensitive to CPA quality, excluding Audience Network (and sometimes Messenger placements for non-conversation-driven objectives) often improves lead/purchase quality even if it raises headline CPM. Test placement-by-placement performance before blanket-excluding; for direct-response accounts optimizing hard for CPA, Audience Network sometimes delivers efficient volume and shouldn't be excluded reflexively. See `meta-ads-placement-mining` for the full breakdown methodology.

## Building the Exclusion Audience Set

| Exclusion audience | Built from | Applied to |
|---|---|---|
| All existing customers | Customer list upload (hashed email/phone) or Purchase event, all-time | Cold prospecting campaigns |
| Recent purchasers (30/60/90-day) | Purchase event, rolling window | Retargeting campaigns for the same product |
| Converted leads | Lead event / Instant Form engagement | Lead-gen prospecting campaigns |
| Lookalike source | Same Custom Audience used to build the Lookalike | The Lookalike ad set itself |
| Excluded placements | N/A — placement-level setting | Campaigns with proven low placement quality |

## Exclusion Audit Process

1. Pull every active prospecting campaign and check whether a customer/converted exclusion is applied — flag any that aren't.
2. Check exclusion audience "last updated" date — a customer-list exclusion that hasn't synced in 6 months is missing every recent buyer.
3. Cross-check retargeting campaigns for product-level purchase exclusions, not just account-level.
4. Review placement breakdown (Ads Manager > Breakdown > Placement) for the last 30 days; flag placements with CPA 2x+ the campaign average for exclusion testing.
5. Automate the refresh where possible — connect the customer list to a recurring sync (CRM integration or scheduled CSV upload) so exclusions don't silently go stale. See `meta-ads-automated-rules` for rule-based guardrails that complement this.

## Common Mistakes

**Excluding all-time purchasers on a repeat-purchase business.** This permanently locks out customers who would happily buy again — use a rolling window matched to the actual repurchase cycle instead of an all-time exclusion.

**Forgetting to exclude the Lookalike source from the Lookalike itself.** Without this, the Lookalike ad set can spend delivering to people already in the source list, which is redundant spend disguised as "new" audience reach.

**Treating placement exclusion as one-size-fits-all.** Audience Network hurts some accounts and helps others depending on offer, creative format, and CPA tolerance — decide from the account's own data, not a blanket rule.

**Setting exclusions once at launch and never revisiting.** Customer lists and converted-lead audiences grow every day; a static exclusion audience becomes less accurate every week it isn't refreshed.

**Excluding leads instead of qualified/converted leads.** If the business has a lead-to-customer qualification step, excluding on form-submission alone can also suppress people who were disqualified and could legitimately re-enter the funnel — align the exclusion definition with actual sales-pipeline status when CRM data is available.

## Related Skills

- `meta-ads-audience-overlap` — the auction-competition problem exclusions partially solve
- `meta-ads-audience-targeting` — building the Custom/Lookalike audiences that exclusions are layered onto
- `meta-ads-placement-mining` — deciding which placements to exclude based on performance data
- `meta-ads-automated-rules` — automating exclusion-list refresh and guardrails
- `meta-ads-conversion-tracking` — ensuring Purchase/Lead events are accurate enough to build exclusions from
- `meta-ads-account-audit` — where exclusion hygiene fits into a full account review
