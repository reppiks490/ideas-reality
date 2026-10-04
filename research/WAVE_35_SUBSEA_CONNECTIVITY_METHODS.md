# Wave 35C — Research Methods

Namespace: **W35C**

## W35C-M01 — NORS Confidentiality Gate
FCC NORS filings are presumptively confidential.
Never claim direct public access or reconstruct confidential reports.

## W35C-M02 — Public Confirmation Standard
Create a confirmed cable fault only from operator/carrier/regulator notice or strong independent telemetry later corroborated by an authoritative source.

## W35C-M03 — Fault-Time vs Public-Time
Store physical estimated fault time separately from first-public confirmation.

## W35C-M04 — Logical vs Physical Restoration
Customer traffic restoration and cable physical repair are separate states.

## W35C-M05 — Capacity Uncertainty
Nominal/design, lit/activated and actually utilized capacity are distinct.

## W35C-M06 — Route Independence
Two cable systems are not fully independent if they share landing station, beach manhole, terrestrial backhaul or common shallow-water corridor.

## W35C-M07 — Structural Data Vintage
Cable owners, landing points and ready-for-service status change over time.

## W35C-M08 — BGP Confirmation Caveat
BGP changes can be caused by policy/maintenance unrelated to cable faults.

## W35C-M09 — Latency Baseline
Compare affected route with same-clock historical latency and unaffected control routes.

## W35C-M10 — Customer Impact Separation
Higher latency is not automatically economic loss.

## W35C-M11 — Operator ETR Vintage
Archive every repair estimate; never overwrite earlier public estimates.

## W35C-M12 — Repair Vessel Identity
Require authoritative operator/maritime notice or independently verified vessel identity before using vessel ETA.

## W35C-M13 — Vessel Position Rights
AIS/vendor licensing varies. Do not assume proprietary vessel tracking is freely redistributable.

## W35C-M14 — Maritime Notice Semantics
Cable-laying/repair navigational warnings indicate operations in an area; they do not by themselves prove the exact fault cause or completion.

## W35C-M15 — Permit State
Preserve regulator/permit jurisdiction and public evidence separately from vessel readiness.

## W35C-M16 — Weather Window
Use marine-operability data from W24M for repair hazard, not generic city weather.

## W35C-M17 — Multi-Fault Parent Event
Correlated cable failures from one geological/anchor event must not be counted as independent evidence.

## W35C-M18 — Geography Confidence
Exact cable routes can be proprietary/approximate. Maintain confidence and avoid false precision.

## W35C-M19 — Repair Outcome
Physical repair requires operator/authoritative confirmation or clear telemetry plus subsequent confirmation.

## W35C-M20 — Operational Promotion Gate
Before financial alpha require OOS prediction of:
routing/latency degradation,
spare-capacity stress,
repair duration,
second-fault vulnerability,
or customer-service impairment.
