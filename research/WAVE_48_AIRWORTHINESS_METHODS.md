# Wave 48A — Research Methods

Namespace: **W48A**

## W48A-M01 — SDR Availability Clock
Store difficulty date, submission/approval/public date where available, and first ingest.

Recently submitted SDRs are not public until FAA approval.

## W48A-M02 — SDR Reporting Bias
SDR coverage differs by operator/regulatory reporting obligation.

Do not treat report counts as incident incidence without exposure normalization.

## W48A-M03 — Installed-Base Denominator
Normalize component/model report counts by estimated installed fleet.

## W48A-M04 — Independent-Operator Count
Weight repeated defects across distinct operators more heavily than duplicate narratives.

## W48A-M05 — Narrative Deduplication
Detect amended/duplicate reports and common-event submissions.

## W48A-M06 — Advisory vs Mandatory
SAIBs are non-regulatory/non-mandatory; ADs are mandatory.

Never merge them.

## W48A-M07 — Actual Notice vs Universal Effect
Emergency AD actual notice can precede Federal Register universal effectiveness.

Model both clocks explicitly.

## W48A-M08 — AD Applicability Parser
Extract make/model/serial/component/configuration exclusions and exceptions.

## W48A-M09 — Compliance-Time Parser
Normalize:
flight hours,
cycles,
calendar days,
before further flight,
before next flight after condition,
repetitive intervals.

## W48A-M10 — Optional vs Required Actions
Service bulletins can contain optional/non-required work even when incorporated by reference.

Parse AD-required actions only.

## W48A-M11 — AMOC State
Alternative Method of Compliance can change operator burden, but may be operator-specific and not broadly public.

Do not infer universal relief.

## W48A-M12 — Supersedure Versioning
An AD no longer applies once superseded according to FAA semantics; preserve historical state.

## W48A-M13 — Tail Applicability Confidence
Registry make/model match alone may be insufficient where part/configuration matters.

Use UNKNOWN rather than false precision.

## W48A-M14 — Fleet Registry Point-in-Time
Registration records change over time; archive daily/periodic vintages for historical fleet estimates.

## W48A-M15 — Operator Fleet Resolution
Map registered owner, operator and lessor separately.

## W48A-M16 — Maintenance Capacity Evidence
Use documented labor/task times, part availability and MRO capability where public.

## W48A-M17 — Schedule Outcome Validation
Validate predicted capacity loss against actual cancellations, gauge changes, utilization or cargo schedule where lawful data are available.

## W48A-M18 — Regulator Common-Cause Control
FAA/EASA actions may respond to the same underlying event. Do not count as independent defects.

## W48A-M19 — Media vs Regulatory Clock
Press reports/manufacturer statements preceding official ADs remain separate information events.

## W48A-M20 — Physical Promotion Gate
Before financial alpha, require OOS improvement in:
regulatory action,
tail applicability,
grounded/inspection burden,
fleet availability,
cancellations,
or return-to-service.
