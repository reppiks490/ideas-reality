# Wave 57L — LNG Commissioning & Feedgas Step-Change

Namespace: **W57L**

Thesis: LNG export terminals do not jump from "under construction" to "fully operational." They progress through public regulatory and engineering milestones that can expose an approaching step-change in domestic natural-gas demand before backward-looking export statistics fully reflect it.

This wave owns the **terminal-side commissioning state machine**. W22G remains owner of interstate-pipeline transport constraints, nomination cycles, linepack and capacity.

All candidates are research hypotheses only. Claude owns later implementation.

## W57L-E01 — FERC Commissioning Permission State

Primary source:
FERC eLibrary / project dockets.

Normalize delegated orders and notices authorizing:
COMMISSION_SYSTEM
INTRODUCE_HAZARDOUS_FLUIDS
INTRODUCE_FEED_GAS
COMMISSION_LIQUEFACTION_BLOCK
COMMISSION_TANK
COMMISSION_BOG
COMMISSION_FLARE
PLACE_FACILITY_IN_SERVICE.

Priority: S

## W57L-E02 — Hazardous-Fluid Introduction Progression

FERC permissions to introduce hazardous fluids can mark the transition from static construction toward active process commissioning.

Build:
count/capacity of terminal systems newly authorized
/
total required commissioning systems.

Priority: S

## W57L-E03 — Train / Block Commissioning Breadth

Map every regulatory milestone to exact:
train,
liquefaction block,
storage tank,
utility system,
pipeline/interconnect.

Output:
fraction of design liquefaction capacity in ACTIVE_COMMISSIONING.

Priority: S

## W57L-E04 — First-Gas Clock

Track first public evidence that feed gas is admitted to terminal systems.

Separate:
authorization to introduce gas
from
observed/announced actual gas introduction.

Priority: S

## W57L-E05 — Cooldown Cargo State

Some terminals may receive imported LNG or use inventory to cool tanks/piping before export.

State:
NO_COOLDOWN
COOLDOWN_REQUESTED
COOLDOWN_AUTHORIZED
COOLDOWN_UNDERWAY
COOLDOWN_COMPLETE.

Priority: A+

## W57L-E06 — First-LNG Production State

Operator/FERC evidence that first LNG has been produced by a train/block.

This is later than construction completion but earlier than stable commercial operation.

Priority: S

## W57L-E07 — First Export Cargo State

Track first commissioning/export cargo:
loading start,
sail date,
volume if public,
destination if public.

Do not equate first cargo with full run-rate.

Priority: S

## W57L-E08 — Train Substantial Completion State

Example operator semantics:
construction/commissioning complete,
care/custody/control transferred from EPC contractor.

This can change accounting/economic ownership before full project completion.

Priority: A+

## W57L-E09 — Commercial Operation Date State

Separate:
first gas,
first LNG,
first cargo,
substantial completion,
commercial operation.

Each milestone has different feedgas and financial meaning.

Priority: S

## W57L-E10 — Commissioning Ramp Curve

Estimate expected feedgas demand by days since:
first gas,
first LNG,
first cargo,
or train substantial completion.

Use train-specific historical commissioning analogs.

Priority: S

## W57L-E11 — Ramp Acceleration Surprise

Feature:
observed feedgas-ramp slope
-
expected train-specific commissioning slope.

Priority: S-

## W57L-E12 — Ramp Stall Hazard

Detect:
feedgas stops increasing,
commissioning authorizations pause,
cargo cadence stalls,
operator milestones slip.

Target:
probability of delayed next train/block milestone.

Priority: S

## W57L-E13 — Regulatory Milestone Velocity

Feature:
number and capacity-weighted importance of new FERC commissioning permissions per 7/14/30 days.

Question:
does milestone acceleration predict near-term feedgas step-up?

Priority: A+

## W57L-E14 — Regulatory Silence Hazard

For a project that should be advancing:
time since last expected commissioning permission
relative to historical milestone cadence.

Silence is not automatically a delay; validate against project phase and public schedule.

Priority: A

## W57L-E15 — Train-by-Train Feedgas Shadow Demand

For every newly commissioning train/block:
expected incremental feedgas at stable run rate
× probability of reaching that state by horizon.

Aggregate:
expected new feedgas demand next 7/30/90 days.

Priority: S

## W57L-E16 — Feedgas Step vs Pipeline Capacity

Fuse W57L expected terminal demand with W22G:
available pipeline capacity,
maintenance,
OFOs,
linepack,
scheduled volumes.

Output:
terminal-ramp transport tightness.

Priority: S

## W57L-E17 — Feedgas Step vs Storage

Expected terminal demand increase
× storage inventory/deviation
× injection/withdrawal season.

Target:
storage-balance impact before weekly EIA statistics fully realize the ramp.

Priority: S

## W57L-E18 — Feedgas Step vs Power Burn

Higher LNG feedgas competes with domestic gas demand.

Condition on:
temperature,
power-sector gas burn,
coal/nuclear/hydro availability,
pipeline basis.

Priority: S-

## W57L-E19 — Gulf Coast Basis Pressure

Map terminal ramp to economically connected pipelines/hubs.

Validate first against local/regional basis before Henry Hub or broad futures.

Priority: S

## W57L-E20 — Commissioning Cargo Cadence

Track interval between initial LNG cargoes.

Feature:
cargo cadence acceleration
as physical confirmation of ramp.

Priority: A+

## W57L-E21 — Cargo Size / Run-Rate Consistency

Compare exported cargo volume/cadence to estimated terminal output.

Use as a noisy downstream validation of feedgas/liquefaction ramp.

Priority: A

## W57L-E22 — DOE Export Authorization State

Primary source:
DOE Hydrocarbons and Geothermal Energy Office.

Normalize:
APPLICATION
FTA_AUTHORIZATION
NON_FTA_AUTHORIZATION
AMENDMENT
VACATE
BLANKET_IMPORT
BLANKET_EXPORT
CONTRACT_REGISTRATION.

Priority: A

## W57L-E23 — Authorization vs Physical Readiness Gap

DOE export authorization does not imply a terminal is physically ready.

Feature:
regulatory commercial authority
minus
FERC/physical commissioning progress.

Priority: A+

## W57L-E24 — Long-Term Contract Coverage State

DOE publishes long-term LNG delivery and natural-gas supply contract information for authorized facilities.

Estimate:
contracted volume
/
authorized or design capacity.

Use only point-in-time public contract filings.

Priority: A+

## W57L-E25 — Contracted Ramp vs Uncontracted Optionality

Distinguish:
capacity backed by long-term sales
vs
merchant/spot optionality.

Question:
does early cargo cadence differ by contract coverage?

Priority: A

## W57L-E26 — FERC Project Schedule Revision

Track public target dates in FERC construction/progress filings.

Feature:
new expected milestone date
-
prior expected date.

Priority: S-

## W57L-E27 — Operator-vs-Regulator Schedule Gap

Compare company-announced startup targets with:
FERC filing milestones,
actual authorization cadence,
observed feedgas/cargo state.

Priority: S

## W57L-E28 — Commissioning Surprise Index

Fuse:
regulatory acceleration,
feedgas acceleration,
cargo acceleration,
schedule revisions,
operator guidance.

Output:
AHEAD_OF_EXPECTATION
ON_TRACK
AT_RISK
DELAYED.

Priority: S

## W57L-E29 — Terminal Availability Shock

After commissioning:
detect forced reduction from normal LNG feedgas/export state.

Route operational terminal outages back to W22G/W15X where transport/industrial-event ownership applies.

W57L owns only the terminal-state transition and ramp context.

Priority: A+

## W57L-E30 — New-Capacity Storage Draw Equivalent

Translate expected incremental LNG feedgas into:
Bcf/day,
Bcf/week,
share of normal seasonal storage change.

Priority: S

## W57L-E31 — New-Capacity Price Sensitivity Envelope

Use structural scenarios rather than direct price prediction:
incremental feedgas demand
× supply elasticity
× storage tightness
× local transport constraint.

Priority: S

## W57L-E32 — LNG Startup Truth Ladder

DOE AUTHORITY
-> FERC CONSTRUCTION/COMMISSIONING PERMISSION
-> FIRST GAS
-> FIRST LNG
-> FIRST CARGO
-> SUBSTANTIAL COMPLETION
-> COMMERCIAL OPERATION
-> STABLE RUN RATE
-> OBSERVED STORAGE/BASIS EFFECT.

Priority: S architecture

## Highest-priority W57L tests

1. W57L-E02 Hazardous-Fluid Introduction Progression
2. W57L-E03 Train / Block Commissioning Breadth
3. W57L-E10 Commissioning Ramp Curve
4. W57L-E12 Ramp Stall Hazard
5. W57L-E15 Train-by-Train Feedgas Shadow Demand
6. W57L-E16 Feedgas Step vs Pipeline Capacity
7. W57L-E17 Feedgas Step vs Storage
8. W57L-E27 Operator-vs-Regulator Schedule Gap
9. W57L-E28 Commissioning Surprise Index
10. W57L-E32 LNG Startup Truth Ladder
