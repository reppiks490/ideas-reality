# Wave 58A — Animal Disease & Biological Capacity Loss

Namespace: **W58A**

Thesis: animal disease can destroy productive biological capital, restrict movement/trade, and create recovery lags that are observable before conventional monthly livestock statistics fully update. The important state is not merely "disease detected"; it is **productive capacity removed, replacement time, geographic concentration, trade restriction, and substitute supply**.

All candidates are research hypotheses only. Claude owns later implementation.

## W58A-E01 — APHIS Commercial-Flock HPAI Shock

Primary source:
USDA APHIS HPAI commercial/backyard flock confirmations.

For commercial flocks:
confirmation date,
state/county,
species/production type where public,
birds affected/depopulated where public.

Priority: S

## W58A-E02 — Layer-Hen Capacity Loss

Estimate:
affected egg-laying hens
/
current national and regional layer inventory.

Use NASS point-in-time inventory denominator.

Priority: S

## W58A-E03 — Broiler Capacity Loss

Separate broiler breeder, hatchery and grow-out exposure.

Direct bird count alone may not equal near-term meat output impact.

Priority: A+

## W58A-E04 — Turkey Capacity Loss

Map HPAI events to turkey production geography and seasonal demand.

Validate against AMS/NASS slaughter and market data.

Priority: A+

## W58A-E05 — Flock Depopulation Timing

Where public response data permit:
confirmation
-> quarantine
-> depopulation
-> disposal/cleaning
-> restocking eligibility.

Priority: S

## W58A-E06 — Biological Replacement Clock

Estimate time from flock removal to productive replacement.

For layers:
pullet/hatchery pipeline matters.
For broilers/turkeys:
breeder/hatchery/grow-out cycle differs.

Priority: S

## W58A-E07 — Replacement-Pipeline Sufficiency

Use NASS hatchery/pullet data to estimate whether replacement capacity is sufficient to rebuild lost productive flock on normal timing.

Priority: S

## W58A-E08 — Layer Inventory Recovery Forecast

Forecast future laying-hen inventory from:
depopulation,
pullet placements,
historical maturation,
normal attrition,
restocking constraints.

Priority: S

## W58A-E09 — Egg Production Recovery Forecast

Translate layer inventory and eggs-per-layer into projected egg production.

Validate against monthly NASS Chickens and Eggs.

Priority: S

## W58A-E10 — HPAI Supply Shock × Egg Demand

Disease loss has larger price effect under strong seasonal/holiday demand.

Fuse:
lost layers
× demand seasonality
× shell-egg inventories/imports.

Priority: S-

## W58A-E11 — Cage-Free Constraint Amplifier

Cage-free legal/retailer sourcing requirements can reduce substitutability after regional HPAI loss.

Estimate:
cage-free productive capacity lost
/
available cage-free substitute supply.

Priority: A+

## W58A-E12 — Wholesale Egg Price Transmission

Use USDA AMS Market News.

Track:
wholesale shell egg price,
product size/grade,
region,
availability/offering language,
retail lag.

Priority: S

## W58A-E13 — Poultry Market Tightness Breadth

Fuse HPAI capacity loss with AMS:
egg,
broiler,
turkey,
cold-storage/slaughter indicators.

Priority: A+

## W58A-E14 — HPAI Geographic Production Concentration

Weight detections by state/county production share rather than raw case count.

Priority: S

## W58A-E15 — Wild-Bird Spillover Pressure

APHIS wild-bird surveillance can provide environmental/spillover context.

Use only as hazard context; wild-bird detections are not commercial-capacity loss.

Priority: B+

## W58A-E16 — Dairy-Herd H5 State

Primary source:
APHIS HPAI livestock confirmations + National Milk Testing Strategy.

Track affected/unaffected state status and confirmed dairy herds.

Priority: S-

## W58A-E17 — Dairy Movement-Restriction State

Federal orders require testing for interstate movement of lactating dairy cattle and mandate reporting of positives.

Research:
movement friction
× affected herd geography
× milk/cattle flow.

Priority: A+

## W58A-E18 — Bulk-Milk Surveillance Transition

NMTS stages provide state-level disease-presence/absence progression.

Feature:
state status transition
and days since last confirmed herd.

Priority: A

## W58A-E19 — Milk Production Reality Gap

Compare H5 herd state to:
USDA milk production,
cow numbers,
milk per cow,
dairy-product output.

Question:
does disease state predict local/national production deviation?

Priority: A+

## W58A-E20 — New World Screwworm Livestock Shock

Primary source:
APHIS/Screwworm.gov confirmed animal/fly detections.

Track:
county,
species,
confirmation date,
active/inactive case,
distance to production/import corridors.

Priority: S-

## W58A-E21 — Cattle Import Port Restriction State

APHIS can close/reopen southern livestock ports based on NWS risk.

State:
CLOSED
PHASED_REOPEN
OPEN_WITH_PROTOCOL
NORMAL.

Priority: S

## W58A-E22 — Mexico Feeder-Cattle Import Loss

Use AMS weekly U.S.–Mexico livestock import reports.

Measure:
actual feeder-cattle imports
vs
seasonal expectation
following port restrictions/reopening.

Priority: S

## W58A-E23 — Import Restriction Recovery Ramp

Port reopening does not imply immediate normal cattle flow.

Track:
inspection capacity,
protocol restrictions,
weekly head counts,
price spreads.

Priority: A+

## W58A-E24 — Live-Cattle Supply Substitution

Lost Mexican feeder-cattle inflow
/
available domestic or Canadian substitute supply.

Priority: S-

## W58A-E25 — WOAH Global Outbreak Shock

Primary source:
World Organisation for Animal Health WAHIS.

Immediate notifications include:
disease,
affected species,
geography,
control measures,
laboratory status.

Use for foreign supply/trade disruptions.

Priority: S

## W58A-E26 — Foreign Disease Regionalization / Trade Ban State

Map disease event to importing-country restrictions:
countrywide ban,
regional ban,
product-specific ban,
vaccination/processing exemption,
reopening.

Priority: S

## W58A-E27 — Disease-Driven Export Diversion

If destination market restricts origin:
estimate displaced poultry/meat/dairy volume
and likely alternate destinations/domestic overhang.

Priority: A+

## W58A-E28 — Disease-Driven Import Substitution

Domestic capacity loss may increase imports if sanitary rules and external supply permit.

Priority: A+

## W58A-E29 — Feed-Demand Secondary Shock

Large poultry/swine herd/flock losses reduce feed demand.

Map:
animals removed
× expected feed consumption
to corn/soymeal demand scenarios.

Priority: A

## W58A-E30 — Animal Disease Capacity-Loss Quotient

ADCLQ =
productive biological capacity removed
/
replacement + import + substitute protein capacity.

Priority: S

## W58A-E31 — Biological Recovery Half-Life

Estimate time until:
productive animal count,
output,
trade flow,
and prices
normalize.

Priority: S

## W58A-E32 — Disease Truth Ladder

DETECTION
-> QUARANTINE/MOVEMENT CONTROL
-> DEPOPULATION/CAPACITY LOSS
-> REPLACEMENT PIPELINE
-> OUTPUT LOSS
-> TRADE RESTRICTION/SUBSTITUTION
-> PRICE/INVENTORY EFFECT
-> RECOVERY.

Priority: S architecture

## Highest-priority W58A tests

1. W58A-E02 Layer-Hen Capacity Loss
2. W58A-E06 Biological Replacement Clock
3. W58A-E07 Replacement-Pipeline Sufficiency
4. W58A-E08 Layer Inventory Recovery Forecast
5. W58A-E10 HPAI Supply Shock × Egg Demand
6. W58A-E16 Dairy-Herd H5 State
7. W58A-E21 Cattle Import Port Restriction State
8. W58A-E22 Mexico Feeder-Cattle Import Loss
9. W58A-E26 Foreign Disease Regionalization / Trade Ban State
10. W58A-E30 Animal Disease Capacity-Loss Quotient
