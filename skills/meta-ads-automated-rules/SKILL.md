---
name: meta-ads-automated-rules
description: "When the user wants to automate parts of a Meta Ads account with Automated Rules or the Marketing API — pausing underperformers, scaling winners, capping spend, or building custom automation. Triggers on 'set up automated rules', 'pause underperforming ad sets automatically', 'scale winning ads automatically', 'automate my Meta account', 'Marketing API automation', 'rule to pause high CPA', or 'spend cap safety net'. Also covers the account-safety risks of aggressive API automation — see meta-ads-anomaly-detection for diagnosing damage already done and meta-ads-budget-pacing for pacing-specific rules."
metadata:
  version: 1.0.0
---

# Meta Ads — Automated Rules

You are configuring rule-based automation for a Meta Ads account, either through the native Automated Rules feature or, for more complex logic, direct Marketing API scripts. The goal is to remove manual busywork without introducing new failure modes — over-aggressive automation is one of the fastest ways to quietly wreck an account's learning phase or, at the API level, get the account restricted.

## How Automated Rules Work

Rules are condition-action pairs evaluated on a schedule — continuous (roughly every 30 minutes), or hourly/daily/custom — applied at the campaign, ad set, or ad level. Actions available: pause, adjust budget by amount or percentage, adjust bid, send notification only. Rules can combine multiple conditions (AND logic) and should always include a minimum spend or minimum result threshold so they don't fire on statistically meaningless early data.

## Rule Recipes

| Goal | Condition | Action | Caveat |
|---|---|---|---|
| Pause underperformers | CPA > target AND spend > 2–3x target CPA, over 3-day window | Pause ad set | Never fire before ad set exits learning phase (~50 conversions) |
| Scale a winner | ROAS > target for 3 consecutive days AND spend > threshold | Increase budget 15–20% | Cap increment size — large jumps reset learning phase |
| Spend safety net | Account or campaign spend > daily cap | Turn off campaign | Set as a hard backstop, not primary budget control |
| Frequency watch | Frequency > 4 within 7 days | Notify only, don't auto-pause | High frequency isn't always inefficient — check CPA first |
| Pacing check | Daily spend < 50% of budget by a fixed time | Notify | Signals delivery/targeting problem, not something to auto-fix blindly |

## Pitfalls: Rules That Do More Harm Than Good

- **Pause rules with no minimum sample size.** A rule that pauses on "0 conversions in first 24 hours" will kill nearly every ad set before it has a chance to exit learning, because early delivery is inherently noisy.
- **Rules that check too frequently on thin data.** Continuous evaluation on a brand-new ad set amplifies noise into false signals.
- **Stacked, conflicting rules.** A scale rule and a pause rule both watching similar metrics can thrash an ad set — scaling it one day, pausing it the next — which is worse than doing nothing.
- **Ignoring attribution lag.** Conversion events can land up to several days after the click. A rule judging "no conversions yet" without accounting for lag punishes ad sets that are actually performing fine.
- **Budget-increase rules with no ceiling on increment size.** A 20%+ single jump resets the learning phase and can spike CPA right when the rule thinks it's rewarding a winner.

## When Native Rules Aren't Enough: Marketing API Automation

Cross-account logic, multi-condition scoring, or automation driven by external signals (inventory, weather, CRM data) requires going direct to the Marketing API. This is more powerful — and considerably riskier if built carelessly.

## Security & Pacing Guidance for API Automation

**This is the section to get right before writing any code.** Aggressive automated write actions — rapid-fire budget changes, high-frequency polling loops, mass ad creation or pause/unpause cycling — are a leading cause of account-level restrictions and bans on the platform. Before building direct API automation:

- Respect Meta's rate limits and implement exponential backoff on failures; never retry in a tight loop.
- Batch write requests instead of issuing many small sequential calls.
- Avoid write-heavy automation patterns on new or unverified Business Manager accounts — these accounts have far less tolerance before triggering automated enforcement.
- Use a System User access token scoped to the minimum required permissions rather than a personal token, and rotate/secure tokens properly.
- Throttle automated pacing/scaling logic to human-plausible frequencies (e.g., budget changes no more than once every few hours) rather than reacting to every data tick.
- This skill is a pointer, not a full technical spec — consult the account's dedicated API rate-limit and security guidance before shipping automation that writes to a live ad account.

## Output Template

```
RULE AUDIT CHECKLIST
Rule name: [ ]
Trigger condition(s): [ ]
Minimum sample threshold set? [Y/N]
Action: [ ]
Check frequency: [ ]
Conflicts with other active rules? [ ]
Last reviewed: [ ]
```

## Common Mistakes

- No minimum spend/conversion threshold on pause rules.
- Rules firing while an ad set is still in the learning phase.
- Stacking rules with overlapping, conflicting logic.
- Building custom API automation without rate-limit handling or backoff — resulting in a flagged or restricted ad account.
- Set-and-forget rules never revisited as CPMs, seasonality, and account context shift.

## Related Skills

- meta-ads-anomaly-detection — diagnosing damage after a bad rule or automation run
- meta-ads-budget-pacing — pacing-specific automation and manual controls
- meta-ads-bidding — how bid strategy interacts with automated budget changes
- meta-ads-account-audit — where rule health should be checked as part of a full audit
- meta-ads-attribution — understanding lag before writing conversion-based rule conditions
