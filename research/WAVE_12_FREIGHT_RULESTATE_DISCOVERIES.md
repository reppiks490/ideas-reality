# Wave 12F — Freight, Livestock & Exchange Rule-State

Namespace: **W12F**

Thesis: price formation changes when the physical movement of goods is constrained, when mandatory cash-market transactions reveal the underlying benchmark, or when exchange rules mechanically change what positions/prices are legally possible. These states are observable and often deterministic.

All candidates are hypotheses for Claude to falsify later. This repository remains research-only.

## W12F-E01 — Commercial Border Delay Field

Primary source:
U.S. Customs and Border Protection Border Wait Times.

Status:
LIVE public operational data.

CBP publishes commercial-vehicle wait state by land port/crossing, including General and FAST lanes where available, open lanes, operating hours and update timestamps.

Build:
- wait-minutes residual by crossing/hour/day
- open-lane fraction
- delay persistence
- queue acceleration
- port-closure indicator
- update staleness
- northern vs southern border breadth.

Mechanism:
This measures an actual impediment to cross-border truck throughput.

Targets:
autos/parts, industrial supply chains, agriculture/perishables and regional logistics before any broad-index use.

Priority: S-

## W12F-E02 — FAST vs General Commercial-Lane Divergence

At ports where both lane types exist:

feature =
General wait
-
FAST wait

Interpretation:
A large divergence may distinguish general processing congestion from a broad physical crossing-capacity problem.

Condition on:
lanes open, time of day, port and trusted-trader lane availability.

Priority: A

## W12F-E03 — Border Delay × Throughput Importance

Source pairing:
live CBP wait times + BTS validated Border Crossing/Entry history.

BTS provides port-level monthly inbound trucks, trains, loaded/empty truck containers and rail containers, but the validated series can have substantial publication lag.

Use BTS only to estimate historical port importance/seasonality.

Candidate:
impact_pressure =
live_delay_residual
× historical_port_throughput_weight.

Priority: S-

## W12F-E04 — Cross-Border Industrial Exposure Graph

Graph:
port/crossing
-> commodity/industry corridor
-> OEM/factory/distribution region
-> public issuer exposure.

Start with well-documented corridors:
automotive, appliances/electronics, produce, energy equipment and industrial components.

Hard requirement:
no issuer exposure without sourced geography/supply-chain evidence.

Priority: A+

## W12F-E05 — Border Congestion Recovery Half-Life

Measure:
onset
peak wait
lane reopening
50% normalization
90% normalization
post-event throughput catch-up.

Hypothesis:
recovery path may matter more than peak wait for production interruption risk.

Priority: A

## W12F-E06 — Multimodal Border Substitution State

Fuse:
truck-border constraints
+ rail service
+ rail-container flow
+ nearby port/air alternatives where economically relevant.

Output:
NO_SUBSTITUTE / PARTIAL_SUBSTITUTE / ROUTE_MIGRATION / NORMAL.

Question:
Does alternative capacity absorb the shock before inventories/production are affected?

Priority: A+

## W12F-E07 — Mandatory Cattle Cash Pulse

Primary source:
USDA Agricultural Marketing Service Livestock Mandatory Reporting API/DataMart.

Status:
LIVE public mandatory market reporting.

Official API exposes reports including 5-Area Daily Weighted Average Direct Slaughter Cattle — Negotiated.

Features:
- negotiated price residual
- negotiated volume
- live vs dressed basis
- regional breadth
- morning/afternoon revision
- purchase-type mix
- delivery-period structure.

Priority: S-

## W12F-E08 — Mandatory Hog Cash Pulse

Source:
USDA LMPR.

Build:
- negotiated hog price/volume
- Swine/Pork Market Formula state
- negotiated-formula state
- purchase-type mix
- regional cash dispersion
- cash-to-CME index/futures basis.

Priority: S-

## W12F-E09 — Negotiated Benchmark Fragility

Recent empirical work using daily LMR data documents that lean-hog cash/futures convergence worsens as the share of negotiated transactions becomes thinner.

General candidate:
benchmark_fragility =
1 / effective_negotiated_volume_share

Then test:
basis error
× benchmark fragility
× expiry proximity.

Do not assume the same mechanism transfers from hogs to cattle; test separately.

Priority: S

## W12F-E10 — Cash-Futures Convergence State

For cattle/hogs:

states:
CASH_LEADS
FUTURES_LEADS
CONVERGING
DIVERGING
THIN_BENCHMARK
EXPIRY_CONVERGENCE_FAILURE.

Use mandatory cash prices/volumes and exact futures settlement rules.

Priority: S

## W12F-E11 — Boxed-Meat Margin Transmission

Sources:
USDA mandatory/Market News cattle/hog procurement
+ boxed beef/pork reports
+ feed costs
+ futures.

Construct approximate economic chain:
livestock acquisition cost
-> wholesale cutout
-> packer spread
-> cash procurement response
-> futures basis.

Goal:
measure who absorbs a demand/supply shock.

Priority: A+

## W12F-E12 — LMR Correction / Revision State

USDA APIs/public notices expose correction-aware reporting.

Track:
original publication
-> correction
-> revised fields
-> correction magnitude
-> time-to-correction.

Research:
whether unusually large corrections indicate stressed/thin markets or only clerical noise.

Hard rule:
backtests use the original value until correction-publication time.

Priority: B+

## W12F-E13 — CME Price-Limit State Machine

Primary source:
CME/CBOT rulebooks and daily price-limit pages.

Represent each contract session as:
NORMAL_INITIAL_LIMIT
LIMIT_SETTLEMENT
EXPANDED_NEXT_DAY
MULTI_DAY_EXPANSION
REVERSION
SPOT_LIMIT_REMOVED
DYNAMIC_HALT where applicable.

This is deterministic from exchange rules and settlement state.

Priority: S

## W12F-E14 — Cross-Contract Limit Trigger Graph

Exchange rules can propagate a limit state across related products.

Examples documented by CME:
- Soybeans / Soybean Meal / Soybean Oil can cross-trigger expanded limits
- Chicago Wheat / KC HRW Wheat can cross-trigger
- Live Cattle and Feeder Cattle can trigger expanded limits across the paired livestock complex.

Research:
Does the mechanically expanded opportunity set alter overnight liquidity, option pricing, basis or next-session gap behavior?

Priority: S

## W12F-E15 — Next-Session Price-Bound Expansion

Feature known after qualifying settlement:
tomorrow's permitted price range / today's permitted range.

Question:
Does a newly wider legal price range change:
depth,
overnight gap,
market-order impact,
options skew,
liquidity provision?

Do not interpret expansion itself as directional.

Priority: A+

## W12F-E16 — Price-Limit × Margin-Shock Interaction

Fuse:
W12F-E13 exchange price-limit state
+ W11C-E05/E06 margin requirement shock.

Mechanism:
One rule expands/restricts reachable prices while another changes collateral required to hold risk.

Research:
whether simultaneous margin and price-limit changes create nonlinear deleveraging/liquidity effects.

Priority: S

## W12F-E17 — Spot-Month Position Compression Clock

Source:
CME rules / monthly spot-limit effective-date notices.

Position limits can step down as expiration/delivery approaches depending on product.

Feature:
remaining allowable position
/
pre-compression position/open-interest proxy.

Research:
liquidity and spread effects around *known rule transitions*, distinct from ordinary roll activity.

Priority: A+

## W12F-E18 — Delivery Certificate Capacity Constraint

CME Rule 562 / product rules specify limits on holdings of registered shipping certificates/warehouse receipts for certain CBOT products.

Current 2026 advisory examples include limits for:
corn, wheat, soybeans, oats, soybean oil, rough rice, soybean meal and KC wheat.

State:
certificates outstanding
relative to
permitted ownership concentration
and
nearby delivery/open-interest pressure.

Priority: S-

## W12F-E19 — Forced Retender / Recycle Pressure

CME guidance states that if a participant is stopped for delivery in a quantity that pushes certificate holdings over the applicable limit, the excess must generally be cancelled, retendered or sold by the close of the following business day unless exempt.

Hypothesis:
This rule can create a deterministic short-horizon need to recycle excess delivery instruments.

Research carefully at clearing-firm/aggregate level; do not infer beneficial owner identity from clearing-firm labels.

Priority: S-

## W12F-E20 — Position-Limit Rule-Change Shock

Source:
CME Market Regulation notices + CFTC rule filings.

Examples include increases/decreases in spot-month limits and accountability levels with explicit notice/effective dates.

Test separately:
announcement effect
effective-date effect
position migration
liquidity response
delivery behavior.

Priority: A

## W12F-E21 — First-Notice / Price-Limit-Removal Transition

For some physically delivered contracts, ordinary price limits are removed as the current month approaches delivery/first notice according to product rules.

Feature:
transition from bounded to unbounded daily movement
× OI remaining
× delivery inventory
× basis.

This is a structural regime shift, not a generic expiry dummy.

Priority: A+

## W12F-E22 — Freight × Cash Benchmark × Rule-State Collision

Composite:
physical freight constraint
× mandatory cash-market signal
× exchange price/position/delivery rule state.

Example:
large export demand + river/border/logistics constraint + grain futures entering expanded-limit/delivery regime.

Goal:
identify when fundamental pressure and the market's mechanical ability to absorb/reprice it are simultaneously stressed.

Priority: S

## Highest-priority W12F tests

1. W12F-E01 Commercial Border Delay Field
2. W12F-E03 Border Delay × Throughput Importance
3. W12F-E07 Mandatory Cattle Cash Pulse
4. W12F-E08 Mandatory Hog Cash Pulse
5. W12F-E09 Negotiated Benchmark Fragility
6. W12F-E10 Cash-Futures Convergence State
7. W12F-E13 CME Price-Limit State Machine
8. W12F-E14 Cross-Contract Limit Trigger Graph
9. W12F-E16 Price-Limit × Margin-Shock Interaction
10. W12F-E22 Freight × Cash Benchmark × Rule-State Collision
