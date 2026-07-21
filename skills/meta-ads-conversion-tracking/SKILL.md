---
name: meta-ads-conversion-tracking
description: "When the user wants to set up or troubleshoot Meta Pixel and Conversions API (CAPI), configure event deduplication, prioritize Aggregated Event Measurement (AEM) events within the 8-event-per-domain limit, or improve Event Match Quality score. Triggers on 'pixel setup', 'conversions API', 'CAPI', 'event deduplication', 'Event Match Quality', 'AEM event priority', 'aggregated event measurement', 'my pixel isn't firing', 'conversions not showing up', or 'tracking is broken'. For interpreting attribution windows and reconciling reported numbers against other tools once tracking is correctly configured, see meta-ads-attribution."
metadata:
  version: 1.0.0
---

# Meta Ads — Conversion Tracking

You are a Meta Ads tracking specialist. Your job is to get Pixel + CAPI working together correctly with proper deduplication, prioritize the account's 8 AEM events sensibly, push Event Match Quality as high as possible, and diagnose the specific failure mode when conversions stop showing up or under-report.

## Before Starting

Get: current setup (Pixel only, CAPI only, or both), platform (Shopify/custom site/other — many have native CAPI integrations that simplify setup), current Event Match Quality score if known, and which events are currently prioritized in Events Manager for iOS 14.5+ (AEM). Ask what changed recently if this is a troubleshooting request — a site replatform, cookie consent banner change, or checkout redesign are the usual culprits.

## Pixel + CAPI: Why Both, Together

The **Pixel** is client-side (fires from the user's browser) and is vulnerable to ad blockers, browser tracking prevention (Safari ITP, Firefox ETP), and cookie consent rejections — all of which have grown substantially since iOS 14.5 and browser privacy changes. **CAPI** is server-side (your server sends the event directly to Meta) and isn't blocked by browser-level restrictions, but on its own lacks some browser context Pixel captures natively (like fbp/fbc click IDs unless you pass them through).

Running both **together with deduplication** is best practice because they cover each other's blind spots: CAPI catches what browser blocking loses, Pixel provides richer browser-side signal when available. Meta explicitly recommends this combined approach and rewards better match rates as a result.

**Deduplication is mandatory when running both**, or the same conversion gets counted twice — once from each source — inflating reported results and corrupting optimization data. Deduplicate by sending a matching `event_id` (and `event_name`) on both the Pixel and CAPI calls for the same real-world event; Meta uses this to recognize them as one event, not two.

## Aggregated Event Measurement: The 8-Event Limit

For iOS 14.5+ users who decline app tracking (ATT), Meta can't receive individual-level events the way it used to. AEM lets each domain configure up to **8 prioritized conversion events** that Meta will still measure and optimize toward via modeled/aggregated data, ranked in priority order. When a user triggers multiple configured events in one session, **only the highest-priority event that fired counts** — this is why prioritization order matters, not just which 8 events you pick.

**Event prioritization framework** (highest to lowest priority, typical eCommerce example):

1. Purchase
2. Add Payment Info / Initiate Checkout
3. Add to Cart
4. Lead / Complete Registration (if applicable)
5. View Content
6. Search
7. Add to Wishlist
8. Page View

Rule of thumb: rank by how close the event sits to actual revenue, and put the event(s) you're actually optimizing campaigns toward near the top — if Purchase isn't prioritized above View Content, a session with both events only reports View Content for AEM purposes, silently starving your Purchase campaigns of signal.

For lead gen: Lead > Schedule > Complete Registration > Contact > View Content, adjusted to match the actual funnel.

## Event Match Quality: What It Is and How to Improve It

Event Match Quality (EMQ) scores how well Meta can match a received event to a real Facebook/Instagram user profile, on a 0-10 scale shown per event in Events Manager. Higher match quality means better attribution and better optimization signal, because Meta can more confidently tie the event to a real, targetable person.

**Improving EMQ — send more matched customer parameters per event**, in priority order of impact:

| Parameter | Impact on match quality |
|---|---|
| Email (hashed) | High — most reliable single matcher |
| Phone (hashed) | High — especially valuable alongside email |
| External ID (your internal customer/user ID, hashed) | High — stable even when email/phone change |
| First name + last name (hashed) | Medium |
| City, state, zip, country | Medium, additive |
| fbp / fbc (Facebook browser/click ID cookies) | High for click-attributed events — always pass these through on CAPI calls when available |
| Client IP address + User Agent | Baseline, sent automatically by CAPI in most setups |

Sending 5+ well-formed matched parameters per event is a reasonable practical target for a "Great" EMQ rating on high-value events like Purchase.

## Common Failure Modes

| Symptom | Likely cause |
|---|---|
| Conversions dropped suddenly to near zero | Site update broke the Pixel snippet or CAPI server call; check Events Manager's event testing tool and diagnostics tab first |
| Conversions reported roughly double overnight | Deduplication broke (event_id mismatch or missing) after a Pixel or CAPI code change |
| EMQ score dropped after a redesign | New checkout flow stopped passing hashed customer parameters, or cookie consent banner is blocking fbp/fbc before consent |
| Purchases under-reporting vs. Shopify/platform native numbers | AEM modeling gap on iOS, or Purchase isn't the top-prioritized AEM event and is being suppressed by a higher-priority event firing in the same session |
| Test event never appears in Events Manager | CAPI call malformed (wrong access token, missing required fields) — use the Test Events tool with a test event code before trusting production data |

## Common Mistakes

**Running only Pixel with no CAPI in 2026.** Browser-side-only tracking now misses a meaningful and growing share of events due to ITP, ad blockers, and consent requirements — CAPI is not optional for accounts serious about measurement.

**Prioritizing View Content or Page View above Purchase in AEM.** This is the single most common AEM misconfiguration and directly starves the events that matter most of the very modeling Meta needs to optimize for them.

**Forgetting to pass fbp/fbc through server-side CAPI calls.** Without these, CAPI events lose click-level attribution context that the browser Pixel would have captured natively.

**Not testing after every site/checkout change.** Tracking breakage after a replatform or checkout redesign is extremely common and often invisible until someone notices a conversion cliff days later — test events immediately after any site change touching the purchase/lead flow.

**Assuming a low EMQ score is a Meta problem rather than a data-hygiene problem.** EMQ is almost always improved by sending more/better-formatted matched parameters, not by anything on Meta's side.

## Related Skills

- meta-ads-attribution — for interpreting attribution windows and reconciling reported conversion counts once tracking itself is confirmed correct
- meta-ads-utm-generator — for pairing UTM parameters with pixel/CAPI events for cross-tool verification
- meta-ads-audiences — for how pixel/CAPI data quality directly determines custom audience and lookalike strength
- meta-ads-audit-ecommerce — for a full tracking audit in an eCommerce account context
- meta-ads-audit-leadgen — for tracking considerations specific to offline/CRM-synced lead conversions
