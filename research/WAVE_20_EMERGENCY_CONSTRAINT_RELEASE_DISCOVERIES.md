# Wave 20E — Emergency Constraint Release

Namespace: **W20E**

Thesis: emergency waivers/orders are endogenous responses to scarcity or infrastructure stress. They can confirm that normal capacity is insufficient while simultaneously unlocking substitute supply/logistics. The research target is the net change in effective capacity after relief—not the headline alone.

All candidates are research hypotheses only. Claude owns implementation.

## W20E-E01 — EPA Emergency Fuel-Waiver Pulse

Primary source:
EPA Fuel Waivers.

Event fields:
announcement,
effective start/end,
geography,
fuel/specification waived,
stated supply circumstance,
renewal/termination.

Priority: S

## W20E-E02 — Fuel-Spec Constraint Release Capacity

Translate a waiver into estimated additional compatible supply:
RVP relaxation,
boutique-fuel relaxation,
ethanol blend flexibility,
diesel sulfur relaxation.

Candidate:
incremental eligible inventory/production/distribution capacity.

Priority: S

## W20E-E03 — Waiver Renewal Persistence

Repeated 20-day waivers/renewals indicate unresolved supply stress.

Feature:
number of consecutive renewal windows
× geography
× unchanged/expanded scope.

Priority: A+

## W20E-E04 — Waiver Geography Breadth

State/local waiver versus national waiver.

Weight by:
fuel consumption,
refining capacity,
pipeline connectivity,
season.

Priority: A+

## W20E-E05 — Fuel Waiver × Inventory Tightness

Fuse:
waiver state
+ EIA regional product inventory
+ refinery outages
+ pipeline/port state.

Question:
Does waiver impact depend on how little buffer existed beforehand?

Priority: S

## W20E-E06 — Fuel Waiver Counterfactual Spread

Estimate:
product basis/spread under observed waiver
versus expected spread without constraint relief.

Do not treat waiver issuance as purely bullish/bearish.

Priority: A

## W20E-E07 — FMCSA Emergency Logistics Relief

Primary source:
FMCSA Emergency Declarations.

Capture:
commodity/service covered,
states,
regulations relaxed,
effective/expiration,
extensions.

Priority: S-

## W20E-E08 — Heating-Fuel Delivery Backlog State

FMCSA/state energy emergency declarations can explicitly cite:
delivery backlog,
regional propane shortages,
rail disruption,
refinery outage,
extreme cold.

Convert narrative to structured causal fields.

Priority: S

## W20E-E09 — HOS Capacity Release

Estimate incremental truck-hours/logistics capacity available under hours-of-service relief.

Condition on:
driver availability,
terminal loading capacity,
truck fleet,
weather/road constraints.

Priority: A+

## W20E-E10 — Emergency Declaration Persistence

Extensions imply the original logistics constraint has not fully normalized.

Measure:
days under relief
× number of extensions
× shrinking/expanding geography.

Priority: A

## W20E-E11 — FMCSA Relief × Rail Failure Collision

Example chain:
rail propane disruption
-> truck substitution demand
-> HOS relief
-> trucking catch-up.

Use rail service metrics from W16S to measure substitute burden.

Priority: S-

## W20E-E12 — DOE 202(c) Reliability Emergency State

Primary source:
DOE CESER Section 202(c) orders.

Build:
application time,
order time,
RTO/region,
specified resources,
constraint overridden,
effective window,
extensions.

Priority: S

## W20E-E13 — Environmental/Operating-Limit Override

Some 202(c) orders authorize generation above normal operating/environmental constraints when needed for reliability.

Candidate:
normally unavailable incremental MW
made conditionally dispatchable.

Priority: S

## W20E-E14 — Backup-Generation Unlock

2026 DOE orders demonstrate authorization for RTOs to call backup generation at data centers/large loads as a last-resort reliability tool.

Estimate:
load removed from grid
or backup MW activated
before/at EEA3.

Priority: S

## W20E-E15 — 202(c) Application-to-Order Lead

An RTO application can precede the signed DOE order.

Separate:
RTO REQUEST
DOE ORDER
RESOURCE DISPATCH
ORDER EXPIRATION.

Priority: A+

## W20E-E16 — Grid Scarcity Severity Confirmation

A 202(c) request/order is an endogenous indicator that normal market/rule resources may be insufficient.

Fuse with:
reserve shortfall,
outages,
exports,
load,
transmission constraints.

Priority: S

## W20E-E17 — Relief Effectiveness Test

Measure whether emergency authority actually:
raised generation,
reduced grid load,
improved reserves,
prevented load shed.

Priority: S

## W20E-E18 — Jones Act Waiver Request Pulse

Primary source:
CBP public navigation-law waiver request page.

Requests can include:
cargo,
vessel,
flag,
loading/delivery dates,
ports,
capacity rationale.

Priority: S-

## W20E-E19 — Coastwise Capacity Deficit

A perfected waiver request can expose lack of suitable coastwise-qualified vessel capacity for a specific shipment/window.

Candidate:
required cargo-tonnage/vessel-days
-
available domestic vessel capacity.

Priority: S

## W20E-E20 — Waiver Request vs Grant

Separate:
REQUEST_POSTED
MARAD CAPACITY REVIEW
GRANTED
DENIED/WITHDRAWN
EXPIRED.

A request is evidence of desired capacity; a grant is actual constraint release.

Priority: A+

## W20E-E21 — Jones Act Route/Cargo Stress Map

Map:
origin port
destination port
cargo type
required delivery date
normal domestic shipping cost/capacity.

Targets:
fuel,
natural gas/LNG where legally relevant,
fertilizer,
coal,
critical cargo.

Priority: A+

## W20E-E22 — Maritime Capacity Release Estimate

Estimate extra voyage capacity unlocked by allowing otherwise-ineligible vessel(s).

Compare to total regional shipment need.

Priority: A

## W20E-E23 — Emergency Relief Stack

Multiple independent relief actions can occur for one shortage:
EPA fuel waiver
+ FMCSA HOS relief
+ Jones Act waiver
+ DOE emergency action.

Composite breadth may identify severe cross-mode/system stress.

Priority: S

## W20E-E24 — Constraint-Release Substitution Quotient

CRSQ =
incremental capacity unlocked by emergency relief
/
estimated capacity deficit.

Interpretation:
<1 insufficient relief
≈1 matched relief
>1 potentially ample relief.

Priority: S

## W20E-E25 — Relief Withdrawal / Expiry Risk

When waiver/order expires:
does the underlying constraint remain?

Track:
scheduled expiry
renewal probability
inventory recovery
physical normalization.

Priority: A+

## W20E-E26 — Endogenous-Policy Response Architecture

Causal chain:

PHYSICAL SCARCITY
-> AGENCY/RTO REQUEST
-> EMERGENCY RELIEF
-> SUBSTITUTE CAPACITY
-> BACKLOG/RESERVE RESPONSE
-> PRICE NORMALIZATION OR FAILURE.

Never model the policy action as exogenous.

Priority: S architecture

## Highest-priority W20E tests

1. W20E-E02 Fuel-Spec Constraint Release Capacity
2. W20E-E03 Waiver Renewal Persistence
3. W20E-E08 Heating-Fuel Delivery Backlog State
4. W20E-E09 HOS Capacity Release
5. W20E-E12 DOE 202(c) Reliability Emergency State
6. W20E-E14 Backup-Generation Unlock
7. W20E-E16 Grid Scarcity Severity Confirmation
8. W20E-E19 Coastwise Capacity Deficit
9. W20E-E23 Emergency Relief Stack
10. W20E-E24 Constraint-Release Substitution Quotient
