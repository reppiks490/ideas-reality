# Wave 36P — Research Methods

Namespace: **W36P**

## W36P-M01 — Daily Shortage Vintage
FDA says the shortage list is updated daily.
Archive every observed public vintage rather than querying only current state.

## W36P-M02 — Initial Posting vs Change Date
Preserve initial_posting_date, update/change dates and first-ingest separately.

## W36P-M03 — Manufacturer Availability Semantics
FDA notes presentation availability reflects manufacturer-supplied current information; it is not itself FDA's determination that the overall shortage is resolved.

## W36P-M04 — National vs Local Shortage
FDA shortage status is national.
Do not treat a local pharmacy/hospital stockout as national shortage without FDA confirmation.

## W36P-M05 — NDC / Presentation Identity
Strength, dosage form, package and manufacturer are separate supply units.

## W36P-M06 — Manufacturer Entity Resolution
Applicant, labeler, manufacturer and physical manufacturing facility may differ.
Map separately.

## W36P-M07 — Recall Public-Time Ledger
Store company announcement/recall initiation, FDA classification/report/publication dates separately.

## W36P-M08 — Recall Scope Uncertainty
Do not infer national supply share from lot count without denominator.

## W36P-M09 — Inspection Classification Lag
FDA final inspection classification can be sent/post after inspection close, commonly on a 45–90 day horizon depending on inspection type.
Use public classification time.

## W36P-M10 — Inspection Database Coverage
FDA says the classification database is not comprehensive and excludes specified inspection categories.
Absence is not a clean bill of health.

## W36P-M11 — OAI Semantics
OAI means official action is indicated/recommended; it does not automatically mean facility shutdown.

## W36P-M12 — Form 483 Semantics
A Form 483 is inspectional observation, not a final agency determination.

## W36P-M13 — 483 Publish-Date Mask
Only use 483 content when the record became publicly posted/available.

## W36P-M14 — Warning Letter Separation
Warning letter issue/public date and later closeout/corrective status are separate events.

## W36P-M15 — Import Alert Versioning
Archive current public red/green/exception lists and effective changes by firm/product/country.

## W36P-M16 — Product-Facility Provenance
Do not attribute a product shortage to a facility merely because that firm has an FDA action.

## W36P-M17 — Therapeutic Equivalence Gate
Substitution must respect dosage form, indication, route, regulatory status and clinical constraints.

## W36P-M18 — Hidden Notification Boundary
Manufacturers provide FDA non-public shortage-prevention information.
Do not infer or backtest from information not public at the time.

## W36P-M19 — Demand Common-Cause Control
Demand surges can cause both shortage and higher manufacturer sales.
Separate demand-driven from supply-driven shortage.

## W36P-M20 — Physical Promotion Gate
Before market alpha require OOS prediction of:
shortage entry/resolution,
presentation availability,
substitution,
supply restoration,
or procurement/volume effect.
