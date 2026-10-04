# Wave 40B — Border Detention & Import Release Risk

Namespace: **W40B**

Thesis: goods can physically exist, ship successfully, and still be unavailable to the U.S. economy because regulators or customs authorities legally constrain their entry. Import Alerts, detention-without-physical-examination status, Withhold Release Orders, Findings, UFLPA entity status, and final import refusals create a distinct supply state between "produced/shipped" and "commercially available."

The research target is legally constrained import capacity, release probability, substitution, and downstream shortage—not unsupported claims that a specific shipment was detained when public sources do not identify it.

All candidates are research hypotheses only. Claude owns implementation.

## W40B-E01 — FDA Import Alert State

Primary source:
FDA Import Alerts.

FDA states its Import Alert databases are updated in real time.

Normalize:
ACTIVE_DWPE
EXEMPT_GREEN_LIST
RED_OR_YELLOW_LIST
DEACTIVATED
REPLACED
UNKNOWN.

Priority: S

## W40B-E02 — Import Alert Inclusion Shock

Event:
firm/product/country newly becomes subject to DWPE.

Estimate exposure:
historical U.S. import dependence
× supplier share
× product criticality.

Priority: S

## W40B-E03 — Import Alert Removal / Remediation Shock

Event:
firm/product removed from Red/Yellow List or otherwise becomes exempt from DWPE.

Research:
time from restriction to remediation
and
post-removal import recovery.

Priority: S-

## W40B-E04 — Green-List Exemption Loss

For alerts using Green Lists:
removal from Green List can mean the firm/product becomes subject to DWPE.

Treat as a deterioration event distinct from Red-List addition.

Priority: A+

## W40B-E05 — DWPE Scope Expansion

Track changes in:
firm,
product,
country,
facility,
importer/manufacturer combinations.

Feature:
newly constrained share of previously eligible supply.

Priority: S

## W40B-E06 — DWPE Constraint Severity

DWPE is not an absolute import ban:
an importer may attempt to overcome the appearance of violation for an individual shipment.

Estimate:
expected release probability
× documentation burden
× substitute-source availability.

Priority: A+

## W40B-E07 — FDA Import Refusal Velocity

Primary source:
FDA Import Refusals Dashboard.

FDA states this dataset is updated weekly and contains final actions.

Features:
new final refusals,
country/product/manufacturer breadth,
reason/charge concentration.

Priority: A as delayed confirmation

## W40B-E08 — Refusal Reason Transition

Classify final refusal causes:
adulteration,
misbranding,
GMP/registration,
pathogen/contamination,
unapproved product,
labeling,
other.

Research which cause families lead to persistent supply impairment.

Priority: A

## W40B-E09 — Import Alert -> Refusal Realization

For each firm/product alert:
later final refusal count/value proxy where public.

Target:
probability that an eligibility restriction translates into observed final refusal activity.

Priority: S-

## W40B-E10 — Pharma/API Import Constraint

Map FDA drug/API import alerts to:
manufacturer,
site,
active ingredient,
finished drug,
U.S. shortage exposure.

Fuse with W36P.

Priority: S

## W40B-E11 — Medical Device Import Constraint

Map device alerts/refusals to:
device category,
criticality,
alternative suppliers,
U.S. shortage/discontinuance lists where available.

Priority: A+

## W40B-E12 — Food / Protein Import Constraint

Fuse FDA food/seafood import alerts with W19B/W31F.

Target:
import availability,
domestic substitution,
cold-chain/processing consequences.

Priority: A

## W40B-E13 — Critical Input Constraint

Map import restrictions to upstream inputs:
copper,
aluminum,
polysilicon,
battery materials,
chemical intermediates,
industrial components.

Priority: A+

## W40B-E14 — CBP Withhold Release Order State

Primary source:
CBP Withhold Release Orders & Findings.

CBP issues a WRO when reasonable suspicion exists that goods were produced with forced labor.

State:
ACTIVE_WRO
MODIFIED
REVOKED/REMOVED
SUPERSEDED
UNKNOWN.

Priority: S

## W40B-E15 — WRO Immediate Supply Eligibility Shock

CBP press releases can make new WROs effective immediately at all U.S. ports of entry.

Estimate:
affected supplier/product share
× U.S. import dependence
× substitute capacity.

Priority: S

## W40B-E16 — Finding Escalation

CBP Finding is stronger than WRO:
CBP states a Finding allows seizure of covered goods.

State transition:
WRO/INVESTIGATION
-> FINDING
-> MODIFIED/REMOVED.

Priority: S-

## W40B-E17 — WRO Modification / Release Shock

When CBP modifies a WRO after remediation:
goods may again enter if otherwise compliant.

Measure:
restriction duration
and
post-modification import recovery.

Priority: S-

## W40B-E18 — WRO Commodity Concentration

Aggregate active WRO exposure by:
commodity,
country,
supplier,
downstream industry.

Priority: A+

## W40B-E19 — UFLPA Entity-List Shock

Primary source:
DHS Forced Labor Enforcement Task Force / UFLPA Entity List.

Event:
entity addition/removal/effective-date change.

Map:
entity
-> sector
-> upstream/downstream supplier graph
-> U.S. import exposure.

Priority: S

## W40B-E20 — UFLPA Sector Enforcement Breadth

Primary source:
CBP UFLPA enforcement statistics.

Use aggregated public data for:
shipment counts,
value,
status/outcome,
country,
sector where exposed.

Priority: A

## W40B-E21 — UFLPA Denial Rate

Candidate:
denied shipments
/
resolved reviewed shipments

by sector/country/time.

Hard rule:
dashboard aggregates do not identify specific companies/shipments.

Priority: A+

## W40B-E22 — UFLPA Pending-Review Pressure

Feature:
pending or unresolved reviewed shipment count/value
relative to historical norm.

Interpret as regulatory-friction stock, not confirmed supply loss.

Priority: A

## W40B-E23 — Solar / Polysilicon Border Risk

Fuse UFLPA electronics enforcement with:
verified solar supply-chain entity exposure,
domestic module/cell inventory,
project pipeline.

Do not label all "electronics" as solar.

Priority: S-

## W40B-E24 — Auto / Battery Material Border Risk

Map entity/sector restrictions to:
battery cells,
critical minerals,
automotive components
only where product lineage is sourced.

Priority: A

## W40B-E25 — Palm Oil / Food Input Border Risk

Map WRO/Findings affecting palm oil or derivative goods to:
food,
oleochemicals,
consumer products,
substitute oils.

Priority: A

## W40B-E26 — Copper / Metal Border Risk

Map metal-specific WROs to:
U.S. refined/semi-finished import exposure,
alternate origin capacity,
inventory.

Priority: A+

## W40B-E27 — Legal Eligibility vs Physical Arrival Gap

Fuse W32R:
cargo can arrive at a U.S. port while entry remains constrained.

State:
ARRIVED_BUT_ELIGIBILITY_UNKNOWN
vs
LEGAL_RESTRICTION_ACTIVE
vs
RELEASE_CONFIRMED where public.

Never infer a specific entry outcome without a public source.

Priority: S architecture

## W40B-E28 — Import Restriction Substitution Quotient

IRSQ =
expected constrained import capacity
/
verified substitute supply capacity.

Substitution:
other foreign supplier,
domestic production,
inventory,
alternative product/material.

Priority: S

## W40B-E29 — Border Constraint Recovery Half-Life

After an alert/WRO/entity restriction is removed:
measure time to:
import recovery,
inventory normalization,
shortage resolution,
price/basis normalization.

Priority: A+

## W40B-E30 — Restriction Revision Velocity

Track additions/removals/modifications across:
FDA Import Alerts,
CBP WROs/Findings,
UFLPA Entity List.

Feature:
net newly constrained supplier/product exposure per week/month.

Priority: S-

## W40B-E31 — Border Risk Supply Graph

Graph:
foreign site/entity
-> product/input
-> importer/brand/manufacturer where public
-> domestic plant/customer
-> inventory/substitute.

Priority: S

## W40B-E32 — Border Constraint Reality Gap

Compare:
legal restriction state
vs
shortage/inventory/price response.

Large restriction with no downstream effect may indicate substitution or low exposure.

Priority: A+

## W40B-E33 — Cross-Regulator Supplier Stress

Same foreign site/entity may face:
FDA alert,
CBP forced-labor restriction,
sanctions/export-control issue,
quality action.

Count only independent authorities/events.

Priority: A

## W40B-E34 — Border Release Truth Ladder

REGULATORY LIST/ORDER
-> ENTRY ELIGIBILITY CONSTRAINT
-> ACTUAL PUBLICLY CONFIRMED REFUSAL/DENIAL
-> IMPORT VOLUME LOSS
-> INVENTORY SHORTAGE
-> SUBSTITUTE RESPONSE
-> PRICE/MARKET EFFECT.

Priority: S architecture

## Highest-priority W40B tests

1. W40B-E02 Import Alert Inclusion Shock
2. W40B-E05 DWPE Scope Expansion
3. W40B-E09 Import Alert -> Refusal Realization
4. W40B-E10 Pharma/API Import Constraint
5. W40B-E15 WRO Immediate Supply Eligibility Shock
6. W40B-E19 UFLPA Entity-List Shock
7. W40B-E21 UFLPA Denial Rate
8. W40B-E28 Import Restriction Substitution Quotient
9. W40B-E31 Border Risk Supply Graph
10. W40B-E34 Border Release Truth Ladder
