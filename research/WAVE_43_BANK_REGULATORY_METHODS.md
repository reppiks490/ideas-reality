# Wave 43B — Research Methods

Namespace: **W43B**

## W43B-M01 — Institution Identity
Map regulator charter/entity IDs, FDIC certificate, RSSD, OCC charter and public parent ticker separately.

## W43B-M02 — Action Effective vs Public Time
Backtests use first public availability, not confidential exam/order negotiation date.

## W43B-M03 — Order Text Parsing
Extract only explicit constraints/deadlines from the signed public order.

## W43B-M04 — Amendment/Termination Versioning
Orders remain active until publicly modified/terminated/suspended/set aside under their terms.

## W43B-M05 — Capital Rule Versioning
PCA thresholds and capital frameworks vary by rule/election/regime.

## W43B-M06 — Ratio Classification Caveat
Numerical capital ratios do not prove legal "well capitalized" status if specific orders/actions impose capital maintenance conditions.

## W43B-M07 — CBLR Handling
Banks using Community Bank Leverage Ratio framework require separate rule logic and grace-period treatment.

## W43B-M08 — Call Report Vintage
Quarterly Call Reports become public after filing; never expose quarter-end values before public availability.

## W43B-M09 — Order-Specific Minimum
Use explicit order requirement if above general threshold.

## W43B-M10 — Brokered Deposit Rule State
Version Section 29 / 12 CFR 337.6 and any applicable waivers/exceptions.

## W43B-M11 — Unknown Waiver Discipline
Absence of public waiver evidence is UNKNOWN, not automatically restricted/unrestricted.

## W43B-M12 — Consolidated vs Bank-Level Capital
Holding company and insured depository subsidiary have different regulatory measures/actions.

## W43B-M13 — Constraint-to-Economics Mapping
An asset cap or branch restriction is legal capacity; actual lost growth must be validated against demand/plans.

## W43B-M14 — Multiple-Action Deduplication
Link overlapping OCC/FDIC/Fed/state actions by root deficiency where possible.

## W43B-M15 — Termination Is Not Exoneration
Termination only proves regulator ended that action; it does not prove normalized earnings/asset quality.

## W43B-M16 — Survivorship Control
Include terminated, merged and failed institutions when building historical samples.

## W43B-M17 — Public-Only Supervisory Boundary
CAMELS ratings and many supervisory communications are confidential.

Do not infer or fabricate them.

## W43B-M18 — Physical Promotion Gate
Before equity/credit testing require OOS improvement in:
deposit/funding change,
asset/loan growth,
capital distribution,
capital headroom,
or order termination.
