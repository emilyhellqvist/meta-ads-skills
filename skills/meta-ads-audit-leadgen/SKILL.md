---
name: meta-ads-audit-leadgen
description: "When the user wants to audit a lead-generation Meta Ads account — CPL benchmarking, Instant Forms vs website lead forms, lead quality, or offline conversion setup. Triggers on 'audit my lead gen Meta campaigns', 'CPL too high', 'instant forms vs website forms', 'lead quality is bad', 'form completion rate', 'my leads are junk', or 'set up offline conversions for lead scoring'. For the general-purpose audit framework see meta-ads-account-audit; for the ecommerce equivalent see meta-ads-audit-ecommerce."
metadata:
  version: 1.0.0
---

# Meta Ads — Lead Gen Account Audit

You are auditing a Meta Ads account built for lead generation. The central risk in lead gen is optimizing for volume and cost while the algorithm has no idea which leads actually became customers — this audit exists to find where that quality signal is missing and get it fixed.

## Audit Layer 1: CPL Benchmarking

Benchmark CPL against the account's own historical baseline first — industry-wide CPL ranges are directional only and vary enormously by offer value, form length, and audience temperature. Use external benchmarks (legal, finance, home services, education typically run higher CPL; ecommerce-adjacent or low-commitment offers typically run lower) only to sanity-check, not to set targets.

## Audit Layer 2: Instant Forms vs. Website Lead Forms

| Dimension | Instant Forms (on-Meta) | Website Forms |
|---|---|---|
| Friction | Low — pre-filled fields, no page load | Higher — full page load, manual entry |
| Typical conversion rate | Often 2–3x higher completion | Lower completion, higher intent |
| Lead quality | More casual/lower-intent, higher volume | Generally higher intent, lower volume |
| Tracking robustness | Data stays largely on-platform; requires CRM sync-back for quality signal | First-party pixel + CAPI event with fuller Event Match Quality |
| Best use | Top-of-funnel volume, brand awareness offers | Bottom-of-funnel, qualified pipeline building |

There's no universally correct choice — the audit should confirm the form type matches the funnel stage the campaign is actually targeting, and flag it when a bottom-funnel, high-consideration offer is running exclusively through low-friction Instant Forms without a quality feedback loop.

## Audit Layer 3: Lead Quality Signal Analysis

Checklist:
- Form field count and friction — each additional required question tends to reduce completion rate meaningfully; check whether questions are qualifying (worth the drop-off) or just extra friction.
- Use of qualifying questions to pre-filter unqualified leads before they even submit.
- Spam/bogus lead rate — check against sales team feedback, not just Meta's own quality metrics.
- Sales follow-up speed correlated against close rate — slow follow-up can make good leads look bad in the data.
- Full funnel visibility: lead → marketing-qualified → sales-qualified → customer, tracked outside Meta in the CRM, not just lead volume inside Ads Manager.

## Audit Layer 4: Offline Conversion Import (CAPI for CRM Data)

This is the fix for the core lead-gen blind spot: Meta's optimization only knows what happens on-platform unless told otherwise. Feed CRM-qualified outcomes back via Offline Conversions / Conversions API so the algorithm can optimize toward actual quality, not just form fills.

- Define the event(s) to send back: Qualified Lead, Sales-Qualified Lead, Closed-Won — whichever stage has enough volume to be a usable optimization signal.
- Expect imperfect match rates — offline data matched back to the original ad exposure depends on the identifiers captured at lead time (email, phone).
- Delayed data still helps: even though offline imports arrive days or weeks after the original ad interaction, they still improve the algorithm's long-run targeting even without real-time feedback.

## Audit Layer 5: Form Completion Rate Diagnostics

| Symptom | Likely cause |
|---|---|
| High CTR, low form open rate | Ad-to-form message mismatch, or landing experience friction |
| High form open, low submit rate | Too many fields, unclear value exchange, poor mobile UX |
| High submit rate but high spam-flag rate | Missing qualifying questions, over-incentivized offer attracting freebie-seekers |

## Output Template

```
LEAD GEN AUDIT SCORECARD
CPL vs. account baseline: [ ]
Form type fit for funnel stage: [ ]
Lead quality signal present? [Y/N]
Offline conversion import configured? [Y/N]
Form completion rate: [ ]% — diagnosis: [ ]
Fix Immediately: [ ]
Fix This Month: [ ]
Ongoing: [ ]
```

## Common Mistakes

- Optimizing purely for CPL/volume with no quality signal feeding back into the algorithm.
- Too many form questions killing completion rate for marginal qualification value.
- Reporting Instant Form and Website leads together, hiding a quality gap between the two.
- Skipping offline conversion import — the single highest-leverage fix in most underperforming lead gen accounts.
- Judging campaign performance before the sales qualification lag has had time to resolve.

## Related Skills

- meta-ads-account-audit — the general framework this specializes
- meta-ads-conversion-tracking / meta-ads-attribution — CAPI setup and Event Match Quality
- meta-ads-ad-copy — aligning ad messaging with form/offer expectations
- meta-ads-bidding — Cost Cap and ROAS goal considerations for lead campaigns
- meta-ads-segmentation — separating lead sources for cleaner quality analysis
