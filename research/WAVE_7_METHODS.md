# Wave 7 Research Methods

## M111 — Capacity Units First

Translate every constraint into a physical unit:
MW,
Bcf/d,
barrels/day,
transits/day,
tons/day,
TEU/day.

Do not compare percentages across systems without physical scale.

## M112 — Substitute Stack Reconstruction

When capacity disappears, enumerate replacement sources in merit order with:
available capacity,
marginal cost,
ramp speed,
network constraint.

This turns "outage" into a causal substitution estimate.

## M113 — Announced vs Effective Capacity

Store:
announcement time,
effective time,
affected future dates,
later amendment/postponement.

Forward constraints can be tradable information before physical effect begins.

## M114 — Forward-Vintage Archive

Archive every ACP water projection, booking schedule and capacity advisory.

Never backtest with the final known restriction applied retrospectively to an earlier date.

## M115 — Cargo-Capacity Conversion

Convert draft/transit restrictions into estimated cargo throughput using vessel-class-specific sensitivity.

A one-foot draft change does not have the same tonnage effect across ship types.

## M116 — Queue Dynamics Model

Measure:
arrival rate,
service rate,
queue growth,
maximum queue,
recovery service rate,
clearance time.

Applicable to ports, canals, locks and other bottlenecks.

## M117 — Scheduled-Maintenance Baseline

Distinguish expected maintenance from forced outage.

Unexpected loss =
actual unavailable capacity
-
capacity already expected unavailable.

## M118 — Nameplate-to-Effective Capacity

For power/refinery/LNG infrastructure distinguish:
nameplate,
operable,
available,
actually utilized.

Signals should use effective incremental capacity.

## M119 — Geographic Substitute Mapping

A substitute only counts if it can physically reach the affected region through transmission, pipeline or shipping capacity.

## M120 — Sign-Decomposition

For each disruption explicitly calculate:
supply effect,
demand effect,
inventory effect,
export effect,
transport effect.

Net sign emerges from components.

## M121 — Constraint Interaction Test

Estimate interaction terms only when mechanisms overlap.

Examples:
low hydro × nuclear outage,
Panama slot reduction × high vessel demand,
crude shut-in × refinery outage.

## M122 — Threshold / Nonlinear Capacity Model

Price effect may be weak until utilization crosses a critical threshold.

Test piecewise or state-dependent response, not only linear regression.

## M123 — Recovery-Surprise Evaluation

At every update estimate expected recovery curve.
New information =
actual recovery - prior expected recovery.

## M124 — Chokepoint Alternative-Route Model

For shipping constraints estimate:
extra distance,
extra days,
fuel cost,
fleet capacity tied up,
cargo type compatibility.

## M125 — Maintenance-Calendar Leakage Guard

Historical maintenance calendars can be revised.
Use only versions/publication dates available before the decision.

## M126 — Physical Capacity Reconciliation

Cross-check operator/regulator reported capacity against observed flows when both are public.

Large disagreement becomes a data-quality flag or separate hypothesis.

## M127 — Seasonal Water Normalization

Reservoir/canal levels are highly seasonal.
Use percentile vs day-of-year and hydrologic regime, not raw elevation alone.

## M128 — Fleet/Plant Exposure Weighting

Convert unit status to economic exposure using nameplate capacity and regional marginal replacement fuel.

## M129 — Constraint Persistence Hazard

Model probability the constraint remains active tomorrow/next week instead of assuming fixed duration.

## M130 — Spare-Capacity Stress Test

Perturb demand and outage assumptions to estimate how close the system is to an infeasible/very expensive state.
