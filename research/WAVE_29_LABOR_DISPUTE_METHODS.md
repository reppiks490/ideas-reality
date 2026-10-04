# Wave 29L — Research Methods

Namespace: **W29L**

## W29L-M01 — Legal-State Clock
Store each procedural event with first-public time, effective time and next legally relevant deadline.

## W29L-M02 — FMCS Batch Availability
Monthly F-7 public files are not real-time filings.

Backtests use the monthly public-posting date unless a faster lawful public source is proven.

## W29L-M03 — F-7 Coverage Boundary
An F-7 notice indicates upcoming covered bargaining/dispute notification, not an inevitable strike.

## W29L-M04 — Contract-Date Versioning
Collective-bargaining dates can be extended or superseded.

Archive every public revision.

## W29L-M05 — Employer Entity Resolution
Facility/employer legal entity may differ from listed parent.

Map with provenance/confidence.

## W29L-M06 — Union/Bargaining Unit Identity
Keep local, international union and bargaining unit distinct.

## W29L-M07 — NLRB Allegation Status
A filed charge is an allegation, not a finding.

Encode:
FILED
INVESTIGATING
DISMISSED
SETTLED
COMPLAINT
DECISION where available.

## W29L-M08 — NLRB Availability
NLRB reports new case information is generally posted within a day; use observed public timestamp/date.

## W29L-M09 — RLA vs NLRA Split
Airline/rail labor under Railway Labor Act follows different procedures than ordinary NLRA-covered industries.

Never apply NMB clocks to non-RLA disputes.

## W29L-M10 — Self-Help Deadline Recalculation
PEB creation, settlement or other legal action can move/remove the self-help date.

## W29L-M11 — PEB Versioning
Store creation order, report date and subsequent cooling-off deadline as separate public events.

## W29L-M12 — Worker Count vs Capacity
Affected worker count is not lost output.

Map roles, shifts, automation, cross-training and facility criticality.

## W29L-M13 — Contingency Capacity
Estimate management/contractor/substitute-carrier capacity with uncertainty, not zero.

## W29L-M14 — Inventory Buffer
Production strike effect depends on days of finished/raw inventory.

## W29L-M15 — Stoppage Start Verification
Strike authorization/vote/threat is not actual stoppage.

Require operational/public confirmation.

## W29L-M16 — BLS Lag Gate
BLS WSP is monthly retrospective validation; never use a later BLS record at the historical stoppage onset.

## W29L-M17 — Agreement vs Operational Recovery
Tentative settlement date, ratification, return-to-work and backlog clearance are separate.

## W29L-M18 — Common-Macro Control
Labor disputes may coincide with industry downturns/inflation cycles.

Control common economic factors before return claims.

## W29L-M19 — Event-Study Selection Control
Do not select only famous strikes. Build the full public-event universe to avoid survivorship.

## W29L-M20 — Physical Promotion Gate
Before market alpha, require OOS prediction of:
actual stoppage,
capacity loss,
shipment/service disruption,
duration,
or recovery.
