# Wave 29L — Labor Dispute Clocks & Capacity Risk

Namespace: **W29L**

Thesis: labor disputes often evolve through public legal/procedural states before an actual work stoppage. Those states create explicit clocks, changing strike/lockout probability and allowing operational exposure to be measured before lost output appears in conventional statistics.

The research target is the transition from bargaining risk to legally possible self-help to realized capacity loss—not a blanket assumption that union activity is bearish.

All candidates are hypotheses only. Claude owns implementation.

## W29L-E01 — FMCS F-7 Upcoming Bargaining Calendar

Primary source:
Federal Mediation and Conciliation Service monthly public F-7 notice files.

Federal labor law generally requires notice to FMCS/state mediation agencies after notice to modify/terminate covered collective bargaining agreements.

Build:
employer,
union,
location,
industry,
notice/contract dates where published,
bargaining-unit size where published.

Priority: S-

## W29L-E02 — F-7 Publication-Lag Clock

FMCS publishes monthly batches after month-end rather than a real-time public feed.

Store:
filing month/date where available,
public monthly-file date,
contract expiration/termination date.

Feature:
remaining public lead time before contract milestone.

Priority: S methodology/edge hybrid

## W29L-E03 — Contract Expiration Density

Aggregate public F-7 notices by:
company,
industry,
region,
supplier network,
calendar week/month.

Question:
when are many economically linked bargaining agreements approaching critical dates simultaneously?

Priority: A+

## W29L-E04 — Bargaining Unit Capacity Exposure

Candidate:
workers in affected bargaining unit
/
facility or company operational workforce.

Use point-in-time employment and facility role.

Priority: S-

## W29L-E05 — Critical Occupation Multiplier

Worker count alone can understate disruption.

Weight by role:
pilots,
rail engineers/conductors,
longshore,
skilled maintenance,
production-line specialty,
warehouse/distribution,
healthcare,
other.

Only assign criticality with sourced operational evidence.

Priority: A+

## W29L-E06 — NLRB Bargaining-Fracture Pulse

Primary source:
NLRB NxGen case data / Advanced Data Search.

NLRB says new cases are posted to its website within about a day.

Research allegations such as:
refusal to bargain,
bad-faith bargaining,
unilateral change/contract modification,
information refusal,
retaliation linked to concerted activity.

Priority: A+

## W29L-E07 — NLRB Case Acceleration

Feature:
new labor cases involving same employer/site/union
× allegation severity
× filing acceleration.

Do not treat allegations as adjudicated facts.

Priority: A

## W29L-E08 — Election-to-First-Contract Risk

NLRB representation/election data identify newly organized bargaining units.

Research:
election/certification
-> first-contract negotiation
-> labor dispute / agreement.

First-contract labor risk differs from renewal bargaining.

Priority: B+

## W29L-E09 — NMB Statutory Mediation State

Primary source:
National Mediation Board.

For airline/railroad major disputes under the Railway Labor Act:
DIRECT_NEGOTIATION
NMB_MEDIATION
ARBITRATION_PROFFER
RELEASED
COOLING_OFF
SELF_HELP_ELIGIBLE
PEB
SETTLED.

Priority: S

## W29L-E10 — Thirty-Day Self-Help Countdown

NMB states that after release from mediation following rejection of arbitration, parties enter a 30-day cooling-off period.

Feature:
days/hours to self-help eligibility.

At expiry, absent agreement/PEB/other intervention, union may strike and carrier may use permitted self-help.

Priority: S

## W29L-E11 — Cooling-Off Resolution Hazard

Estimate:
P(settlement before self-help date).

Inputs:
days remaining,
public mediation meetings,
historical carrier/union bargaining,
wage/work-rule gap where public,
network criticality,
PEB likelihood.

Priority: S

## W29L-E12 — Presidential Emergency Board Intervention State

For qualifying rail disputes, creation of a PEB delays self-help and introduces another investigation/recommendation/cooling-off timeline.

States:
PEB_POSSIBLE
PEB_CREATED
REPORT_PENDING
POST_REPORT_COOLING
SELF_HELP_ELIGIBLE_AFTER_PEB.

Priority: S-

## W29L-E13 — PEB Clock Extension

NMB states a Section 10 PEB generally adds:
up to 30 days for report
+ another 30-day cooling-off period.

Recalculate legal self-help clock whenever PEB status changes.

Priority: A+

## W29L-E14 — Airline Network Labor Exposure

Map affected airline bargaining unit to:
fleet/crew role,
hub,
schedule,
cargo exposure,
substitute carriers.

Candidate:
critical labor capacity at risk
/
network substitute capacity.

Priority: S

## W29L-E15 — Rail Network Labor Exposure

Map affected rail labor group/carrier to:
route miles,
terminal/gateway role,
commodity flows,
intermodal,
grain/coal/auto/crude exposure.

Fuse with STB service data.

Priority: S

## W29L-E16 — Labor Threat × Existing Service Stress

Same labor dispute can have larger impact when current operations are already degraded.

Fuse:
W16S rail dwell/velocity or FAA constraints
× labor self-help probability.

Priority: S

## W29L-E17 — Strike Capacity-Loss Scenario Envelope

Before a stoppage, estimate:
LOW
BASE
SEVERE
capacity-loss scenarios from:
participating worker fraction,
critical roles,
management substitution,
contractors,
inventory buffers,
customer rerouting.

Priority: S

## W29L-E18 — Work-Stoppage Confirmation

Primary source:
BLS Major Work Stoppages.

BLS publishes monthly preliminary data for stoppages involving >=1,000 workers and at least one full shift.

Use as realized-event validation for large stoppages.

Priority: Validation

## W29L-E19 — Small-Stoppage Coverage Gap

BLS excludes stoppages under 1,000 workers.

Do not use absence from BLS as proof no stoppage occurred.

Use company/union/regulatory/operational sources for smaller events.

Priority: Methodology

## W29L-E20 — Strike Duration Survival Model

Once stoppage begins estimate:
P(return by day N)
and expected lost worker-days/capacity.

Inputs:
industry,
bargaining gap,
inventory,
substitute capacity,
prior dispute history,
mediation/intervention.

Priority: A+

## W29L-E21 — Partial Return / Tentative Agreement State

Separate:
TENTATIVE_AGREEMENT
RATIFICATION_PENDING
PARTIAL_RETURN
FULL_RETURN
REJECTED_AGREEMENT.

BLS ending date may reflect tentative settlement and need not equal full operational recovery.

Priority: A

## W29L-E22 — Post-Strike Backlog Liquidation

After workers return:
production/logistics may remain impaired by backlog.

Track:
rail dwell,
air cancellations,
port/warehouse queue,
orders/shipments,
plant output.

Priority: A+

## W29L-E23 — Labor Dispute Supply-Chain Propagation

Graph:
employer/facility
-> supplier/customer
-> transport node
-> inventory buffer
-> substitute producer.

Goal:
measure indirect capacity loss beyond workers directly involved.

Priority: S-

## W29L-E24 — Labor Demand Transfer

A strike can benefit substitutes/competitors.

Feature:
lost capacity at affected firm
/
spare capacity at competitors.

Priority: A+

## W29L-E25 — Bargaining Reality Gap

Compare:
company/union public confidence language
vs
procedural/legal state
vs
operational preparations.

Research divergence rather than sentiment alone.

Priority: A

## W29L-E26 — Strike-Preparation Operational Signal

Where public:
schedule reductions,
customer embargoes,
inventory prebuild,
rerouting,
contingency hiring,
equipment repositioning.

These may provide physical confirmation that strike probability is being operationalized.

Priority: S-

## W29L-E27 — Labor Capacity Risk Quotient

LCRQ =
probability-weighted unavailable critical capacity
/
available substitute capacity.

Priority: S

## W29L-E28 — Labor Dispute Truth Ladder

F-7 / bargaining signal
-> formal dispute
-> NMB/NLRB procedural escalation
-> lawful self-help eligibility
-> actual stoppage
-> operational throughput loss
-> inventory/price effect
-> recovery.

Promotion requires intermediate validation.

Priority: S architecture

## Highest-priority W29L tests

1. W29L-E01 FMCS F-7 Upcoming Bargaining Calendar
2. W29L-E06 NLRB Bargaining-Fracture Pulse
3. W29L-E09 NMB Statutory Mediation State
4. W29L-E10 Thirty-Day Self-Help Countdown
5. W29L-E11 Cooling-Off Resolution Hazard
6. W29L-E14 Airline Network Labor Exposure
7. W29L-E15 Rail Network Labor Exposure
8. W29L-E17 Strike Capacity-Loss Scenario Envelope
9. W29L-E23 Labor Dispute Supply-Chain Propagation
10. W29L-E27 Labor Capacity Risk Quotient
