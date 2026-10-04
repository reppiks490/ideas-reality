# Wave 62C — Research Methods

Namespace: **W62C**

## W62C-M01 — COT Release Lag
Tuesday positions are usually published Friday 3:30 p.m. ET.
Backtests use publication time, never Tuesday as information availability.

## W62C-M02 — Holiday/Delay Calendar
Use actual CFTC release schedule/publication timestamp.

## W62C-M03 — Contract Identity
Map exact CFTC market code to exchange contract.
Do not blend mini/micro/related contracts without explicit logic.

## W62C-M04 — Category Semantics
TFF and Disaggregated categories differ.
Never map "leveraged funds" directly to "managed money" as identical populations.

## W62C-M05 — Classification Revision Risk
CFTC notes trader classification can change as new information arrives.
Version definitions and detect structural breaks.

## W62C-M06 — Spreading Separation
Spreading is economically distinct from outright directional risk.

## W62C-M07 — Gross vs Net
Preserve both gross and net concentration.

## W62C-M08 — Trader Count Suppression
Counts under confidentiality thresholds may be suppressed.
Missing count is not zero.

## W62C-M09 — OI Denominator
Use report-date open interest corresponding to CFTC snapshot.

## W62C-M10 — Futures+Options Semantics
Combined reports convert options to futures-equivalent under CFTC methodology; do not mix raw option OI.

## W62C-M11 — Public Reporting API Vintage
Archive exact CFTC dataset state/file at release.

## W62C-M12 — Current-Position Uncertainty
Between Tuesday and Friday/current date, treat position as latent.

## W62C-M13 — Physical State Alignment
Compare COT only to physical information public by the COT publication time.

## W62C-M14 — Price-Endogeneity Guard
Position changes and returns are jointly determined.
Do not claim causality from correlation.

## W62C-M15 — Roll/Expiry Control
Position changes around futures roll can be mechanical.

## W62C-M16 — Cross-Contract Aggregation
Aggregate related contracts only with documented conversion/coverage.

## W62C-M17 — Bank Participation Lag
BPR is monthly, based on first Tuesday and released first Friday under current schedule.

## W62C-M18 — Confidentiality/Composition Change
Bank counts and participant mix can change; concentration shifts may reflect entry/exit.

## W62C-M19 — Extreme-State Pre-Registration
Set crowding thresholds before outcome testing.

## W62C-M20 — Incremental Promotion Gate
Promote only if crowding/concentration adds OOS information beyond:
price trend,
volatility,
OI,
and physical/fundamental state.
