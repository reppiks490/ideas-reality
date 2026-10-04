# Wave 37O — Research Methods

Namespace: **W37O**

## W37O-M01 — EDGAR Acceptance Clock
Use SEC EDGAR acceptance/public time, not later aggregator timestamp.

## W37O-M02 — Transaction-vs-Filing Time
Execution date and public filing date are separate.

## W37O-M03 — Form 4 Row Semantics
Parse each row's transaction code, acquired/disposed flag, price, ownership form and referenced footnotes.

## W37O-M04 — Document-Level 10b5-1 Flag Caveat
A checked plan box does not automatically apply to every transaction row.
Follow footnote references.

## W37O-M05 — Adoption-Date Provenance
Use disclosed plan adoption date from Form 4 footnote or Item 408(a), not inferred date.

## W37O-M06 — Item 408 Quarterly Lag
Plan adoption/termination disclosure can arrive only in the next applicable 10-Q/10-K.
Do not make it visible earlier.

## W37O-M07 — Cooling-Off Rule Version
Apply current Rule 10b5-1 timing and historical rule version by date/person type.

## W37O-M08 — No Motive Inference
A trade's economic direction does not establish personal motive or possession of information.

## W37O-M09 — Compensation Neutralization
Exercise, vesting and tax-withholding transactions need separate treatment from open-market purchases/sales.

## W37O-M10 — Indirect-Ownership Deduplication
Avoid double counting the same economic shares across reporting person, trust, LLC or group.

## W37O-M11 — Holding Fraction Denominator
Use pre-event holdings on comparable direct/indirect basis.

## W37O-M12 — Form 144 Is Intent
Form 144 is a notice of proposed Rule 144 sale; it is not evidence that sale occurred.

## W37O-M13 — Form 144 Threshold
Affiliate Form 144 filing threshold is proposed sales exceeding 5,000 shares or $50,000 in a three-month period under current Rule 144 conditions.

## W37O-M14 — Rule 144 Capacity
Apply current holding/volume/manner/current-information conditions when estimating potential sale capacity.

## W37O-M15 — 13D Public Clock
Current initial Schedule 13D deadline is five business days after the triggering acquisition; material amendments are due within two business days.

## W37O-M16 — 13G Category Clock
Qualified institutional, exempt and passive investors follow different initial/amendment timing.
Encode category explicitly.

## W37O-M17 — Ownership Percentage Denominator
Use point-in-time shares outstanding and correct beneficial-ownership rules.

## W37O-M18 — Group Status
13D/G group formation and shared voting/investment power require filing-specific interpretation; do not merge entities merely because they appear together.

## W37O-M19 — HFIA Coverage Break
March 18, 2026 expands Section 16 coverage to directors/officers of covered foreign private issuers; historical comparisons must account for the regime break.

## W37O-M20 — Intermediate Promotion Gate
Before financial alpha require OOS prediction/reconstruction of:
executed ownership flow,
holding change,
plan execution,
large-owner accumulation/distribution,
or free-float/liquidity change.
