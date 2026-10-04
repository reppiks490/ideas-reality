# Wave 12F — Research Methods

Namespace: **W12F**

## W12F-M01 — Port-Time Residualization
For each border crossing/lane model expected wait by:
hour, weekday, season, holiday, lane type and operating schedule.

Use residual delay, not raw minutes.

## W12F-M02 — Wait-Time Freshness Gate
Every observation stores:
source update time
first seen time
ingest time
port status.

Stale/Update Pending/Lanes Closed are distinct from zero delay.

## W12F-M03 — Slow Baseline / Fast State Separation
BTS validated crossing counts are slow historical context.
CBP Border Wait Times are current operational state.

Never backfill a current wait model with BTS data not yet published at the historical decision date.

## W12F-M04 — Crossing Importance Weight
Estimate historical importance from inbound truck/container counts and economic-corridor mapping.

Do not assume every port has equal economic impact.

## W12F-M05 — Directionality Boundary
BTS Border Crossing/Entry counts are inbound to the United States.

Do not infer outbound physical flow from an inbound-only dataset.

## W12F-M06 — Publication-Time Livestock Ledger
Store LMPR:
report date
published timestamp
retrieval time
correction timestamp
report/section ID.

Use published time as information availability.

## W12F-M07 — Morning/Afternoon Version Control
When USDA publishes multiple same-day livestock reports, preserve each version rather than replacing morning information with the afternoon report.

## W12F-M08 — Purchase-Type Decomposition
Separate negotiated, formula and other purchase categories exactly as source semantics define them.

Do not merge them to increase sample size unless the economic question supports it.

## W12F-M09 — Thin-Benchmark Effective Sample Size
Measure information content using transaction/volume concentration and negotiated share, not only nominal report row count.

## W12F-M10 — Settlement-Definition Versioning
Cash-settled futures/index inputs and physically delivered contract rules can change.

Backtests must use the settlement methodology/rules effective at that date.

## W12F-M11 — Deterministic Rule Engine
Encode exchange rules as explicit state transitions:
inputs -> rule predicate -> next-session state.

Unit-test against historical exchange notices.

## W12F-M12 — Rule Change vs Rule Activation
Separate:
rule announcement,
effective date,
periodic reset,
daily trigger activation,
expiry-specific transition.

## W12F-M13 — Cross-Product Trigger Graph
Represent products connected by exchange rule dependencies.

A limit settlement in one node may mechanically alter another node's next-session range.

## W12F-M14 — Limit-State Endogeneity Control
Price limits trigger because prices moved.

Use matched large-move non-trigger days, near-threshold days and cross-contract controls before attributing subsequent effects to the rule state.

## W12F-M15 — Position-Compression Clock
Compute exact time until each spot-month step-down/effective limit using the historical rule version.

No hand-written generic "days to expiry" proxy.

## W12F-M16 — Certificate-Limit Action Window
For delivery-limit research encode the legally allowed correction window after excess certificates are received.

Test only information actually observable publicly/through licensed delivery reports.

## W12F-M17 — Clearing Firm != Beneficial Owner
Issues/stops identify clearing-side categories, not necessarily ultimate economic owner.

Prohibit beneficial-owner narratives absent evidence.

## W12F-M18 — Delivery and Futures Double-Count Guard
Spot-month futures positions and delivery/certificate holdings can have separate limits.

Model them as separate states unless the rule explicitly aggregates them.

## W12F-M19 — Recovery-Curve Validation
For border/logistics constraints measure whether physical throughput actually normalizes after wait times recover.

A shorter queue does not prove backlog cleared.

## W12F-M20 — Composite Incrementality Test
W12F-E22 promotes only if freight, cash-market and rule-state components each add OOS information beyond the others and beyond price/volatility baselines.
