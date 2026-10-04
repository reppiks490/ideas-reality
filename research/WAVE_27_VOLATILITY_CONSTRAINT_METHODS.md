# Wave 27V — Research Methods

Namespace: **W27V**

## W27V-M01 — Exact LULD Reference Reconstruction
Reconstruct the plan-defined rolling eligible-trade reference price and historical rule version.

Do not approximate bands from last trade.

## W27V-M02 — SIP Timestamp Contract
Store:
eligible trade time,
SIP receive/dissemination time,
band message time,
limit-state time,
pause time,
resume time.

## W27V-M03 — Tier/Price/Clock Parameter Versioning
Encode applicable percentage parameters by Tier, security price, time of day and historical plan amendment.

## W27V-M04 — Band-Touch vs Limit-State vs Pause
These are distinct states and labels.

Never treat every band touch as a pause.

## W27V-M05 — Fifteen-Second Survival Clock
Start the pause-hazard clock only from qualifying Limit State entry.

## W27V-M06 — Halt Cause Provenance
Use primary/exchange halt code and public timestamp.

Do not infer halt reason from price behavior.

## W27V-M07 — Primary Listing Exchange Reopen Rules
Reopening auction mechanics differ by listing market and historical rule version.

Use venue-specific rules.

## W27V-M08 — Auction Collar Version Ledger
Store each active collar, indicative price, imbalance and extension timestamp.

## W27V-M09 — Stale Index Calculation
When constituent is halted, preserve last valid cash price used by the index and compute hypothetical index values under shadow-price scenarios.

## W27V-M10 — Point-in-Time Index Weights
Use weights effective at halt time.

## W27V-M11 — Shadow-Price Uncertainty Interval
Latent halted value must be a distribution/interval, not a point claim.

## W27V-M12 — Cross-Market Latency Alignment
Align futures/ETF/options/peer observations to public halt/pause state with realistic feed latency.

## W27V-M13 — Reopening Outcome Target
Define reopening target before model search:
auction price,
first 1m VWAP,
repeat-pause probability,
or post-reopen liquidity.

## W27V-M14 — SSR Trigger Reconstruction
Use prior official regular-session close and actual Rule 201 trigger semantics.

## W27V-M15 — SSR Duration State
Track remainder-of-day + following-trading-day restriction and re-trigger extensions.

## W27V-M16 — Short-Exempt Separation
Short-exempt trades/orders are not equivalent to constrained ordinary shorts.

## W27V-M17 — Regression-Discontinuity Design
For Rule 201 causal research compare stocks just above/below the -10% trigger threshold under matched timing/regime conditions.

## W27V-M18 — Options Substitution Control
Options evidence is valid only when options remain tradable/liquid and contract terms are unaffected.

## W27V-M19 — Endogeneity Guard
LULD/SSR occur because prices moved sharply.

Any claimed post-trigger effect must separate regulatory mechanics from the underlying shock.

## W27V-M20 — Mechanical Intermediate Gate
Before directional alpha, require OOS prediction of:
pause,
auction extension,
reopen price,
repeat pause,
flow migration,
basis distortion,
or liquidity normalization.
