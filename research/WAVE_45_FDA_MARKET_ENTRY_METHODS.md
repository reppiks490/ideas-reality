# Wave 45F — Research Methods

Namespace: **W45F**

## W45F-M01 — Application Identity
Use NDA/BLA/ANDA application and submission numbers as primary regulatory keys; map sponsor/product/ticker separately.

## W45F-M02 — Sponsor-Disclosed Goal-Date Provenance
A sponsor-stated PDUFA date is public evidence but not an FDA-hosted universal calendar.

Store source and publication time.

## W45F-M03 — Review-Class Rule Versioning
Standard/priority, NME/non-NME, original/resubmission and supplement classes have different clock rules.

## W45F-M04 — Goal-Date Revision Ledger
Never overwrite old dates. Archive each public revision/extension.

## W45F-M05 — Advisory Question Semantics
Parse exact committee question and denominator.

A favorable vote on one question is not full-product approval.

## W45F-M06 — Briefing-Material Public Clock
Use first public FDA committee-material availability, not document creation date.

## W45F-M07 — Outcome Public Clock
Store FDA action date, FDA public-posting time and sponsor announcement time separately where observable.

## W45F-M08 — CRL Transparency Vintage
FDA's public CRL database is a newer transparency source and can contain delayed/archive additions.

Do not expose a CRL before its actual historical public availability.

## W45F-M09 — Deficiency Extraction Confidence
Distinguish explicit FDA text from sponsor paraphrase.

## W45F-M10 — Label Diff
Compare proposed/base-case and approved label only with sourced pre-decision expectations.

## W45F-M11 — Approval != Launch
Commercial launch requires independent observation.

## W45F-M12 — Orange Book Vintage
Patent/exclusivity data must be point-in-time; current listings cannot reconstruct historical visibility by themselves.

## W45F-M13 — Tentative Approval Boundary
Tentative approval demonstrates substantive ANDA review completion but not final market authorization.

## W45F-M14 — 180-Day Exclusivity Uncertainty
First-applicant eligibility/forfeiture/trigger rules are complex.

Use FDA/legal public evidence, not heuristic inference.

## W45F-M15 — Biosimilar Interchangeability Separation
Biosimilar licensure and interchangeability are distinct regulatory states.

## W45F-M16 — Manufacturing Dependency
Cross-link W36P facility/shortage data rather than duplicating it.

## W45F-M17 — Binary-Event Selection Bias
Include all qualifying public decisions, not only high-volatility biotech names.

## W45F-M18 — Promotion Gate
Before financial alpha require OOS improvement in:
approval/CRL probability,
label scope,
launch delay,
generic/biosimilar entry,
or commercial availability.
