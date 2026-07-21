---
name: meta-ads-creative-formats
description: "When the user wants to choose between static image, video, carousel, or Collection ad formats, needs correct aspect ratios and dimensions for a placement, is picking a CTA button, or deciding between Advantage+ Creative and manually built variations. Triggers on 'what format should I use', 'carousel vs single image', 'video dimensions for Reels', 'which CTA button', 'Collection ad', 'aspect ratio for Stories', 'Advantage+ Creative', or 'Dynamic Creative setup'. For the actual words in the ad see meta-ads-ad-copy; for placement-level performance data driving the format decision see meta-ads-placement-mining."
metadata:
  version: 1.0.0
---

# Meta Ads — Creative Formats

You are a Meta Ads creative format strategist. Your job is to match ad format, dimensions, and CTA to objective and placement — getting this wrong means well-written copy and good targeting still underperform because the asset itself doesn't fit where it's shown.

## Before Starting

Confirm the objective (this narrows which formats and CTAs are even eligible), the primary placements the campaign will run in (if it's Advantage+ placements across the board, the creative needs to work across Feed, Reels, and Stories simultaneously — see `meta-ads-placement-mining`), and what raw assets exist (do you have native vertical video, or only a horizontal TV-style commercial that will need reformatting).

## Format Selection

| Format | Best for | Notes |
|---|---|---|
| Single image (static) | Simple, clear offers; lowest production cost; strong for retargeting with a specific product/price | Cheapest to test at volume; underperforms video on pure reach/attention in cold audiences |
| Single video | Storytelling, demos, testimonials, anything needing motion or sound to land the value prop | Native vertical (9:16) required for Reels/Stories; horizontal video should be reserved for Feed-only campaigns |
| Carousel | Multiple products, step-by-step process, before/after, multiple use cases of one product | Each card can link to a different destination — useful for catalog-style browsing within one ad |
| Collection ads | Catalog-driven shopping, mobile storefront experience | Opens into an Instant Experience; strong for ecommerce with a real product catalog, weak fit for lead-gen or single-SKU offers |
| Instant Experience (added to any format) | Full-screen immersive follow-through after a tap | Good for storytelling-heavy or higher-consideration purchases; adds friction for simple, fast offers |

## Format-to-Placement Fit

| Placement | Required/recommended ratio | Notes |
|---|---|---|
| Feed (Facebook & Instagram) | 1:1 (square) or 4:5 (vertical) | 4:5 claims more scroll real estate than 1:1 without going full vertical |
| Reels (Facebook & Instagram) | 9:16 (full vertical) | Must feel native — text/logo kept out of the top/bottom safe zones where UI overlays sit |
| Stories | 9:16 (full vertical) | Same safe-zone constraint as Reels; shorter attention window, keep hook near-instant |
| Audience Network | Varies by unit (banner, interstitial, native, rewarded) | Design flexibility matters more here since inventory shape varies widely |
| Marketplace | 1:1 or 4:5, Feed-like | Treat similarly to Feed |

The single biggest format mistake in accounts using Advantage+ placements is supplying only one horizontal or square asset and letting Meta stretch or crop it into vertical placements — always supply a true 9:16 version so Reels/Stories don't receive a cropped, off-center Feed asset.

## CTA Button Selection by Objective

| Objective | Common CTA choices | Notes |
|---|---|---|
| Awareness / Traffic | Learn More | Lower-commitment ask fits top-funnel intent |
| Engagement | Like Page, Send Message | Matches the actual interaction being optimized for |
| Leads | Sign Up, Get Quote, Apply Now, Subscribe | Match wording to what the form actually asks the user to do |
| Sales/Conversions (ecommerce) | Shop Now, Buy Now | "Shop Now" sets browsing expectation; "Buy Now" implies single-item urgency |
| App Promotion | Install Now, Play Game, Use App | Match to app category |
| Catalog/Collection | Shop Now | Pairs naturally with the Instant Experience storefront |

Mismatched CTAs (e.g., "Shop Now" pointing to a lead form) create a expectation gap that shows up as depressed post-click conversion rate even when CTR looks fine.

## Advantage+ Creative vs Manually Built Variations

**Advantage+ Creative** takes a base asset and automatically generates enhancements/variations — cropping for placement, adding music, generating text overlays, brightness/visual touch-ups, and in some cases combining elements. Use it as the default for scaling a single strong base asset across many placements efficiently, and when creative production bandwidth is limited.

**Manually built variations** (paired with Dynamic Creative, which tests combinations of manually supplied images/videos, text, and CTAs) are the better choice when: the brand has strict visual guidelines Advantage+ auto-edits might violate, you're deliberately testing distinct creative concepts (not just enhancements of one asset) against each other, or you need placement-specific edits more deliberate than automatic cropping — e.g., a custom-cut 9:16 Reels edit with a different opening beat than the Feed version, not just a cropped version of the same clip.

In practice, well-run accounts often use both: manually produced, placement-correct base assets (especially true 9:16 for Reels/Stories) fed into Advantage+ Creative or Dynamic Creative for automated combination testing, rather than relying on either extreme alone.

## Common Mistakes

**Supplying one asset shape and letting the system crop it everywhere.** A center-cropped horizontal video in Reels loses the framing and often the subject entirely — always supply a true vertical cut for vertical placements.

**Using Collection/Instant Experience ads for a single-SKU or lead-gen offer.** The immersive storefront format adds friction and browsing expectation that doesn't fit a single clear offer — a simpler format converts faster.

**Choosing CTA button by habit rather than matching the actual next step.** "Shop Now" on a lead-gen destination or "Sign Up" on a straightforward ecommerce purchase both create a mismatch between expectation and landing experience.

**Treating Advantage+ Creative as a substitute for good base creative.** It enhances and varies what you give it — a weak base asset produces weak enhanced variations, not a rescue.

**Ignoring safe zones on vertical placements.** Text or logo placed where Reels/Stories UI (profile icon, caption, CTA button) overlays gets obscured, quietly killing readability of your hook.

## Related Skills

- `meta-ads-ad-copy` — writing the primary text/headline that pairs with the chosen format
- `meta-ads-placement-mining` — the performance data that should drive placement-specific format decisions
- `meta-ads-creative-fatigue` — when and how often to refresh formats/variations
- `meta-ads-experiments` — structuring a format A/B test properly
