# Wave 62C — Futures Positioning, Crowding & Concentration

Namespace: **W62C**

Thesis: public CFTC reports expose slow but high-integrity snapshots of who holds risk in U.S. futures markets. The edge is not a folk rule like "commercials are smart money." It is the interaction between **position concentration, category crowding, gross-versus-net exposure, positioning revisions, physical fundamentals, and the market's ability to absorb forced de-risking**.

All candidates are research hypotheses only. Claude owns later implementation.

## W62C-E01 — TFF Leveraged-Fund Net Crowding
Primary source:
CFTC Traders in Financial Futures.

For NQ/ES/Treasuries/FX/VIX and other covered financial contracts:
leveraged-fund net position / open interest.

Priority: S

## W62C-E02 — Asset-Manager / Institutional Positioning
Track directional and spreading exposure of asset-manager/institutional category separately from leveraged funds.

Priority: S-

## W62C-E03 — Dealer / Intermediary Inventory State
Dealer/intermediary category can reflect sell-side accommodation and hedging.

Research interaction with client-side crowding rather than directional interpretation alone.

Priority: A+

## W62C-E04 — Leveraged-Fund Position Change Shock
Feature:
weekly change in leveraged long/short/net
normalized by open interest and historical distribution.

Priority: S

## W62C-E05 — Gross Crowding vs Net Crowding
Large balanced gross positions can be hidden by small net.

Track:
gross_long + gross_short,
net,
spreading
separately.

Priority: S

## W62C-E06 — Top-4 Trader Gross Concentration
Use long-format COT concentration:
largest 4 reportable traders' gross long/short share.

Priority: S

## W62C-E07 — Top-8 Trader Gross Concentration
Same for largest 8.

Priority: A+

## W62C-E08 — Net Concentration
Compare top-4/top-8 net concentration with gross concentration.

A highly concentrated directional book differs from large balanced intermediation.

Priority: S

## W62C-E09 — Concentration Acceleration
Feature:
week-over-week change in top-4/top-8 concentration.

Priority: A+

## W62C-E10 — Trader-Count Compression
Where CFTC reports trader counts:
declining number of active traders while position size stays high may indicate crowding.

Priority: A+

## W62C-E11 — Category Share of Open Interest
Compute each reportable category's long, short, spreading shares relative to total OI.

Priority: S-

## W62C-E12 — Futures-Only vs Futures+Options Gap
Compare category exposure in futures-only and combined reports.

Use as a coarse options-overlay state, not a substitute for strike-level options data.

Priority: A

## W62C-E13 — Disaggregated Managed-Money Crowding
For physical commodities:
managed money long/short/spreading by contract.

Priority: S

## W62C-E14 — Producer/Merchant Hedge Pressure
Track producer/merchant/processor/user gross positioning.

Interpret as physical-commercial risk management, not automatically predictive direction.

Priority: S-

## W62C-E15 — Swap-Dealer Hedge Transfer
Track swap-dealer position changes as a potential mirror of OTC/client risk transfer.

Fuse with W38 OTC derivatives where possible.

Priority: A+

## W62C-E16 — Physical-vs-Paper Divergence
Compare CFTC managed-money direction to repo physical truth:
inventories,
flows,
production,
shipping,
constraints.

States:
PAPER_CONFIRMS_PHYSICAL
PAPER_EUPHORIA
PAPER_PANIC
PHYSICAL_SHOCK_UNPOSITIONED.

Priority: S

## W62C-E17 — Physical Shock into Crowded Opposite Position
Example:
bullish physical disruption
while managed money is heavily short.

Estimate squeeze/forced-cover hazard.

Priority: S

## W62C-E18 — Physical Recovery into Crowded Long
Inverse state:
funds remain heavily long after physical constraint resolves.

Priority: S

## W62C-E19 — Positioning Revision Velocity
COT changes are weekly.
Track first and second differences plus percentile state.

Priority: A+

## W62C-E20 — Positioning Persistence
Measure consecutive weeks above crowding threshold.

Persistent crowding may behave differently from one-week extremes.

Priority: A

## W62C-E21 — Crowding × Realized Volatility
Same net position has different liquidation risk under low vs rising volatility.

Priority: S-

## W62C-E22 — Crowding × Margin Pressure
Fuse with exchange margin changes / W39 fund fragility where available.

Priority: S

## W62C-E23 — Crowding × Liquidity Capacity
Estimate crowded notional relative to market depth/ADV/open interest.

Priority: S

## W62C-E24 — Positioning Shock Absorption Ratio
PSAR =
weekly category position change
/
expected market risk-transfer capacity.

Priority: S

## W62C-E25 — Bank Participation Gross Long/Short
Primary source:
CFTC Bank Participation Report.

Track U.S. and non-U.S. bank gross long/short futures exposure.

Priority: S-

## W62C-E26 — Bank Concentration Regime
Feature:
bank-position share of OI
× bank count
× U.S./non-U.S. split.

Priority: A+

## W62C-E27 — Gold Bank Short Concentration
Specialize BPR for COMEX gold/silver.

Track:
bank gross short % OI,
gross long % OI,
bank count,
monthly change.

Do not infer manipulation from concentration alone.

Priority: S

## W62C-E28 — NQ/ES Bank vs Fund Positioning Gap
Compare monthly bank participation with weekly TFF leveraged/asset-manager states.

Priority: A+

## W62C-E29 — Cross-Asset Crowding Cluster
Aggregate crowded same-direction positions across:
NQ,
ES,
Treasuries,
USD,
gold,
oil,
VIX
after volatility scaling.

Priority: S

## W62C-E30 — Crowded Macro Narrative State
Identify whether several markets imply one common macro bet:
risk-on,
risk-off,
disinflation,
inflation,
growth,
USD.

Priority: S-

## W62C-E31 — Crowding Unwind Cascade Graph
Graph likely forced-risk propagation:
rates
-> equities
-> FX
-> commodities
-> volatility.

Priority: S

## W62C-E32 — COT Release Surprise
Because positions are stale by publication time, compare reported Tuesday position to what market/flow proxies implied by Friday release.

Target:
unexpected historical positioning state, not current exact position.

Priority: A

## W62C-E33 — Position Extrapolation Uncertainty
Estimate current post-Tuesday position as a distribution using:
price,
volume,
OI changes,
fund-flow proxies,
options,
not as fact.

Priority: S architecture

## W62C-E34 — Positioning Truth Ladder
TUESDAY POSITION
-> FRIDAY PUBLICATION
-> CURRENT POSITION DISTRIBUTION
-> PHYSICAL/FUNDAMENTAL STATE
-> LIQUIDITY/MARGIN
-> FORCED UNWIND / ABSORPTION
-> PRICE RESPONSE.

Priority: S architecture

## Highest-priority W62C tests

1. W62C-E04 Leveraged-Fund Position Change Shock
2. W62C-E05 Gross vs Net Crowding
3. W62C-E06 Top-4 Gross Concentration
4. W62C-E08 Net Concentration
5. W62C-E16 Physical-vs-Paper Divergence
6. W62C-E17 Physical Shock into Crowded Opposite Position
7. W62C-E22 Crowding × Margin Pressure
8. W62C-E24 Positioning Shock Absorption Ratio
9. W62C-E27 Gold Bank Short Concentration
10. W62C-E31 Crowding Unwind Cascade Graph
