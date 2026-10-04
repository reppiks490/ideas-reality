# Wave 34D — Research Methods

Namespace: **W34D**

## W34D-M01 — First-Public Clock
Store provider-stated incident start separately from first time the incident was public.

## W34D-M02 — Provider Revision Ledger
Archive every status-page update and later PIR correction.
Never rewrite the historical public state.

## W34D-M03 — Incident Parent Deduplication
One incident affecting many services is one parent event with multiple service impacts.

## W34D-M04 — Reporting-Threshold Bias
Providers differ materially in which incidents they publish.
Do not compare raw incident counts without provider-specific reporting controls.

## W34D-M05 — Public vs Account-Specific
AWS/Azure/Google public status does not expose all account-specific impact.
Absence from public status is not evidence of no customer issue.

## W34D-M06 — Severity Normalization
Provider severity labels are not directly comparable.
Create an internal severity ontology from observed functional impact.

## W34D-M07 — Region Weighting
Affected region size/customer importance must be estimated separately from incident count.

## W34D-M08 — Control-vs-Serving Plane
Deployment/control-plane failure cannot be assumed to stop existing serving workloads.

## W34D-M09 — BGP Is Not Outage
Route withdrawal/peer-state change is evidence of routing change, not proof of user-visible service failure.

## W34D-M10 — IODA Diurnal Control
Active-probing/telescope signals have normal diurnal patterns.
Compare against historical same-clock baselines.

## W34D-M11 — Cloudflare Verification State
Preserve algorithmic anomaly vs manually/externally corroborated outage.

## W34D-M12 — Independent Confirmation
Require at least one independent operational source before labeling provider self-report as externally confirmed.

## W34D-M13 — Dependency Provenance
Customer-provider dependency must be sourced from filings, architecture docs, case studies or other authoritative evidence.

## W34D-M14 — Dependency Versioning
Cloud vendors/regions and architecture change over time.

## W34D-M15 — Business-Hours Localization
Convert outage interval to customer-local operating hours and known transaction cycles.

## W34D-M16 — Multi-Cloud Failover Reality
Marketing claims of multi-cloud do not prove automatic failover.
Require evidence of actual architecture/operational substitution.

## W34D-M17 — Cyber Attribution Gate
Do not classify an outage as malicious without authoritative attribution.

## W34D-M18 — Customer Outcome Validation
Require customer-visible service/transaction impact before claiming business-capacity loss.

## W34D-M19 — Provider vs Customer Equity Separation
Provider stock effect and customer stock effect are separate targets with separate mechanisms.

## W34D-M20 — Operational Promotion Gate
Before financial alpha require OOS prediction of:
incident expansion,
customer impairment,
recovery duration,
transaction outage,
or independently measured traffic/routing degradation.
