# Wave 84X — Research Methods

Namespace: **W84X**

## W84X-M01 — Availability Timestamp for Every Series
Each series stores observation_date, published/last_updated time and first_seen_time; FRED DFII10 shows a one-business-day lag (observed).

## W84X-M02 — Vintage-Safe Daily Macro Joins
Daily macro files are joined to intraday bars only after availability_time; no same-day joins.

## W84X-M03 — Synchronous Clock Alignment
Align all assets to exchange timestamps in UTC, handle maintenance gaps (BTC 16:00-16:02 CT) and Globex breaks explicitly.

## W84X-M04 — Return Definition
Use log returns on a continuous-contract series built with matched roll rules; ETF returns total-return adjusted only in daily tests.

## W84X-M05 — Non-Synchronous Trading Correction
Cash ETFs and futures trade on different clocks; use overlapping windows only and add a Epps-effect test for short horizons.

## W84X-M06 — Rolling Window Parameterisation
All windows (30-min, 60-min, 20-day) are parameters grid-searched on a development period and frozen.

## W84X-M07 — Correlation Estimator Robustness
Compare Pearson, Spearman and shrinkage covariance; report estimator sensitivity before accepting a regime.

## W84X-M08 — Hysteresis and Dwell Rules
Regime changes require enter/exit thresholds and minimum dwell (E50) to avoid flip-flop.

## W84X-M09 — Placebo and Shuffle Controls
Time-shifted series, block-shuffled returns and wrong-asset substitutions for every lead-lag and beta claim.

## W84X-M10 — Event Overlap Masks
Single-event inference only when no other scheduled event is within window.

## W84X-M11 — Sign Ambiguity
Dollar, oil and rate links are explicit about sign dependence by regime; two-sided tests.

## W84X-M12 — Proxy Honesty
Proxies (6E for dollar, ETF pairs for TIPS) are labelled with measured tracking error against the official series when available.

## W84X-M13 — Rights Gate
MOVE, DXY, index data are licensed; production use requires the licence; vendor feeds are never redistributed.

## W84X-M14 — Look-Ahead in PCA
PCA loadings estimated only on past data; rolling refits; no full-sample loadings.

## W84X-M15 — Multiple Testing Family
FDR control across the W84X family; priority list is a reading order.

## W84X-M16 — Cost-Net Evaluation
Regime gates are evaluated by drawdown and slippage reduction, not signal PnL alone.

## W84X-M17 — Out-of-Sample Regime Coverage
Require at least two distinct stock-bond sign regimes and two vol regimes in the sample before promotion.

## W84X-M18 — Minimum Event Counts
FOMC-day and similar event edges: n small, report as underpowered (8 meetings per year, verified in FOMC calendar).

## W84X-M19 — Cross-Wave Deduplication
Cite W62C-E29, W70B-E25, W6N, W76Q before extending; state increment.

## W84X-M20 — Source Kill Rule
PP sources unverified in 30 days are downgraded; dependent edges capped at B.

## W84X-M21 — Structural Break Log
Log product changes (ETF launches, contract spec changes, index methodology).

## W84X-M22 — Latency Realism
Lead-lag lags must exceed measured feed latency and cost before being called tradable.

## W84X-M23 — Promotion Gate
Intermediate-outcome promotion gate: calibration, placebo, cost-net uplift, regime stability, shadow period.

## W84X-M24 — Provenance Language
VERIFIED (page read), SEARCH_VERIFIED (snippet only), PP (pending).
