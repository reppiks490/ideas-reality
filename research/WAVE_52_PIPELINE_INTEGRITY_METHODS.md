# Wave 52P — Research Methods

Namespace: **W52P**

## W52P-M01 — Order-Service Clock
Store issue date, service/effective time, first public-web time and ingest time separately.

## W52P-M02 — Enforcement-Page Lag
PHMSA enforcement web data can update after the underlying order.

Backtests use observed public availability, not inferred issue availability.

## W52P-M03 — Order-Version Archive
Archive original CAO, every amendment, operator response and closure document.

## W52P-M04 — Segment Definition Parser
Extract exact affected/isolated segment endpoints, mileage, diameter and system name.

## W52P-M05 — Shutdown vs Restriction
A segment shutdown and a pressure restriction are different capacity states.

## W52P-M06 — Hydraulic Translation
Pressure-to-flow mapping must use pipeline physics/configuration.

No linear shortcut without validation.

## W52P-M07 — Station Set-Point State
Where public, preserve pump/compressor/regulator set-points and ordered changes.

## W52P-M08 — Restart Approval vs Actual Restart
Regulatory approval is not proof that commercial operations resumed at that moment.

## W52P-M09 — Pressure Restoration Gate
Do not restore full modeled capacity until written approval and/or actual flow supports it.

## W52P-M10 — Root-Cause Vintage
Preliminary cause, final RCFA and regulator-accepted findings are distinct states.

## W52P-M11 — ILI Data Availability
Inspection results may be private. Use only public order/report summaries unless lawful data access exists.

## W52P-M12 — Incident-Report Lag
30-day reports are delayed validation, not event-time data.

## W52P-M13 — Enforcement Case Taxonomy
Keep CAO, Safety Order, Consent Order, NOPV, Compliance Order and Warning Letter separate.

## W52P-M14 — Operator Entity Resolution
Map operating subsidiary, parent, pipeline system and FERC/operator identities with provenance.

## W52P-M15 — NPMS Access Boundary
Public NPMS geography is intentionally restricted in precision and excludes distribution/gathering systems.

Respect access policy.

## W52P-M16 — Annual Mileage Availability
PHMSA annual mileage/facility data are structural denominators, not live capacity telemetry.

## W52P-M17 — Flow Validation
Validate capacity impact using nominations, tariffs, maintenance notices, pipeline flows or downstream receipts where lawful/public.

## W52P-M18 — Alternate-Capacity Proof
Rail/truck/barge/other-pipeline capacity counts only if geography, product compatibility and spare capacity support it.

## W52P-M19 — Common-Incident Deduplication
NRC notice, operator press release, PHMSA case and 30-day report may describe one event.

Parent them under one incident.

## W52P-M20 — Physical Promotion Gate
Before return testing require OOS improvement in:
capacity restriction,
restart timing,
actual flow,
reroute,
inventory,
or regional basis.
