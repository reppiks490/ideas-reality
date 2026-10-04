# Wave 3 Research Methods

## M41 — Venue-Leader State Estimation
For multi-venue assets such as BTC:
estimate rolling directed influence among CME, regulated spot, ETF-related state, and offshore perpetual markets.

Use lagged conditional models, not contemporaneous correlation.

Output:
leader probability by venue and horizon.

## M42 — Market-Structure Change Audit
Before reusing historical crypto or microstructure edges:
split sample around major structural changes:
ETF launch,
24/7 regulated futures changes,
new margin rules,
venue dominance shifts,
fee/microstructure changes.

A signal that only worked under a previous market architecture is not current alpha.

## M43 — Public-Chain Reproducibility Standard
For on-chain signals:
publish exact contract addresses, event types, chain height/block timestamps, bridge rules, mint/burn rules, reorg handling and entity-label dependencies.

If an edge requires unverifiable vendor heuristics, classify it PROPRIETARY_HEURISTIC.

## M44 — Chain Reorganization / Finality Safety
Event_time != finality_time.

For crypto:
record block timestamp, observed time, confirmation/finality threshold and any reorg correction.

Backtests cannot assume final data instantly.

## M45 — Cross-Venue Clock Normalization
Normalize:
exchange timestamps,
block timestamps,
ETF market hours,
CME session/settlement,
offshore 24/7 venue clocks.

Prevent fake lead-lag from mismatched timestamp conventions.

## M46 — Physical Balance Reconciliation
For commodities:
every balance model must reconcile approximately:

beginning inventory
+ production
+ imports
- domestic demand
- exports
= ending inventory

Residual becomes a data-quality diagnostic, not hidden model noise.

## M47 — Intermediate-Target First
For natural gas:
predict storage/physical balance before price.

For ports:
predict import/inventory KPI before stocks.

For patents:
predict future innovation/commercial KPI before returns.

For stablecoins:
predict venue/chain liquidity before BTC return.

Promotion requires passing the intermediate mechanism test where feasible.

## M48 — Forced-Flow Identification
Label candidate mechanisms by whether they can create mechanically forced trading:
dealer delta hedge,
ETF creation/redemption,
margin/liquidation,
auction/dealer inventory,
index rebalance,
storage/physical constraints.

Prioritize forced-flow edges over vague sentiment.

## M49 — Opposite-Sign Mechanism Test
Commodity events often have opposite local/global effects.

Example:
LNG terminal outage can reduce U.S. feedgas demand (domestically bearish gas) while tightening global LNG supply.

Every event model must enumerate competing causal signs before data fitting.

## M50 — Event Availability Ladder
For innovation/regulation:
filing/application date
public-inspection/publication date
market ingestion time
later grant/effective date.

Only public availability is legal for historical features.

## M51 — Delayed-Outcome Validation
Some alternative data have fast observations but slow economic consequences.

Estimate response curve:
5m, 1h, 1d, 1w, 1m where appropriate.

Do not force all data into intraday prediction.

## M52 — Mechanism-Specific Half-Life
Edge decay should reflect mechanism.

Examples:
order-book refill: seconds/minutes
Federal Register event: minutes/days
port manifests: days/weeks
patent pipeline: weeks/months

Use different validation horizons by causal process.

## M53 — Data Rights Classification
Every source:
PUBLIC_COMMERCIAL_OK
PUBLIC_NONCOMMERCIAL
PUBLIC_WITH_ATTRIBUTION
ACCOUNT_REQUIRED
PAID
PROPRIETARY
FUTURE
TERMS_REVIEW_REQUIRED

Research output must not imply production rights.

## M54 — Source Substitution Test
If an edge only works with one opaque vendor, attempt reproduction with an independent source.

Examples:
vendor stablecoin flow -> raw chain events
vendor ETF flow -> issuer shares/holdings
vendor gas flow -> official EIA/FERC proxies

A reproducible weaker edge may be preferable to an opaque stronger one.

## M55 — Causal Disagreement Research
Specifically search for states where independent channels disagree.

Examples:
BTC CME basis bullish, stablecoin liquidity contracting.
Strong export sales, river logistics constrained.
Hot weather demand, LNG terminal offline.
Positive patent novelty, weak corporate capex.

Hypothesis:
disagreement may forecast volatility, regime transition or model failure even when direction is ambiguous.
