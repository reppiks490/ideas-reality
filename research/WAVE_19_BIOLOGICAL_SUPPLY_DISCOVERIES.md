# Wave 19B — Biological Supply & Quarantine Shocks

Namespace: **W19B**

Thesis: biological events can remove supply through mandatory depopulation, movement controls, quarantine, import restriction, disease-status changes, or cascading recalls before broad production statistics fully adjust. Detection alone is not the edge; the edge is the measurable transition from detection to constrained economic capacity.

All candidates are research hypotheses only. Claude owns any later implementation.

## W19B-E01 — Commercial Poultry HPAI Detection Pulse

Primary source:
USDA APHIS confirmed HPAI detections in commercial/backyard flocks.

Build each commercial event from:
confirmation date,
state/county,
species/production type,
birds affected where available,
premises type.

Separate:
table egg,
broiler,
turkey,
duck,
breeder,
live-bird market,
backyard/noncommercial.

Priority: S

## W19B-E02 — HPAI Bird-Capacity Removal

APHIS response policy uses stamping-out/depopulation for infected poultry and states a goal of depopulation within 24–48 hours or less.

Candidate:
confirmed affected birds
× production type
× expected production contribution
× repopulation lag.

Priority: S

## W19B-E03 — Egg-Layer Capacity Shock

For table-egg operations:
estimate laying-hen capacity removed
relative to
regional/national flock
and current shell-egg inventory.

Validate against:
AMS daily shell egg prices,
weekly inventory,
breaking stock,
processed-egg output.

Priority: S

## W19B-E04 — Turkey / Broiler Supply Shock

Translate infected commercial premises into expected meat-production interruption using:
bird type,
age/production stage if available,
regional slaughter capacity,
replacement-cycle timing.

Priority: A+

## W19B-E05 — HPAI Control-Area Movement Friction

APHIS HPAI control areas use quarantine/movement permitting for animals, eggs, litter, feed and other regulated movements.

State:
INFECTED_PREMISES
CONTACT/SUSPECT
CONTROL_AREA
PERMITTED_MOVEMENT
RELEASED.

Research throughput consequences beyond the depopulated flock itself.

Priority: A+

## W19B-E06 — HPAI Geographic Cluster / Flyway Pressure

Aggregate recent detections by:
county/state,
migratory flyway,
production type,
commercial bird capacity.

Question:
Does spatial clustering improve probability of nearby commercial detections beyond seasonality?

Use only for hazard/risk state, not deterministic prediction.

Priority: A

## W19B-E07 — Wild-Bird-to-Commercial Spillover Hazard

Fuse:
APHIS wild-bird surveillance
+ commercial poultry geography
+ season/flyway
+ recent local detections.

Target:
probability of commercial detection over a short horizon.

Do not use private premise identities if not public.

Priority: A

## W19B-E08 — Dairy Cattle H5N1 Herd Pulse

Primary source:
APHIS confirmed HPAI cases in livestock.

APHIS states the livestock map is updated each weekday and shows recent/cumulative confirmed cases by state.

Build:
new affected herd state
× regional milk production
× movement/testing status.

Priority: A+

## W19B-E09 — Dairy Interstate Movement Friction

APHIS Federal Order/guidance can require testing or alter interstate movement requirements for lactating dairy cattle based on disease status.

Research:
state disease status
-> testing burden
-> interstate movement
-> replacement/heifer logistics
-> milk/cattle flow.

Priority: A

## W19B-E10 — Unaffected-State Status Transition

Under the National Milk Testing Strategy, disease surveillance can change testing/movement obligations.

Treat:
UNAFFECTED
AFFECTED/DETECTED
SURVEILLANCE
REGAINED_STATUS
as regulatory-operational states.

Priority: A

## W19B-E11 — New World Screwworm Proximity Hazard

Primary source:
USDA APHIS screwworm current-status updates.

APHIS publishes case geography/proximity and updates current status on a scheduled basis.

Candidate:
distance of active case to U.S. border
× livestock corridor exposure
× sterile-fly/control status.

Priority: S-

## W19B-E12 — Screwworm Border Trade State

APHIS can suspend, phase-reopen or re-restrict livestock import ports based on screwworm risk.

Build state by port/species:
CLOSED
RESTRICTED
PHASED_REOPEN
OPEN_WITH_PROTOCOL
PAUSED.

Priority: S

## W19B-E13 — Mexico-to-U.S. Feeder Cattle Capacity Shock

Translate screwworm-related import-port restrictions into:
head/day import capacity,
route displacement,
quarantine/treatment cost,
feedlot regional exposure.

Validate against USDA import/cash/feeder-cattle data.

Priority: S

## W19B-E14 — Border Reopening Optionality

A phased port reopening is a future supply-capacity increase, not only a removal of risk.

Feature:
announced/reopened import capacity
-
prior available capacity.

Priority: A+

## W19B-E15 — Animal-Disease Import Restriction Shock

APHIS animal-health status/import alerts can alter eligibility/requirements for live animals or animal products after foreign disease events.

Research:
effective-date restriction
× normal import volume
× substitute origins
× domestic inventory.

Priority: A

## W19B-E16 — Plant-Pest Quarantine Establishment

Primary source:
APHIS Plant Protection and Quarantine federal orders / program updates.

Build each event:
pest/disease,
detection date,
announcement/effective date,
quarantine polygon/area,
commercial acreage/hosts affected,
movement restrictions.

Priority: S-

## W19B-E17 — Fruit-Fly Commercial Acreage Exposure

APHIS fruit-fly quarantine notices can specify square miles and commercial acreage.

Candidate:
commercial acres newly quarantined
× crop value/yield season
× harvest proximity.

Priority: S-

## W19B-E18 — Citrus Disease Quarantine Expansion

For HLB/citrus greening and related citrus disease:
new commercial acres inside quarantine
× crop stage
× packing/transport restrictions
× neighboring citrus density.

Priority: A+

## W19B-E19 — Quarantine Removal / Capacity Release

APHIS also removes quarantine areas after eradication criteria are met.

Treat release as:
reduced movement friction
and
lower biological-risk state.

Priority: A

## W19B-E20 — Detection-to-Quarantine Lag

Measure:
biological detection
-> state quarantine
-> federal order/publication
-> effective restriction.

This availability clock is essential for backtesting.

Priority: A+

## W19B-E21 — Quarantine Perimeter Growth Velocity

Feature:
change in regulated area
and commercial acreage
per unit time.

Hypothesis:
rapid perimeter expansion is more informative than one isolated detection.

Priority: A

## W19B-E22 — FSIS Real-Time Recall / Public Health Alert Pulse

Primary source:
USDA FSIS Recall API.

FSIS says the API provides real-time access to recall/public-health alert information.

Fields include establishment/product/reason/status/distribution and recall details.

Priority: A

## W19B-E23 — Ingredient Recall Propagation Graph

A contaminated ingredient can propagate to multiple downstream meat/poultry products and establishments.

Graph:
ingredient/source
-> receiving establishments
-> products
-> retailers/states
-> recall/alert expansion.

Priority: A+

## W19B-E24 — Recall Expansion Velocity

Track:
initial recall/alert
-> additional products
-> additional states/establishments
-> expanded pounds
-> closure/termination.

Use vintage snapshots; later expansion is new information.

Priority: A

## W19B-E25 — Biological Capacity Loss vs Price Response

For each event:
estimate actual supply capacity removed
before examining futures/spot price.

Examples:
layers removed
feeder cattle imports blocked
commercial citrus acres quarantined
meat pounds recalled.

Priority: S architecture

## W19B-E26 — Substitution Buffer

Biological shock impact depends on:
inventory
imports
alternative regions
cold storage
species/product substitution
production cycle.

Candidate:
capacity_loss / available substitute buffer.

Priority: S

## W19B-E27 — Biological Recovery Clock

Recovery can require:
cleaning/disinfection,
testing,
quarantine release,
repopulation/grow-out,
border reauthorization,
pest eradication generations.

Model expected time-to-capacity restoration separately by event type.

Priority: S

## W19B-E28 — Biological Supply Stress Composite

Combine only validated components:
animal capacity removed
movement/trade restriction
plant acreage constrained
recall propagation
substitution buffer
recovery horizon.

Output:
NORMAL
LOCALIZED
TIGHTENING
MATERIAL_SUPPLY_LOSS
PERSISTENT_BIOLOGICAL_STRESS.

Priority: S

## Highest-priority W19B tests

1. W19B-E02 HPAI Bird-Capacity Removal
2. W19B-E03 Egg-Layer Capacity Shock
3. W19B-E05 HPAI Control-Area Movement Friction
4. W19B-E08 Dairy Cattle H5N1 Herd Pulse
5. W19B-E12 Screwworm Border Trade State
6. W19B-E13 Mexico-to-U.S. Feeder Cattle Capacity Shock
7. W19B-E16 Plant-Pest Quarantine Establishment
8. W19B-E17 Fruit-Fly Commercial Acreage Exposure
9. W19B-E23 Ingredient Recall Propagation Graph
10. W19B-E26 Substitution Buffer
