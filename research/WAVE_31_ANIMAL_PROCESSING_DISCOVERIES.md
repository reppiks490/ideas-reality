# Wave 31F — Animal Processing & Protein Supply Capacity

Namespace: **W31F**

Thesis: livestock and protein markets can be constrained by the conversion layer between live animals and finished meat. A slaughter/processing bottleneck can create opposite effects upstream and downstream: live-animal backlogs may pressure cattle/hog prices while wholesale meat tightens. Disease-control and import restrictions can also alter feeder/live-animal supply before conventional monthly statistics reveal the full effect.

All candidates are research hypotheses only. Claude owns any later implementation.

## W31F-E01 — Daily Federally Inspected Slaughter Residual
Primary: USDA AMS Daily Livestock and Poultry Slaughter.
Compute estimated slaughter minus weekday/holiday/seasonal expected slaughter by species.
Priority: S

## W31F-E02 — Week-to-Date Processing Deficit
Compare current WTD slaughter with prior week, year-ago and seasonal expected.
Priority: S

## W31F-E03 — Saturday Catch-Up Intensity
Saturday slaughter relative to normal Saturday baseline conditioned on weekday deficit.
Priority: A+

## W31F-E04 — Hog Scheduled-Delivery Queue
USDA AMS National Daily Direct Hog Prior Day Report publishes future dates/head counts scheduled for delivery to packing plants.
Priority: S

## W31F-E05 — Hog Queue Pressure Ratio
HQPR = scheduled hog deliveries over next N days / expected available slaughter capacity.
Priority: S

## W31F-E06 — Cattle Processing Capacity Tightness
Market-ready fed cattle supply / effective steer-heifer slaughter capacity.
Priority: S

## W31F-E07 — Live-Animal / Meat Divergence
Detect states where slaughter capacity falls, wholesale meat tightens and live-animal prices weaken from backlog.
Priority: S

## W31F-E08 — Packer Margin Shock
Wholesale carcass/cutout value minus implied live-animal acquisition cost minus normal processing cost, conditioned on capacity utilization.
Priority: A+

## W31F-E09 — Processing Bottleneck Regime
ANIMAL_SHORTAGE / BALANCED / PACKER_CAPACITY_TIGHT / MEAT_SHORTAGE / RECOVERY.
Priority: S

## W31F-E10 — Estimated-to-Actual Slaughter Revision
Use later actual federally inspected slaughter to calibrate uncertainty in same-day estimates.
Priority: A

## W31F-E11 — Species/Class Mix Shift
Track cattle classes and hog classes versus seasonal baselines.
Priority: A

## W31F-E12 — Carcass Weight Compensation
Head-count shock versus dressed-weight shock versus meat pounds.
Priority: A+

## W31F-E13 — Effective Meat Output
Slaughter head × dressed weight × usable production factor; validate against meat production.
Priority: S-

## W31F-E14 — FSIS Inspection Suspension State
NORMAL / NOIE / WITHHOLDING / SUSPENSION_IN_EFFECT / SUSPENSION_ABEYANCE / CLOSED.
Priority: S-

## W31F-E15 — Whole-Plant vs Process-Specific Suspension
Estimate only affected process/species; not every suspension is whole-plant.
Priority: S methodology/edge hybrid

## W31F-E16 — FSIS Reinstatement / Abeyance Recovery
Track suspension -> corrective plan -> abeyance -> closure/normal operation.
Priority: A

## W31F-E17 — Establishment Capacity Map
FSIS MPI Directory + Establishment Demographic Data provide weekly location/species/size/activity structure.
Priority: S infrastructure

## W31F-E18 — Active-to-Inactive Establishment Transition
Archive weekly MPI vintages and detect active/inactive transitions as slow structural capacity changes.
Priority: A

## W31F-E19 — Regional Slaughter Concentration
Estimate species-specific processing concentration by state, region, owner and plant.
Priority: S-

## W31F-E20 — Large-Plant Shock Severity
LPSS = estimated affected daily head capacity / national species slaughter capacity.
Priority: S

## W31F-E21 — HPAI Commercial Flock Capacity Loss
Confirmed infected commercial poultry premises can be quarantined/depopulated under APHIS response policy.
Priority: S-

## W31F-E22 — HPAI Control-Area Spillover
Estimate movement/logistics capacity affected beyond infected premises without assuming all premises are depopulated.
Priority: A+

## W31F-E23 — HPAI Depopulation-to-Restock Gap
Detection -> depopulation -> control-area release -> restock -> production normalization.
Priority: A+

## W31F-E24 — New World Screwworm Cattle-Import Gate
Track APHIS port states: CLOSED / PHASED_REOPEN / OPEN_WITH_PROTOCOL / PAUSED_AFTER_DETECTION.
Priority: S

## W31F-E25 — Mexico Feeder-Cattle Supply Shock
Normal Mexican cattle imports minus currently permitted/realized flow, propagated through feedlot lag to later slaughter.
Priority: S

## W31F-E26 — Border Port Reopening Capacity Ramp
Track port, effective date, inspection/protocol constraints and actual crossing volume where public.
Priority: A+

## W31F-E27 — Disease / Processing Collision
Model joint states where animal supply and slaughter capacity are impaired simultaneously.
Priority: S

## W31F-E28 — Cold Storage Buffer
Use USDA NASS monthly frozen beef/pork/poultry stocks as lagged buffer state.
Priority: A

## W31F-E29 — Meat Scarcity vs Animal Backlog Index
MSABI = downstream meat scarcity - upstream live-animal scarcity.
Priority: S

## W31F-E30 — Protein Substitution Pressure
Map shocks across beef, pork, chicken and turkey.
Priority: A+

## W31F-E31 — Processing Recovery Half-Life
Time to normalization of slaughter, backlog, cutout, cash livestock and cold storage.
Priority: A+

## W31F-E32 — Animal-to-Meat Conversion Truth Ladder
LIVE SUPPLY -> SLAUGHTER CAPACITY -> SLAUGHTER ACTIVITY -> MEAT PRODUCTION -> INVENTORY -> WHOLESALE SPREAD -> MARKET.
Priority: S architecture

## Highest-priority W31F tests
1. W31F-E01
2. W31F-E04
3. W31F-E05
4. W31F-E07
5. W31F-E09
6. W31F-E14
7. W31F-E20
8. W31F-E24
9. W31F-E29
10. W31F-E32
