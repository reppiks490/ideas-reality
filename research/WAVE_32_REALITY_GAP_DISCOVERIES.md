# Wave 32R — Reality Gap & Cross-Layer Contradiction

Namespace: **W32R**

Thesis: disagreement between independently measured layers of reality can be more informative than any single signal. A forecast can improve while realized operations worsen. A legal restriction can lift while throughput remains impaired. Physical infrastructure can recover while financial claims keep accelerating. Credit can deteriorate while equity remains complacent. Futures can discover price while a halted cash constituent remains stale.

The research object is the **expected relationship between layers**, the uncertainty around that relationship, and the standardized residual when reality violates it.

All candidates are hypotheses for Claude to test later. This repo remains research-only.

## W32R-E01 — Cross-Layer Reality Gap

General form:

RealityGap(A -> B) =
observed_B
-
E[B | A, state, lag]

standardized by forecast uncertainty.

Examples:
physical recovery -> expected throughput,
throughput recovery -> expected claims stabilization,
credit deterioration -> expected equity repricing.

Priority: S

## W32R-E02 — Forecast-vs-Realization Surprise

For every forward source:
forecast state
-> realized state.

Feature:
realized outcome - latest legally/publicly available forecast.

Examples:
port cargo forecast vs arrival,
grid forecast vs load,
weather vs outage,
reservoir forecast vs operation,
OFS marine forecast vs observed navigability.

Priority: S

## W32R-E03 — Forecast Revision Momentum

Track changes across consecutive point-in-time forecast vintages.

Feature:
first derivative,
second derivative,
direction persistence,
cross-source agreement.

Research whether revision trajectory adds information beyond latest forecast level.

Priority: S-

## W32R-E04 — Regulatory-Relaxation / Operational-Impairment Gap

Examples:
port reopened but queue persists,
mine withdrawal order terminated but production remains low,
water curtailment suspended but intake/output remains constrained,
grid emergency state clears but communications remain on backup power.

Priority: S

## W32R-E05 — Operational-Recovery / Financial-Loss Gap

Fuse:
physical/service recovery
vs
catastrophe claims/loss revisions.

State:
PHYSICAL_RECOVERY_FAST / FINANCIAL_LOSS_STILL_ACCELERATING.

Hypothesis:
markets may overfocus on restored infrastructure while lagged loss development continues worsening.

Priority: S

## W32R-E06 — Financial-Loss Stabilization / Physical-Impairment Gap

Inverse of E05:
claims/assistance flatten,
but physical throughput remains impaired.

Potential implication:
business interruption/economic loss not captured by household/insurance claim channels.

Priority: A+

## W32R-E07 — Legal Capacity vs Physical Capacity

Compare what is legally allowed with what can physically operate.

Examples:
water right available vs flow inadequate,
port open vs unsafe draft/current,
pipeline authorized vs compressor outage,
generator permitted vs fuel/water unavailable.

Priority: S

## W32R-E08 — Physical Capacity vs Utilized Capacity

Compare estimated available capacity with actual flow/output.

Gap can indicate:
weak demand,
hidden bottleneck,
commercial constraint,
labor shortage,
data problem.

Priority: S

## W32R-E09 — Mandatory Commitment vs Physical Delivery

Compare:
USDA export sale commitment -> inspection/shipment,
procurement award -> delivery/performance,
TBA trade -> settlement,
pipeline nomination -> scheduled/actual flow.

Output:
realization probability and slippage.

Priority: S

## W32R-E10 — Price Move Unsupported by Physical Truth

Condition on market move and ask whether higher-truth layers confirm it:
transactions,
institutional flow,
operations,
physical sensors,
realized outcome.

Feature:
market move magnitude
-
mechanism-supported move expectation.

Do not automatically fade unsupported moves; first test continuation/reversal behavior.

Priority: S

## W32R-E11 — Physical Shock Unpriced by Market

Inverse:
large verified physical/operational shock with muted price response.

Possible explanations:
inventory buffer,
substitution,
already anticipated,
market underreaction,
wrong target.

Priority: S

## W32R-E12 — Credit-vs-Equity Contradiction

Reuse W25C.

States:
CREDIT_WORSE / EQUITY_CALM,
EQUITY_WORSE / CREDIT_CALM,
BOTH_WORSE,
BOTH_RECOVER.

Track persistence and resolution direction.

Priority: S

## W32R-E13 — Cash-vs-Futures Stale-State Gap

Reuse W27V halted-constituent architecture.

When cash is constrained/halted:
futures/ETF/options can move while cash index contribution remains stale.

Feature:
latent cross-market value - stale cash value.

Priority: S

## W32R-E14 — Grid Restored / Telecom Backup-Power Gap

Reuse W13H + grid layers.

If grid metrics normalize but many cell sites remain on backup power or communications remain impaired:
recovery is incomplete or geographically mismatched.

Priority: A+

## W32R-E15 — Port Open / Queue Not Cleared

Reuse W24M.

State:
formal COTP restriction lifted
while
AIS/queue/throughput remains impaired.

Measure backlog half-life.

Priority: S-

## W32R-E16 — Labor Settlement / Throughput Not Recovered

Reuse W29L.

Tentative agreement or return-to-work
does not equal
normal production/service.

Feature:
post-settlement operational residual.

Priority: A+

## W32R-E17 — Mine Order Terminated / Output Not Recovered

Reuse W28M.

Test whether order termination predicts physical recovery or whether maintenance/repair backlog dominates.

Priority: A+

## W32R-E18 — Water Curtailment Suspended / Intake Still Constrained

Reuse W30W.

Legal diversion can resume while hydrology/temperature/physical intake remains unfavorable.

Priority: A+

## W32R-E19 — Disaster Narrative / Measured Damage Gap

Compare:
headline/forecast severity
vs
OpenFEMA damage development,
FCC outage,
Black Marble,
grid,
logistics,
claims.

Priority: S

## W32R-E20 — Claims Accelerating / Market Recovery Gap

If affected insurer/utility/bank/REIT equity recovers while claims/loss nowcast continues revising upward:
measure disagreement.

Must control broad risk-on rebound and exposure uncertainty.

Priority: A+

## W32R-E21 — Capacity Available / Demand Not Realized

Examples:
LNG export capacity restored but feedgas stays weak,
rail service improves but carloads do not,
port operability improves but arrivals remain low,
power capacity available but load weak.

Interpret as demand-side information, not supply failure.

Priority: A+

## W32R-E22 — Demand Strong / Capacity Not Responding

Inverse:
commitments/orders/load rise while physical flow/output remains flat.

Potential bottleneck or rationing state.

Priority: S-

## W32R-E23 — Multi-Sensor Disagreement Breadth

For an event/system:
count independent modalities whose standardized residuals conflict with the current consensus.

Weight by source independence and calibrated reliability.

Priority: S

## W32R-E24 — Conflict Persistence

Feature:
time that disagreement remains above calibrated threshold.

Transient disagreement may be timing noise; persistent disagreement may indicate regime shift or hidden constraint.

Priority: S

## W32R-E25 — Which Source Is Wrong? Posterior

Maintain posterior probability that each source/model is:
healthy,
stale,
biased,
mis-mapped,
structurally broken.

Do not turn a bad sensor into alpha.

Priority: S architecture

## W32R-E26 — Source Reliability Regime

Each source has time-varying reliability from:
latency,
revision rate,
missingness,
recent forecast error,
schema changes,
coverage.

Conflict weight is discounted by current reliability.

Priority: S

## W32R-E27 — Independent Confirmation Count

Count independent truth layers confirming the same mechanism.

Avoid double-counting correlated feeds derived from the same upstream source.

Priority: A+

## W32R-E28 — Cross-Layer Surprise Tensor

Dimensions:
source layer,
target layer,
direction,
magnitude,
uncertainty,
persistence,
expected lag,
regime.

This is the generalized representation of all RealityGap edges.

Priority: S

## W32R-E29 — Contradiction Cascade

Graph:
initial contradiction
-> downstream layer mismatch
-> market repricing.

Example:
port physically impaired
but official restriction lifted
-> queue grows
-> delivery misses
-> inventory tightens
-> price responds.

Priority: S

## W32R-E30 — Reality-Gap Resolution Direction

Target:
which layer moves to resolve the disagreement?

Possibilities:
A catches B,
B catches A,
both revert,
third constraint explains gap,
source failure.

Priority: S

## W32R-E31 — Reality-Gap Half-Life

Estimate expected duration of each contradiction type.

Use as state-dependent horizon selection.

Priority: A+

## W32R-E32 — Bayesian Surprise State

Measure information gain when new observation materially changes belief about latent operational/financial state.

Candidate:
KL or related divergence between prior and posterior distributions, with robust implementation.

Priority: A+

## W32R-E33 — Change-Point vs Collective-Anomaly Classifier

A one-off contradiction and a permanent relationship change are different.

Use online changepoint/anomaly methods to classify:
TRANSIENT_ANOMALY
COLLECTIVE_ANOMALY
REGIME_SHIFT.

Priority: S

## W32R-E34 — Disagreement-Driven Abstention

Some contradictions should reduce confidence rather than create a trade.

Output:
TRADE_SIGNAL
RESEARCH_ALERT
ABSTAIN
SOURCE_HEALTH_ALERT.

Priority: S architecture

## W32R-E35 — Reality Gap Portfolio

Treat contradiction families as separate mechanisms:
physical-financial,
legal-operational,
forecast-realized,
cross-market,
capacity-utilization,
sensor-sensor.

Build orthogonality/correlation graph before combining.

Priority: S

## W32R-E36 — Contradiction-of-Contradictions

Meta-state:
multiple independent RealityGaps point to the same hidden explanation.

Example:
port open but queue high
+ rail dwell high
+ inventory falling
+ freight rates rising
=> likely true logistics constraint despite formal reopening.

Priority: S

## Highest-priority W32R tests

1. W32R-E01 Cross-Layer Reality Gap
2. W32R-E04 Regulatory-Relaxation / Operational-Impairment Gap
3. W32R-E05 Operational-Recovery / Financial-Loss Gap
4. W32R-E07 Legal Capacity vs Physical Capacity
5. W32R-E09 Mandatory Commitment vs Physical Delivery
6. W32R-E23 Multi-Sensor Disagreement Breadth
7. W32R-E25 Which Source Is Wrong? Posterior
8. W32R-E28 Cross-Layer Surprise Tensor
9. W32R-E30 Reality-Gap Resolution Direction
10. W32R-E33 Change-Point vs Collective-Anomaly Classifier
