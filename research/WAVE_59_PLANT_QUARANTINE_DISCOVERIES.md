# Wave 59P — Plant Pest, Quarantine & Crop Capacity

Namespace: **W59P**

Thesis: plant pests and diseases can reduce productive acreage, destroy perennial biological capital, restrict movement of crops/nursery stock, and impair export access before conventional crop statistics fully reveal the damage. The edge is not "pest detected"; it is **quarantine footprint × host crop exposure × movement restriction × crop biology × substitute supply**.

All candidates are research hypotheses only. Claude owns later implementation.

## W59P-E01 — APHIS Quarantine Boundary Shock
Primary source: USDA APHIS plant-health quarantine maps/descriptions.

Track additions, expansions, contractions and removals of federal quarantine areas.

Priority: S

## W59P-E02 — Host-Crop Exposure
Intersect quarantine polygons with verified host-crop acreage/production geography.

Priority: S

## W59P-E03 — Quarantine Acreage Delta
Feature:
newly regulated host acreage
minus
released host acreage.

Priority: S-

## W59P-E04 — Movement-Restriction Severity
Normalize:
NO_RESTRICTION
TREATMENT_REQUIRED
CERTIFICATION_REQUIRED
PACKINGHOUSE_RESTRICTION
NO_MOVEMENT
DESTRUCTION/REMOVAL.

Priority: S

## W59P-E05 — Quarantine Supply Isolation
Estimate product that remains biologically produced but cannot move normally from origin to destination.

Priority: S

## W59P-E06 — Fruit-Fly Incursion State
Primary source:
APHIS exotic fruit-fly detections/quarantine maps.

State:
DETECTION
QUARANTINE_ESTABLISHED
EXPANSION
ERADICATION_TREATMENT
NO_NEW_DETECTIONS
QUARANTINE_LIFTED.

Priority: S

## W59P-E07 — Fruit-Fly Host Breadth
Different fruit flies affect different host sets.

Weight quarantine by crop-specific host exposure, not total agricultural acreage.

Priority: A+

## W59P-E08 — Eradication Clock
Estimate time from quarantine establishment to lifting using historical outbreaks and required biological trapping windows.

Priority: A+

## W59P-E09 — Citrus Greening Biological Capital Loss
HLB/citrus greening has no cure and infected trees ultimately die.

Model:
tree infection prevalence
-> yield deterioration
-> tree removal
-> replant
-> immature-tree lag.

Priority: S

## W59P-E10 — Citrus Productive-Tree Age Structure
Recovery depends on tree age and replacement maturation.

Build productive-capacity curve rather than acreage-only measure.

Priority: S-

## W59P-E11 — Citrus Disease Quarantine State
Track HLB, Asian citrus psyllid, citrus canker, black spot and sweet orange scab separately.

Priority: S-

## W59P-E12 — Citrus Movement-Rule Delta
APHIS federal orders define movement conditions for fruit, nursery stock, leaves, green waste and other regulated articles.

Feature:
restriction change by commodity/article.

Priority: A+

## W59P-E13 — NASS Citrus Forecast Revision
Primary source:
USDA NASS scheduled citrus forecasts.

Archive each vintage and decompose revisions by state/crop.

Priority: S

## W59P-E14 — Pest-vs-Forecast Reality Gap
Compare quarantine/disease expansion to subsequent NASS production revision.

Target:
future forecast error/revision, not direct futures return.

Priority: S

## W59P-E15 — Hurricane × Disease Interaction
For citrus:
storm damage can interact with chronic HLB weakness.

Fuse weather damage with disease/quarantine state.

Priority: A+

## W59P-E16 — Nursery-Stock Constraint
Restrictions on nursery stock can slow orchard/grove replacement and extend biological recovery.

Priority: A

## W59P-E17 — Export Phytosanitary Access State
Track destination-specific phytosanitary requirements/bans when public.

Priority: S-

## W59P-E18 — Export Diversion Pressure
If one market restricts an origin/product:
estimate displaced domestic supply and alternate-destination capacity.

Priority: A+

## W59P-E19 — Import Substitution Capacity
Domestic quarantine/crop loss can be offset by imports only if foreign supply and phytosanitary access exist.

Priority: A+

## W59P-E20 — Pest-Control Cost Shock
Treatment, trapping, certification, inspection and sanitation add cost even without lost output.

Priority: B+

## W59P-E21 — Quarantine Logistics Friction
Estimate added time/cost from treatment/certification/approved-facility requirements.

Priority: A

## W59P-E22 — Perennial vs Annual Crop Recovery
Perennial tree crops can have multi-year biological recovery; annual crops may recover next planting cycle.

Encode separately.

Priority: S methodology/edge hybrid

## W59P-E23 — Plant Disease Capacity-Loss Quotient
PDCLQ =
productive host capacity lost or immobilized
/
available substitute production + inventory + imports.

Priority: S

## W59P-E24 — Quarantine Lift Recovery
After legal quarantine ends, monitor whether actual shipments/production normalize immediately or lag.

Priority: A+

## W59P-E25 — Plant Pest Truth Ladder
DETECTION
-> QUARANTINE
-> MOVEMENT/TREATMENT RESTRICTION
-> BIOLOGICAL/LOGISTICS CAPACITY LOSS
-> PRODUCTION REVISION
-> TRADE SUBSTITUTION
-> PRICE/INVENTORY EFFECT
-> RECOVERY.

Priority: S architecture

## Highest-priority W59P tests

1. W59P-E01 Quarantine Boundary Shock
2. W59P-E02 Host-Crop Exposure
3. W59P-E04 Movement-Restriction Severity
4. W59P-E05 Quarantine Supply Isolation
5. W59P-E06 Fruit-Fly Incursion State
6. W59P-E09 Citrus Greening Biological Capital Loss
7. W59P-E13 NASS Citrus Forecast Revision
8. W59P-E14 Pest-vs-Forecast Reality Gap
9. W59P-E17 Export Phytosanitary Access State
10. W59P-E23 Plant Disease Capacity-Loss Quotient
