# Wave 28M — Mine Withdrawal & Forced Capacity Loss

Namespace: **W28M**

Thesis: mining capacity can be legally removed before monthly/quarterly commodity-production statistics reveal it. MSHA withdrawal orders, mine status, imminent-danger enforcement and accident/emergency controls create observable state transitions from normal operation to restricted capacity and back.

The research objective is to estimate actual capacity removed, duration, substitutability and downstream commodity consequences—not to treat every safety citation as a trading event.

All candidates are hypotheses only. Claude owns any later implementation.

## W28M-E01 — MSHA 107(a) Imminent-Danger Withdrawal Pulse

Primary source:
MSHA dedicated 107(a) Orders Issued dataset.

Section 107(a) requires withdrawal of persons from the affected mine area when an MSHA representative finds an imminent danger, until the danger/causal condition no longer exists.

Candidate event:
order issue date
-> active restriction
-> termination date.

Priority: S

## W28M-E02 — Active Withdrawal Duration

Feature:
termination_time/date - issue_time/date.

Where intraday time is not publicly available, retain interval uncertainty.

Research whether duration predicts:
lost shifts,
later production loss,
shipment shortfall,
commodity basis stress.

Priority: S

## W28M-E03 — Open 107(a) Order Inventory

The dedicated dataset includes termination status/date.

Construct:
active unresolved 107(a) orders
by mine/operator/commodity/region.

Priority: S-

## W28M-E04 — Mine-Area vs Whole-Mine Capacity Fraction

A 107(a) order applies to the area throughout which imminent danger exists; it does not automatically mean the entire mine is shut.

Estimate affected capacity using:
subunit,
mine type,
narrative/area if source available,
mine geometry/operation metadata,
historical production structure.

Priority: S

## W28M-E05 — Production-Weighted Withdrawal Severity

Candidate:
estimated affected mine output
/
regional or national commodity output.

For coal, use MSHA historical mine-level production as denominator.
For metal/nonmetal, seek commodity-specific external production denominators because MSHA operators are not generally required to report production the same way.

Priority: S

## W28M-E06 — Repeated Imminent-Danger Mine State

Feature:
107(a) order count and recency by mine,
normalized by inspection exposure and operating scale.

Question:
does repeated imminent danger predict future forced interruptions?

Priority: A+

## W28M-E07 — Operator-Wide Safety Contagion

Map mine IDs to operator/controller.

Research whether severe enforcement at one mine is followed by:
heightened inspection/enforcement,
operational changes,
or disruptions at sister mines.

Do not assume regulator contagion without evidence.

Priority: A

## W28M-E08 — Pattern-of-Violations Capacity Risk

Primary source:
MSHA POV status/notices.

Under POV, subsequent S&S violations can trigger withdrawal orders from affected areas until abatement.

State:
NORMAL
POV_RISK
POV_NOTICE
WITHDRAWAL_UNDER_POV
POV_TERMINATED.

Priority: S-

## W28M-E09 — POV Withdrawal Hazard

For mines under active POV:
estimate P(withdrawal order in next inspection/window).

Inputs:
recent S&S rate,
inspection intensity,
violation mix,
corrective action,
mine type.

Priority: A+

## W28M-E10 — S&S Rate Acceleration

MSHA provides compliance monitoring and S&S measures.

Research:
recent S&S violation-rate acceleration
as a slow precursor to severe enforcement.

Hard rule:
use only information publicly available before the outcome.

Priority: A

## W28M-E11 — 103(j)/(k) Accident-Control Capacity State

MSHA can issue section 103(j)/(k) orders after mine accidents/emergencies to control activity and protect persons/evidence.

Separate:
accident-site restriction
from
whole-operation restriction.

Priority: A+

## W28M-E12 — Preliminary Fatality/Accident Shock

MSHA publishes preliminary fatality reports with mine/operator identity and event details.

Use:
event confirmation,
potential operational interruption,
later enforcement state.

Do not assume every fatality causes material production loss.

Priority: A

## W28M-E13 — Emergency-to-Withdrawal Escalation

State path:
ACCIDENT_NOTIFICATION
-> 103(j/k)
-> 107(a) where applicable
-> MODIFICATION
-> TERMINATION
-> NORMAL_OPERATION.

Priority: A+

## W28M-E14 — Mine Status Transition

MSHA Mines dataset includes current mine status.

Track:
ACTIVE
NONPRODUCING
TEMPORARILY_IDLE where source semantics support
ABANDONED/SEALED
and status date.

Use as slow capacity-state confirmation.

Priority: A

## W28M-E15 — Enforcement Recovery Half-Life

After severe order:
time to termination
time to status normalization
time to production normalization
time to shipment normalization.

Market impact may depend more on recovery than initial enforcement headline.

Priority: S-

## W28M-E16 — Coal Production Baseline by Mine

Primary source:
MSHA quarterly employment/production.

Official release:
first Friday of the second month following quarter, roughly 30–45 days after quarter-end.

Use only as historical capacity/exposure denominator, not live production.

Priority: Infrastructure

## W28M-E17 — Mine Labor-Hours Capacity Proxy

Quarterly MSHA data include employee count and hours worked.

Use to estimate:
mine operating scale,
labor intensity,
lost-shift sensitivity.

Priority: A as denominator

## W28M-E18 — Withdrawal × Inventory Buffer

A mine outage matters less if downstream inventories are abundant.

Fuse:
lost capacity
× commodity inventory tightness
× delivery location
× transport substitutability.

Priority: S

## W28M-E19 — Withdrawal × Rail/Port Bottleneck

A production interruption can be amplified or masked by existing transport constraints.

Fuse with:
W16S rail-service stress,
W24M marine operability,
existing port/river sources.

Priority: A+

## W28M-E20 — Mine-to-Plant Dependency Graph

Graph:
mine
-> prep/processing facility
-> rail/barge/port
-> power plant/smelter/mill/customer where sourced.

Goal:
identify where one mine is a critical supplier.

Priority: S-

## W28M-E21 — Critical-Mineral Capacity Shock

For metal/nonmetal mines:
map withdrawal event to critical mineral/commodity only with verified mine commodity identity.

Potential targets:
copper,
silver,
gold,
lithium,
aggregates,
salt,
other industrial minerals.

Priority: A

## W28M-E22 — Coal Basin Capacity Breadth

Aggregate active withdrawal/enforcement stress by basin/state.

Feature:
production-weighted affected share
× duration.

Priority: A+

## W28M-E23 — Safety Order Surprise

Estimate expected enforcement risk from prior mine history/inspection context.

Feature:
observed severe order
-
ex ante hazard.

Priority: A

## W28M-E24 — Forced Mine Capacity Loss Quotient

FMCLQ =
estimated legally unavailable production capacity
/
available substitute supply capacity.

Substitutes:
other mines,
inventories,
imports,
alternate fuel/material,
transport rerouting.

Priority: S

## W28M-E25 — Mine Enforcement Truth Ladder

DISCOVERY/INSPECTION
-> ORDER
-> AREA WITHDRAWN
-> ACTIVE CAPACITY LOSS
-> PRODUCTION/SHIPMENT IMPACT
-> INVENTORY/PRICE EFFECT
-> RECOVERY.

No direct return claim promotes without intermediate physical validation.

Priority: S architecture

## Highest-priority W28M tests

1. W28M-E01 107(a) Imminent-Danger Withdrawal Pulse
2. W28M-E02 Active Withdrawal Duration
3. W28M-E04 Mine-Area vs Whole-Mine Capacity Fraction
4. W28M-E05 Production-Weighted Withdrawal Severity
5. W28M-E08 Pattern-of-Violations Capacity Risk
6. W28M-E13 Emergency-to-Withdrawal Escalation
7. W28M-E15 Enforcement Recovery Half-Life
8. W28M-E18 Withdrawal × Inventory Buffer
9. W28M-E20 Mine-to-Plant Dependency Graph
10. W28M-E24 Forced Mine Capacity Loss Quotient
