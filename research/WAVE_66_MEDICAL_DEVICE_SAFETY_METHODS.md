# Wave 66D — Research Methods

Namespace: **W66D**

## W66D-M01 — Adverse-Event Availability Clock
Store event date, manufacturer-awareness date only if public, FDA receipt and public-data availability separately.

## W66D-M02 — MDR Is Not Causality
MAUDE reports do not prove a device caused the event.

## W66D-M03 — Reporting Bias
Report volume changes with publicity, litigation, reporting practices and installed base.

## W66D-M04 — Installed-Base Denominator
Normalize counts where a defensible population estimate exists.

## W66D-M05 — Monthly/Weekly Feed Semantics
FDA MAUDE downloadable files are monthly; openFDA device-event API can update more frequently.
Use actual source vintage.

## W66D-M06 — Five-Day Reporting Meaning
Five-day category indicates special regulatory reporting circumstances, not necessarily confirmed defect causality.

## W66D-M07 — Supplemental Linking
Link follow-up MDRs to initial reports without double-counting events.

## W66D-M08 — Product-Code Drift
FDA product codes/regulatory classification can change; version mappings.

## W66D-M09 — Recall Initiation vs Posting
Firm action may precede FDA classification/posting.

## W66D-M10 — Recall Lifecycle
Correction/removal initiation, classification, update and termination are separate states.

## W66D-M11 — Unit Count Revision
Recall population can expand or contract.

## W66D-M12 — Implanted Population Uncertainty
Sales history is not identical to active implanted base; use survival/replacement assumptions.

## W66D-M13 — Remedy Clinical Burden
Explant/revision surgery is economically and clinically different from software update.

## W66D-M14 — Shortage List Semantics
FDA explicitly notes list presence does not necessarily mean patient care is affected.

## W66D-M15 — Shortage Vintage
Archive initial, reverified, duration-extension and removal dates.

## W66D-M16 — Discontinuance != Shortage
A discontinued SKU may have substitutes and no active shortage.

## W66D-M17 — Substitute Compatibility
Do not count nominal alternatives that require incompatible hardware, training or workflow.

## W66D-M18 — Company Attribution
Map recalls/events to legal manufacturer and public parent with provenance.

## W66D-M19 — Common-Cause Deduplication
One defect can generate many MDRs, recalls and safety communications.

## W66D-M20 — Clinical Promotion Gate
Before financial alpha require OOS improvement in:
safety escalation,
recall,
remedy burden,
shortage,
procedure capacity,
or recovery.
