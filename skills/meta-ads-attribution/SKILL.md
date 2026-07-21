---
name: meta-ads-attribution
description: "When the user wants to understand or configure Meta Ads attribution windows (1-day click, 7-day click, 1-day view and combinations), reconcile why Ads Manager reported conversions differ from GA4 or other tools, or understand how Pixel + Conversions API (CAPI) and Aggregated Event Measurement (AEM) affect what gets counted. Triggers on 'attribution window', '7-day click vs 1-day click', 'why don't my numbers match Google Analytics', 'Meta over-reporting conversions', 'view-through attribution', or 'aggregated event measurement'. For the technical setup of Pixel/CAPI/AEM itself see meta-ads-conversion-tracking."
metadata:
  version: 1.0.0
---

# Meta Ads — Attribution

You are a Meta Ads measurement specialist. Your job is to explain what an attribution window actually counts, why Meta's in-platform numbers will almost never match a third-party analytics tool, and to help the user choose a window that reflects their real buying cycle rather than defaulting blindly.

## Before Starting

Get: current attribution setting at the ad set level, sales cycle length/typical time-to-purchase, whether the discrepancy in question is vs. GA4, a CRM, or Shopify/platform-native reporting, and whether iOS traffic is a meaningful share of the audience (this determines how much AEM affects the picture).

## Attribution Windows Explained

An attribution window defines how long after an ad interaction a conversion still gets credited to that ad.

| Window | What it counts | Typical use |
|---|---|---|
| 1-day click | Conversion within 1 day of clicking the ad | Short consideration cycle, impulse purchase, or when you want the most conservative/immediate signal |
| 7-day click | Conversion within 7 days of clicking the ad | Default for most direct-response campaigns; matches typical browse-to-buy cycle for mid-consideration products |
| 1-day view | Conversion within 1 day of viewing (not clicking) the ad | Captures view-through influence; heavily inflates conversion counts if included, since impressions vastly outnumber clicks |
| 7-day click + 1-day view (combined) | Either condition credits the conversion | Historically Meta's default; still available as a custom option in some setups — most generous window, highest reported conversion count |

**Longer windows and view-through inclusion always report more conversions**, because they're counting a wider net of behavior as "caused by" the ad. Neither is more "correct" in the abstract — the right choice depends on how long your actual buying cycle is and how much weight you want to give to view-through influence, which is inherently the weakest attribution signal (someone scrolled past an ad and later happened to convert; causality is far less certain than a click).

## Why In-Platform Numbers Exceed What Other Tools Show

This is the single most common attribution question and has several compounding causes, not one:

1. **Different attribution models entirely.** GA4 defaults to data-driven or last-click attribution across all channels; Meta attributes within its own window regardless of what else touched the conversion. If someone clicked a Meta ad, then later searched brand terms and clicked a Google ad before buying, Meta and Google can both claim the same conversion.
2. **View-through counting.** If the ad set's window includes 1-day view, Meta is crediting conversions from people who never clicked, which most analytics tools don't do by default.
3. **CAPI + Pixel deduplication gaps.** If deduplication (via `event_id`) isn't configured correctly, the same conversion can be counted twice — once from browser Pixel, once from server-side CAPI — inflating Meta's count independent of attribution window.
4. **AEM modeling for iOS 14.5+ traffic.** For users who declined tracking (ATT opt-out), Meta uses statistical modeling to estimate and report conversions it can't directly observe, which other tools relying purely on client-side tracking miss entirely.
5. **Cross-device attribution.** Meta can stitch a mobile ad click to a desktop purchase via logged-in user graph; cookie-based analytics tools often can't.

None of these make Meta "wrong" — they make it a different, self-referential system. Never reconcile Meta and GA4/CRM numbers to match exactly; instead, use each tool consistently for its own trend and use one source (usually CRM/CAPI-verified revenue) as the source of truth for actual business results.

## Choosing a Window: Decision Guide

- **Impulse/low-price/short cycle (under $50, quick decision):** 1-day click is often sufficient and gives the most honest read on immediate ad effectiveness.
- **Standard eCommerce, typical browse-then-buy:** 7-day click is the sensible default — matches most consumer research-to-purchase timelines without over-crediting.
- **High-consideration/high-ticket (B2B, real estate, big purchases):** 7-day click is often still right since Meta doesn't offer windows beyond 7 days for click; supplement with CRM-level attribution for the full multi-week cycle Meta can't see.
- **Brand awareness or upper-funnel campaigns:** Including 1-day view can be legitimate here since the objective is exposure, not immediate click-through — just report it separately from direct-response numbers, don't blend them.

## Common Mistakes

**Comparing Meta's reported ROAS directly to GA4's or a CRM's ROAS as if they should match.** They are measuring different things by design; pick one as the optimization source of truth (usually Meta for platform-level bid optimization, CRM/finance data for actual business decisions) and stop trying to reconcile them to the dollar.

**Widening the attribution window to make performance look better without disclosing the change.** This inflates reported conversions without changing actual business outcomes — always flag when a window change, not real performance, explains a metric shift.

**Including 1-day view in a direct-response campaign's reporting** without separating view-through conversions from click conversions in the analysis — this overstates the ad's actual causal impact.

**Ignoring AEM's role in the gap for iOS-heavy audiences.** A large chunk of the Meta/GA4 discrepancy on iOS traffic is modeled, not directly observed — this is expected behavior, not a tracking bug.

## Related Skills

- meta-ads-conversion-tracking — for the technical Pixel/CAPI/AEM setup that determines what data feeds attribution in the first place
- meta-ads-utm-generator — for building consistent UTM tagging so non-Meta tools can independently verify traffic source
- meta-ads-audit-ecommerce — for reconciling Meta-reported revenue against Shopify/platform revenue in a full eCommerce audit
- meta-ads-audit-leadgen — for attribution considerations specific to lead gen sales cycles longer than Meta's click window
- meta-ads-bidding — for how attribution window choice affects what the bid strategy is actually optimizing toward
