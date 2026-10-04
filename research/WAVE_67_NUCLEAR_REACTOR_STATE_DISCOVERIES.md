# Wave 67N — Nuclear Reactor Operational & Regulatory State

Namespace: **W67N**

Thesis: a single nuclear unit can represent a large block of low-marginal-cost baseload. NRC daily reactor status and event notifications expose unit-specific derates, scrams, technical-specification shutdowns and recovery clocks beneath aggregate ISO/RTO outage totals. The useful edge is not "nuclear outage bullish gas"; it is the exact lost MW, cause, expected persistence, substitute generation and reserve context.

W24A owns aggregate generation availability/forced-outage scarcity. W67N owns **unit-level U.S. nuclear operating and regulatory state**.

All candidates are research hypotheses only. Claude owns later implementation.

## W67N-E01 — Daily Reactor Power State
Primary source:
NRC Power Reactor Status Report.

For each operating unit:
reported percent power,
down flag,
reason/comment,
24h change flag,
scram count.

Priority: S

## W67N-E02 — Unit Derate Shock
Feature:
reported power_today
-
power_prior_report.

Classify:
MINOR_DERATE
MAJOR_DERATE
FULL_SHUTDOWN.

Priority: S

## W67N-E03 — Fleet Nuclear MW Lost
Translate percent-power reductions into approximate unavailable MW using licensed/nameplate/net capability mapping.

Priority: S

## W67N-E04 — Regional Nuclear Capacity Loss
Aggregate unavailable nuclear MW by ISO/RTO/balancing region.

Priority: S

## W67N-E05 — Planned Refueling / Coastdown State
Separate:
COASTDOWN
REFUELING_OUTAGE
PLANNED_MAINTENANCE
from forced loss.

Priority: S-

## W67N-E06 — Unplanned Scram State
NRC event/status data identify reactor trips/scrams.

Track:
AUTOMATIC
MANUAL
UNKNOWN/RETRACTED where source supports.

Priority: S

## W67N-E07 — Scram Severity Context
Features:
initial power,
current power/mode,
safety-system actuation,
offsite power state,
emergency classification,
reportable-code family.

Priority: S-

## W67N-E08 — Technical-Specification Required Shutdown
NRC event notifications can report shutdowns required by Technical Specifications.

State:
LIMITING_CONDITION
POWER_REDUCTION
SHUTDOWN_INITIATED
SHUTDOWN_COMPLETE
RECOVERY.

Priority: S

## W67N-E09 — Event Notification-to-Status Gap
Compare first NRC-notification information with next daily status report.

Target:
does early event state correctly imply next-day MW loss?

Priority: S

## W67N-E10 — Event Revision Velocity
Event Notifications can be revised.

Track changes in:
cause,
power/mode,
safety significance,
retraction,
corrective action.

Priority: A+

## W67N-E11 — Forced-Outage Persistence
Estimate duration from:
first unexpected derate/scram
to
sustained return near full power.

Priority: S

## W67N-E12 — Restart Ramp
Track:
0
-> low power
-> intermediate
-> near full power.

Feature:
MW restored per day/report.

Priority: S-

## W67N-E13 — Restart Stall Hazard
If a unit returns partially then stops increasing or derates again:
estimate probability of extended outage/re-shutdown.

Priority: A+

## W67N-E14 — Repeat-Scram Hazard
Recent scram/event history can alter probability of another forced interruption during restart/operation.

Priority: A

## W67N-E15 — Transformer / Grid Interface Constraint
Status reports can cite transformer/electrical limitations distinct from reactor-core issues.

Map cause to likely recovery class.

Priority: A+

## W67N-E16 — Environmental Derate State
Public status comments can identify environmental conditions causing reduced power.

Fuse with W30W water-temperature/flow and weather.

Priority: S-

## W67N-E17 — Seasonal Thermal Constraint
Estimate probability of environmentally driven derate during high river/lake temperature or low-flow state.

Priority: S

## W67N-E18 — Nuclear-to-Gas Substitution
Expected gas-fired replacement MW =
nuclear MW lost
× marginal gas replacement probability.

Condition on:
coal/hydro/renewables,
imports,
reserve headroom,
gas constraints.

Priority: S

## W67N-E19 — Nuclear-to-Power-Price Scarcity
Fuse unit loss with W25R reserve/ramp scarcity and W23T transmission congestion.

Priority: S

## W67N-E20 — Nuclear Outage × Gas Basis
Map affected unit to gas generators/hubs likely to replace output.

Validate regional basis before broad Henry Hub effects.

Priority: A+

## W67N-E21 — Planned-vs-Forced Reality Gap
Compare aggregate ISO/RTO outage classification with NRC unit-level cause/status.

Priority: A+

## W67N-E22 — Daily Status Surprise
Estimate expected power from prior state/known planned outage.

Feature:
reported power
-
expected power.

Priority: S

## W67N-E23 — Event-Notification Surprise
A reportable event at a unit believed stable can precede next-day availability loss.

Priority: S-

## W67N-E24 — Outage Recovery Forecast
Predict:
next-day power,
time to 50%,
time to >90%.

Priority: S

## W67N-E25 — Refueling-Outage Overrun
For planned outages:
actual return date
-
historical/announced expected return.

Priority: A+

## W67N-E26 — Inspection-Finding Risk State
NRC Reactor Oversight Process publishes inspection findings/performance indicators on slower cycles.

Use as structural forced-outage-risk context.

Priority: A

## W67N-E27 — Escalated Enforcement State
NRC enforcement actions/orders can impose corrective obligations or altered operating conditions.

Separate from routine inspection findings.

Priority: A

## W67N-E28 — Part 21 Common-Mode Defect
NRC Part 21 reports can reveal defects/noncompliance in components potentially used across facilities.

Graph:
vendor/component
-> affected reactors
-> common-mode outage/remediation risk.

Priority: S-

## W67N-E29 — Common-Mode Nuclear Fleet Risk
Multiple reactors sharing:
design,
vendor,
component,
environmental exposure
can create correlated derate/remediation risk.

Priority: S

## W67N-E30 — Nuclear Availability Quotient
NAQ =
currently available nuclear MW
/
expected seasonal nuclear MW.

Priority: S

## W67N-E31 — Nuclear Replacement Burden
NRB =
unexpected nuclear MW unavailable
/
dispatchable substitute + import + reserve capacity.

Priority: S

## W67N-E32 — Nuclear Truth Ladder
EVENT / STATUS CHANGE
-> UNIT MW LOSS
-> PERSISTENCE / RESTART
-> REGIONAL RESERVE SUBSTITUTION
-> GAS/POWER FLOW
-> PRICE/BASIS
-> RECOVERY.

Priority: S architecture

## Highest-priority W67N tests

1. W67N-E02 Unit Derate Shock
2. W67N-E04 Regional Nuclear Capacity Loss
3. W67N-E08 Technical-Specification Required Shutdown
4. W67N-E09 Event Notification-to-Status Gap
5. W67N-E11 Forced-Outage Persistence
6. W67N-E13 Restart Stall Hazard
7. W67N-E18 Nuclear-to-Gas Substitution
8. W67N-E24 Outage Recovery Forecast
9. W67N-E29 Common-Mode Nuclear Fleet Risk
10. W67N-E31 Nuclear Replacement Burden
