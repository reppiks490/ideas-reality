# RDX08 — Well Realization & Future Hydrocarbon Supply

Thesis: drilling permits are real options, not production. Public state/federal data expose a chain from permit application to approval, spud, hydraulic-fracture disclosure, completion/recompletion filings, transporter authorization and delayed production. The edge is the probability and timing of each conversion, combined with well productivity and takeaway capacity.

## RDX08-E01 — New Permit Pulse
Nightly/state or periodic approved drilling permits by basin/operator/well type.

## RDX08-E02 — Permit Approval Velocity
Approved permits per operator/basin normalized by historical seasonality and acreage position.

## RDX08-E03 — Permit Quality
Weight permit by lateral/profile, target field/formation, operator historical productivity and proximity to existing infrastructure.

## RDX08-E04 — Permit-to-Spud Hazard
P(well starts drilling within N days | operator, basin, permit age, commodity price, rig availability).

## RDX08-E05 — Permit Expiry / Dormancy
Approved permits aging without spud as unrealized supply option.

## RDX08-E06 — Federal APD Available-to-Drill State
BLM approved-and-available permits are separate from pending/processed APDs.

## RDX08-E07 — Federal Permit Inventory Draw
Available-to-drill APD inventory declining/rising versus federal-land rig activity.

## RDX08-E08 — Spud Pulse
Newly spudded wells by operator/basin where state data expose start activity.

## RDX08-E09 — Rig-to-Spud Efficiency
Spuds per active rig / rig-days; productivity of drilling organization rather than raw rig count.

## RDX08-E10 — Spud-to-Completion Hazard
P(completion in N days | basin, operator, lateral, drilling date, service conditions).

## RDX08-E11 — DUC Inventory
Drilled-uncompleted well probability distribution, not a single stale aggregate count.

## RDX08-E12 — DUC Aging
Age distribution and operator-specific completion hazard.

## RDX08-E13 — Frac Disclosure Pulse
FracFocus new disclosures refreshed five days/week; map well API, operator, fracture dates and treatment details.

## RDX08-E14 — Frac Disclosure Availability Lag
Disclosure submission/publication can occur after actual fracture date. Learn lag by jurisdiction/operator before using as live signal.

## RDX08-E15 — Frac-to-First-Production Hazard
Expected time from treatment/completion evidence to first sale/production.

## RDX08-E16 — Texas Nightly Completion-Form Pulse
RRC nightly data include G-1/W-2 and related completion/recompletion forms submitted/approved previous day.

## RDX08-E17 — Submitted-vs-Approved Completion
Submission, approval and physical completion are separate clocks.

## RDX08-E18 — Completion Rework / Recompletion
Separate new-well completion from recompletion/workover, which has different incremental supply.

## RDX08-E19 — P-4 Transport Authorization State
Texas Producer's Transportation Authority / Certificate of Compliance as one commercialization/readiness milestone.

## RDX08-E20 — Completion-to-Production Confirmation
Later monthly production validates realized supply; never backdate it to completion filing.

## RDX08-E21 — First-Production Nowcast
Predict first-production month and initial volume from pre-production milestones.

## RDX08-E22 — Type-Curve Prior
Operator/formation/lateral-specific initial production and decline prior.

## RDX08-E23 — New-Well Production Capacity
Probability-weighted upcoming first production × expected initial rate.

## RDX08-E24 — Operator Execution Score
Historical permit->spud->completion->first-production conversion, delay and productivity.

## RDX08-E25 — Basin Execution Score
Same conversion metrics by basin/formation.

## RDX08-E26 — Completion Crew Constraint
Spuds accumulate faster than completions when frac/service capacity becomes binding.

## RDX08-E27 — Rig Constraint
Permit inventory grows but spud rate stalls when drilling capacity is constrained.

## RDX08-E28 — Takeaway Constraint
New well capacity × available pipeline/gathering/processing capacity; supply can be stranded/curtailed.

## RDX08-E29 — Gas Processing Constraint
Wet gas/NGL-rich wells require processing capacity; model plant/pipeline exposure.

## RDX08-E30 — Flare/Vent Exception State
Texas nighttime Rule 32 exception data can indicate temporary takeaway/operational constraint; do not equate exception with actual flared volume.

## RDX08-E31 — First-Sales Infrastructure Readiness
Gathering connection / transporter authorization / pipeline availability as commercialization layer.

## RDX08-E32 — Operator Permit Hoarding
High permit inventory with low historical conversion as weak future-supply signal.

## RDX08-E33 — Permit Acceleration Surprise
Permit approvals exceed operator/basin expected cadence conditioned on prices/acreage.

## RDX08-E34 — Completion Acceleration Surprise
Nightly completion filings exceed expected cadence and DUC pool.

## RDX08-E35 — Supply Start-Date Distribution
Aggregate each well's first-production probability into daily/monthly basin supply additions.

## RDX08-E36 — Decline-Offset Requirement
New-well additions minus expected legacy decline.

## RDX08-E37 — Net Basin Supply Growth
Probability-weighted new supply − decline − curtailment.

## RDX08-E38 — Oil-vs-Gas Cross-Product Supply
Associated gas from oil wells and liquids from gas wells can alter both markets; model multiproduct yields.

## RDX08-E39 — New Supply × Storage/Inventory
Same supply revision has different price impact depending on inventory/storage state.

## RDX08-E40 — New Supply × Pipeline Basis
Basin supply growth relative to takeaway predicts local basis/bottleneck pressure before benchmark effect.

## RDX08-E41 — ND Daily Activity State
North Dakota daily reports provide current permit/activity events; use as Bakken-specific fast layer.

## RDX08-E42 — ND Confidential/Tight-Hole Mask
Confidential status can hide details; missing data is not inactivity.

## RDX08-E43 — State Cross-Validation
Compare Texas/ND methodologies before combining; definitions/reporting clocks differ.

## RDX08-E44 — Permit-to-Barrel Conversion Quotient
PBCQ = probability-weighted incremental first-year production / raw permitted capacity or permit count.

## RDX08-E45 — Future Hydrocarbon Supply Tensor
Dimensions: basin, operator, product, milestone, completion probability, start date, expected IP, decline, takeaway constraint.

## RDX08-E46 — Supply Realization Revision
Change in future supply distribution caused by a new permit/spud/frac/completion/constraint event.

## RDX08-E47 — Producer Guidance Reality Gap
Company production/capex guidance versus public well-milestone realization.

## RDX08-E48 — Well Truth Ladder
PERMIT -> SPUD -> DRILL -> FRAC -> COMPLETION PAPERWORK -> TRANSPORT/CONNECTION -> FIRST PRODUCTION -> STABILIZED OUTPUT -> DECLINE.

## Highest-priority tests
E04, E10, E14, E15, E21, E24, E28, E35, E44, E48.
