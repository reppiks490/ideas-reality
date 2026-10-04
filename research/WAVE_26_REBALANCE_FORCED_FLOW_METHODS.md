# Wave 26R — Research Methods

Namespace: **W26R**

## W26R-M01 — Index Announcement Vintage
Archive exact public announcement time, effective date and every revision.

## W26R-M02 — Provider Methodology Versioning
S&P/Nasdaq/Russell methodologies change. Use the rule version active on the historical date.

## W26R-M03 — Target-Weight Reconstruction
Reconstruct index target weights using point-in-time shares, float and provider rules.

Do not use current weights retrospectively.

## W26R-M04 — Tracking-Assets Uncertainty
Represent passive/tracking assets as an interval.

"Assets benchmarked to" != forced one-for-one passive assets.

## W26R-M05 — Origin/Destination Netting
For index migrations, calculate tracker selling from origin and buying into destination before defining net flow.

## W26R-M06 — Sponsor Holdings Vintage
ETF holdings/AUM/shares-outstanding data must be archived daily if used. Current sponsor pages cannot reconstruct all past states.

## W26R-M07 — Corporate-Action Neutralization
M&A, spin-offs, bankruptcies and other actions can drive returns independently of index flow.

Classify and control.

## W26R-M08 — Closing-Auction Baseline
Expected close liquidity is conditioned on:
security,
weekday,
month/quarter end,
volatility,
triple-witching,
recent volume,
prior rebalance days.

## W26R-M09 — Auction-Time Clock
Separate last continuous trade, imbalance publication, auction cutoff, closing print and post-close trading.

## W26R-M10 — Pre-Positioning Measurement
Measure abnormal return/volume/borrow before effective date.

Do not attribute full event-window move to passive funds.

## W26R-M11 — Preliminary-List Probability
For Russell/Nasdaq candidate prediction, freeze eligibility/rank inputs at the actual public reference date.

## W26R-M12 — Revision-as-New-Information
Each preliminary-list update or provider announcement revision is a separate event.

## W26R-M13 — Weight Redistribution Conservation
When capped index weights change, ensure removed weight is redistributed exactly under methodology; total target weights must reconcile.

## W26R-M14 — Futures Contract Identity
Use exact contract months. Continuous series are unsuitable for studying roll mechanics without underlying contract OI/volume.

## W26R-M15 — Roll Progress Curve
Normalize nearby/deferred OI migration by time-to-expiry and historical contract-specific patterns.

## W26R-M16 — SOQ Component Clock
For expiry settlement, track which component has actually opened. Do not substitute prior close as if it were the SOQ opening print.

## W26R-M17 — Option OI Upper-Bound Logic
Open interest is not guaranteed exercise quantity.

Treat moneyness-based assignment as scenario bounds.

## W26R-M18 — Ex-by-Ex Rule State
Version OCC exercise thresholds, special memos and adjusted-deliverable rules historically.

## W26R-M19 — Event Collision Decomposition
Quarterly rebalances often coincide with futures/options expiration.

Use matched/control designs to separate index-flow effect from generic expiration effect.

## W26R-M20 — Financial Promotion Gate
Promote only after OOS prediction of:
auction volume/impact,
tracker holdings change,
roll migration,
basis,
or other mechanical intermediate outcome.
