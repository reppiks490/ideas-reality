# Wave 11S — Future Physical Supply Pipeline

Namespace: W11S

This tranche targets the state transitions that happen before physical supply appears in monthly production statistics: permit intent, regulatory approval, drilling/completion, project queues, construction, commissioning and first flow.

All candidates remain hypotheses until falsified and promoted.

## W11S-E01 — Texas Pending-Permit Intent Pulse

Source:
Railroad Commission of Texas drilling permits pending approval.

Status:
PUBLIC; RRC documents pending-approval files updated twice daily.

Mechanism:
A permit application is early intent, not production.

Features:
- new pending applications
- operator breadth
- county/basin concentration
- horizontal vs other well types
- planned depth
- application type
- amendment/revision activity

Priority: S-

## W11S-E02 — Permit Approval Conversion

Source:
RRC nightly drilling-permit files.

State machine:
PENDING
-> APPROVED
-> AMENDED / EXTENDED
-> EXPIRED / NO_OBSERVED_DRILL
-> downstream completion.

Features:
- approval probability
- time-to-approval
- approval acceleration
- operator-specific conversion rate

Priority: A+

## W11S-E03 — Permit-to-Completion Survival Model

Fuse:
RRC permit master
+ wellbore records
+ nightly completion filings.

Question:
Given a newly approved permit, what is the probability distribution for actual completion and productive status over the next N days/months?

Condition on:
operator, basin/county, well type, horizontal flag, depth, field, commodity regime and operator backlog.

Priority: S

## W11S-E04 — Nightly Completion Momentum

Source:
RRC Completion Information in Data Format.

RRC documents nightly files containing completion forms submitted or approved the prior day.

Features:
- completed wells by basin/operator
- oil vs gas
- initial potential where available
- recompletion vs new
- completion backlog
- submitted-to-approved lag

Intermediate target:
future regional production.

Priority: S

## W11S-E05 — FracFocus Completion Confirmation

Source:
FracFocus public data download.

Status:
PUBLIC; download refreshed five days per week.

Use:
independent confirmation of hydraulic-fracturing activity and well-level disclosure state.

Candidate:
new disclosure count
× well/operator/location
× fracture timing / disclosure attributes where provided.

Hard rule:
disclosure timing is not necessarily fracture execution time. Preserve both source dates where available.

Priority: A+

## W11S-E06 — Permit / Frac / Completion Reality Gap

Fuse:
RRC permit
+ FracFocus disclosure
+ RRC completion.

States:
PERMITTED_ONLY
DRILLED_NOT_FRAC_CONFIRMED
FRAC_DISCLOSED
COMPLETION_SUBMITTED
COMPLETION_APPROVED
PRODUCING_CONFIRMED.

Purpose:
replace raw rig/permit counts with a conversion pipeline.

Priority: S

## W11S-E07 — Operator Backlog / DUC-Like State

Estimate operator-level stock of wells in intermediate states between permit and productive completion.

Features:
- permits minus completions
- age distribution
- basin mix
- operator conversion velocity
- commodity-price sensitivity.

Do not label every unresolved permit a drilled-but-uncompleted well unless drilling evidence exists.

Priority: A+

## W11S-E08 — Completion Intensity Supply Nowcast

Predict near-future Texas oil/gas production using:
completed-well count
+ location
+ well type
+ historical initial productivity
+ operator/basin decline priors.

Validate against later RRC monthly production and EIA production.

Priority: S

## W11S-E09 — EIA-860M Generator Capacity Pipeline

Source:
EIA Preliminary Monthly Electric Generator Inventory.

Status:
MONTHLY; preliminary and revisable.

Tracks existing/proposed generating units of qualifying size with fuel/technology, capacity, location, status and planned in-service information.

Build:
proposed
-> under construction
-> operating
or postponed/canceled.

Priority: A+

## W11S-E10 — Generator Commercial-Operation Slippage

For each proposed generator:
latest expected operating date
-
prior expected operating date.

Features:
- delay frequency
- delay magnitude
- project technology
- developer
- region/balancing authority
- construction status.

Hypothesis:
systematic slippage changes regional capacity/scarcity and fuel-demand expectations.

Priority: A+

## W11S-E11 — Generator Cancellation / Postponement Shock

Use EIA-860M planned/canceled/postponed inventory.

Research:
capacity removed from expected regional supply
× reserve margin
× load growth
× substitute queue capacity.

Priority: A

## W11S-E12 — Interconnection Queue Survival

Sources:
PJM New Services / interconnection data;
ERCOT Generator Interconnection Status reports.

State:
REQUESTED
-> STUDY
-> AGREEMENT
-> CONSTRUCTION / APPROVAL
-> COMMERCIAL
or WITHDRAWN / INACTIVE.

Rather than sum all queue MW, estimate probability-weighted capacity by project phase.

Priority: S

## W11S-E13 — Queue Withdrawal Shock

A large nominal queue can be misleading.

Feature:
probability-weighted capacity lost through withdrawals/inactive status by:
fuel, zone, developer and expected COD.

Potential use:
regional scarcity/capacity-price and equipment-demand outlook.

Priority: A+

## W11S-E14 — Gas Generation Buildout Demand Field

Fuse:
PJM/ERCOT gas generation interconnection requests
+ EIA-860M
+ pipeline capacity/project graph.

Goal:
estimate future incremental gas-fired generation capacity and resulting potential gas demand by region.

Do not convert MW directly to gas burn without heat-rate/capacity-factor uncertainty.

Priority: S-

## W11S-E15 — Battery / Renewable Queue Competition

Track solar/wind/battery/gas queue changes.

Research:
which technologies progress from queue to signed interconnection/commercial status versus remain speculative.

Output:
probability-weighted future capacity mix.

Priority: A

## W11S-E16 — FERC Pipeline Capacity Pipeline

Source:
FERC pending/approved major natural-gas pipeline project datasets and eLibrary/NEPA schedules.

Fields can include:
docket, applicant, states, filing date, completion/certificate dates, miles, capacity and compression.

Build project lifecycle:
PRE_FILING
-> APPLICATION
-> NEPA
-> CERTIFICATE
-> CONSTRUCTION
-> IN_SERVICE.

Priority: S

## W11S-E17 — Pipeline Approval Probability / Timeline Revision

Estimate project approval and in-service timing using:
docket stage
+ NEPA target/actual timing
+ amendments
+ intervention/litigation state
+ historical comparable projects.

Feature:
expected capacity addition × probability × expected in-service distribution.

Priority: A+

## W11S-E18 — LNG Capacity Ramp State

Sources:
EIA U.S. liquefaction project data
+ DOE LNG export authorizations/project status
+ FERC dockets
+ actual feedgas/sendout/export observations.

State:
PROPOSED / AUTHORIZED / FID / UNDER_CONSTRUCTION / COMMISSIONING / PARTIAL_OPERATION / FULL_OPERATION.

Priority: S

## W11S-E19 — First-LNG / Ramp Surprise

For under-construction terminals:
actual commissioning/first-LNG/ramp milestones
vs
latest public expected schedule.

Hypothesis:
schedule surprise can materially alter regional feedgas demand and global LNG balance.

Priority: S-

## W11S-E20 — Future Gas Demand Commitment Graph

Fuse:
future LNG liquefaction
+ gas-power buildout
+ pipeline expansions
+ industrial projects where defensible.

Output:
probability-weighted future gas demand/capacity by basin and corridor.

Priority: S

## W11S-E21 — Future Power Supply Margin

Fuse:
probability-weighted interconnection queue
+ EIA-860M planned capacity
- retirements/cancellations
vs
load-growth scenarios.

Use:
longer-horizon regional scarcity and power/gas infrastructure state.

Priority: A+

## W11S-E22 — Capacity Pipeline Revision Index

Across oil/gas wells, generation and gas infrastructure compute:
upward revisions
minus
delays/cancellations/withdrawals.

Purpose:
measure whether future physical supply is accelerating or decelerating before realized production changes.

Priority: S

## W11S-E23 — Intent-to-Flow Conversion Engine

Generalize state transitions:
permit/application
-> approval
-> construction/drilling
-> completion/commissioning
-> first flow
-> stable production.

Estimate conversion probability and time distribution separately by asset class.

Priority: S

## Highest-priority W11S tests

1. W11S-E03 Permit-to-Completion Survival
2. W11S-E04 Nightly Completion Momentum
3. W11S-E06 Permit/Frac/Completion Reality Gap
4. W11S-E08 Completion Intensity Supply Nowcast
5. W11S-E12 Interconnection Queue Survival
6. W11S-E14 Gas Generation Buildout Demand
7. W11S-E16 FERC Pipeline Capacity Pipeline
8. W11S-E18 LNG Capacity Ramp
9. W11S-E22 Capacity Pipeline Revision Index
10. W11S-E23 Intent-to-Flow Conversion Engine
