# Wave 27V — Volatility Constraint & Reopening Mechanics

Namespace: **W27V**

Thesis: market structure changes discontinuously when a security touches a regulatory price band, enters a trading pause, becomes subject to a short-sale price test, or must reopen through an auction. During those states, ordinary order-flow relationships are no longer stationary. Price discovery can migrate into index futures, ETFs, options, related securities, and reopening-auction indications.

The research target is the state transition itself and the resulting displacement of price discovery—not a naive rule that a halt is bullish or bearish.

All candidates are hypotheses for Claude to test later. No ICARUS implementation is performed here.

## W27V-E01 — LULD Distance-to-Band Hazard

Primary source:
Limit Up Limit Down Plan + SIP price-band data.

For every NMS stock compute:
distance_to_upper_band,
distance_to_lower_band,
distance normalized by short-horizon volatility,
distance normalized by displayed/deep liquidity.

Output:
NORMAL
BAND_APPROACH
AT_BAND
LIMIT_STATE.

Priority: S

## W27V-E02 — 15-Second Limit-State Survival Hazard

Under the LULD Plan, a qualifying Limit State that does not resolve within 15 seconds can become a Trading Pause.

Research:
P(pause | entered limit state)
conditioned on:
side,
queue size,
cancellations,
executions,
spread,
recent sweep intensity,
market volatility,
index weight.

Priority: S

## W27V-E03 — LULD Reference-Price Drift State

LULD bands are based on a rolling five-minute arithmetic mean of eligible reported transactions, with rule-defined reference-price update behavior.

Feature:
last trade / reference price
and
reference-price update pressure.

Question:
Does slow-moving reference price create predictable changes in distance-to-band during very fast moves?

Priority: A+

## W27V-E04 — Tier / Time-of-Day Band Regime

LULD parameters depend on security tier, price and time of day, including wider bands late in the session under current rules.

Explicitly encode:
Tier 1 / Tier 2,
price bucket,
normal vs doubled-band window.

Priority: A

## W27V-E05 — Halted Constituent Stale-Index Distortion

When an index constituent stops trading while ES/NQ/ETF/options markets continue moving, the published cash-index contribution can become stale.

Candidate:
latent_component_value
-
last_cash_component_value

weighted by index weight.

Aggregate across simultaneously halted constituents.

Priority: S

## W27V-E06 — NQ Stale Mega-Cap Basket

Specialize W27V-E05 to high-weight Nasdaq-100 constituents.

Fuse:
NQ futures,
QQQ,
sector/peer returns,
options-implied move,
last cash price.

Output:
estimated latent contribution of halted NDX constituents.

Priority: S

## W27V-E07 — ES Stale-Constituent Basket

Same architecture for S&P 500 / ES.

Use index weights effective at that point in time.

Priority: S-

## W27V-E08 — Futures-as-Shadow-Price During Halt

Question:
When cash constituent trading pauses, do index futures/ETF/options imply a statistically useful range for the halted security's latent value?

Do not assume a one-to-one mapping.

Use factor exposure, sector, index weight and idiosyncratic uncertainty.

Priority: S

## W27V-E09 — Peer Basket Shadow Price

Estimate halted security latent move from:
sector peers,
industry peers,
supplier/customer graph,
market beta,
factor exposures.

Compare against futures/options implied estimates.

Priority: A+

## W27V-E10 — Option-Implied Shadow Price

Where options remain tradable under applicable rules/data:
derive a bounded latent underlying estimate from:
put-call relationships,
near-delta-neutral structures,
IV skew,
synthetic forward.

Hard requirement:
respect stale underlying, wide spreads and option halts.

Priority: A+

## W27V-E11 — Multi-Market Shadow-Price Consensus

Fuse:
index futures,
ETF,
peer basket,
options,
ADR/foreign line where lawful and open.

Output:
latent price interval + confidence.

Priority: S

## W27V-E12 — Reopening Auction Gap

Feature:
reopening auction price
-
last pre-pause eligible trade.

Decompose expected portion from W27V-E11 and residual surprise.

Priority: S

## W27V-E13 — Halt Auction Imbalance Pressure

Primary exchanges disseminate auction-state information under their rules/products.

Research:
indicative match price,
imbalance,
matched shares,
collar,
extension state.

Question:
Does imbalance add information beyond the cross-market shadow price?

Priority: S

## W27V-E14 — Reopening Collar Proximity

For exchanges with published LULD reopening-collar mechanics:
distance of indicative auction price to active collar.

State:
INSIDE
AT_COLLAR
OUTSIDE_COLLAR
COLLAR_WIDENING.

Priority: S-

## W27V-E15 — Reopen Extension Hazard

Cboe and other primary-listing exchanges use rule-defined extension logic when reopening criteria are unmet.

Estimate:
P(auction extends another interval)
from imbalance, indicative price, collar proximity and queued order state.

Priority: A+

## W27V-E16 — Collar-Widening Release

Each auction extension can widen the allowable reopening range under current rule mechanics.

Feature:
new allowable range
-
prior allowable range.

Research whether liquidity/price discovery jumps immediately after each widening.

Priority: A+

## W27V-E17 — Late-Day Volatility Close Transition

Current LULD mechanics include special handling for pauses near the close; some venues transition the halted security into a closing/volatility auction rather than ordinary reopening.

State:
INTRADAY_REOPEN
vs
VOLATILITY_CLOSE.

Priority: S-

## W27V-E18 — Halt Cluster Breadth

Aggregate simultaneous LULD pauses by:
index,
sector,
ETF basket,
factor,
market cap.

Feature:
halted index weight
× directional concentration.

Use as a market-structure stress indicator.

Priority: S

## W27V-E19 — Halt Contagion Graph

Graph:
initial paused security
-> peers
-> ETFs
-> index constituents
-> related options
-> futures.

Target:
probability of additional LULD transitions in related names.

Priority: A+

## W27V-E20 — ETF Creation-Arbitrage Impairment During Component Halt

When ETF components are halted, ordinary arbitrage can become less precise because a component cannot be transacted at its latent value.

Research:
ETF premium/discount
× halted basket weight
× AP substitution/fair-value uncertainty.

Priority: A+

## W27V-E21 — Rule 201 Trigger State

Primary source:
SEC Regulation SHO Rule 201 + exchange circuit-breaker lists.

Trigger:
covered security down at least 10% from prior regular-session close.

Restriction:
short-sale price test applies for remainder of trigger day and following trading day, subject to exceptions.

Priority: S-

## W27V-E22 — Rule 201 Short-Flow Suppression

Recent quasi-experimental research finds Rule 201 materially reduces short-sale activity around the threshold.

Research point-in-time:
short volume before/after trigger
relative to near-threshold controls.

Priority: S-

## W27V-E23 — Rule 201 Ask-Depth Migration

Mechanism evidence suggests constrained short sellers may shift away from marketable sells toward passive ask-side liquidity.

Feature:
ask depth change
-
matched near-threshold control.

Priority: A+

## W27V-E24 — Rule 201 × Options Synthetic-Short Migration

Published research finds option-market behavior changes around Rule 201 triggers and documents put-call parity distortions consistent with synthetic-short substitution.

Research:
options volume/skew/parity residual
after Rule 201 trigger.

Priority: S-

## W27V-E25 — LULD × Rule 201 Collision

A stock can be under both:
volatility-band constraints
and
Rule 201 short-sale restriction.

Output:
NORMAL
SSR_ONLY
LULD_ONLY
SSR_PLUS_LULD
HALTED_UNDER_SSR.

Question:
Does the combined state alter reopening liquidity/price dynamics?

Priority: S

## W27V-E26 — Constraint Migration Index

Measure where price discovery migrates while cash trading is constrained.

Possible destinations:
futures,
ETF,
options,
peer equities,
ADRs,
credit.

Output weights sum to one with uncertainty.

Priority: S

## W27V-E27 — Reopening Price Discovery Error

Compare each pre-reopen shadow-price source to realized reopening price.

Track which market is most informative by:
halt cause,
duration,
stock type,
index weight,
volatility regime.

Priority: S

## W27V-E28 — Halt Cause Taxonomy

Separate:
LULD
NEWS_PENDING
NEWS_DISSEMINATED
REGULATORY
OPERATIONS
IPO
CORPORATE_ACTION
MARKET_WIDE
OTHER.

Never pool all halts into one alpha feature.

Priority: S methodology/edge hybrid

## W27V-E29 — Operational vs Regulatory Halt Divergence

2026 exchange rule harmonization clarifies primary-market regulatory halts and exchange-specific operational halts.

Research:
single-venue impairment vs marketwide/securitywide halt.

Priority: A

## W27V-E30 — Market-Wide Circuit Breaker State

Track Level 1 / Level 2 / Level 3 market-wide circuit-breaker states independently from single-stock LULD.

Research:
futures/cash/options liquidity and reopening dynamics by state.

Priority: A+

## W27V-E31 — Halted-Weight Futures Basis Pressure

Candidate:
halted index weight
× latent halted-component move
× remaining tradable hedge demand.

Target:
ES/NQ cash-futures/ETF basis behavior during clustered constituent pauses.

Priority: S

## W27V-E32 — Reopening Shock Absorption Ratio

RSAR =
reopening net information shock
/
auction + immediate post-reopen liquidity capacity.

Question:
When does reopening clear cleanly versus cascade into another limit state/pause?

Priority: S

## W27V-E33 — Repeat-Pause Hazard

Estimate:
P(second LULD pause within N minutes | reopened).

Inputs:
reopen price,
collar distance,
imbalance,
latent-price uncertainty,
post-reopen depth,
remaining news shock.

Priority: S-

## W27V-E34 — Constraint-Release Half-Life

After SSR expiration or LULD reopening:
measure how quickly:
short-flow,
spread,
depth,
volatility,
ETF premium,
futures basis
normalize.

Priority: A+

## W27V-E35 — Mechanical Constraint State Vector

Create a state vector for every equity:
LULD distance/state,
halt type,
Rule 201 status,
auction state,
index weight,
options status,
ETF membership,
cross-market shadow-price confidence.

This is a conditioning layer, not a standalone trading signal.

Priority: S

## Highest-priority W27V tests

1. W27V-E02 15-Second Limit-State Survival Hazard
2. W27V-E05 Halted Constituent Stale-Index Distortion
3. W27V-E06 NQ Stale Mega-Cap Basket
4. W27V-E11 Multi-Market Shadow-Price Consensus
5. W27V-E13 Halt Auction Imbalance Pressure
6. W27V-E15 Reopen Extension Hazard
7. W27V-E24 Rule 201 × Options Synthetic-Short Migration
8. W27V-E25 LULD × Rule 201 Collision
9. W27V-E31 Halted-Weight Futures Basis Pressure
10. W27V-E32 Reopening Shock Absorption Ratio
