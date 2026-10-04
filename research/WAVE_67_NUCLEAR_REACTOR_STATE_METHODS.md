# Wave 67N — Research Methods

Namespace: **W67N**

## W67N-M01 — Daily Status Availability
NRC status data are daily snapshots; preserve report/public time and source collection window.

## W67N-M02 — Unevaluated Information
NRC status pages can label facility-provided information as unevaluated.
Treat operational fact separately from final causal finding.

## W67N-M03 — Percent-Power Semantics
Reported reactor power is a percentage state, not directly market MW.
Map carefully to unit capability.

## W67N-M04 — Unit Identity
Use NRC docket/unit identifiers; plant name alone can contain multiple units.

## W67N-M05 — Planned/Forced Classification
Parse reason/comments plus known outage calendars; do not classify every reduction as forced.

## W67N-M06 — Event-Time Ledger
Store event occurrence, licensee NRC-notification time, NRC public-report time and later revision time.

## W67N-M07 — Scram Retraction
NRC datasets can flag events later retracted/recategorized.
Do not erase original public state.

## W67N-M08 — Event-Code Taxonomy
Preserve exact 10 CFR reporting basis before grouping into broader causal families.

## W67N-M09 — Status-Report Sampling Lag
An event after the daily collection window may not appear until the next report.

## W67N-M10 — Restart Definition
One day of higher power is not sustained recovery.
Require persistence threshold.

## W67N-M11 — Refueling Baseline
Estimate planned duration by unit/season/history, not fleet-wide average only.

## W67N-M12 — Capacity Mapping
Use time-appropriate net summer/winter/nominal capability mapping.

## W67N-M13 — Regional Grid Mapping
Plant-to-ISO/RTO/BA mapping must be point-in-time and verified.

## W67N-M14 — Gas Substitution Counterfactual
Estimate marginal replacement dispatch from actual regional stack, not assume all lost nuclear becomes gas.

## W67N-M15 — Weather/Load Control
Heat/cold can simultaneously raise load and drive environmental derates.

## W67N-M16 — Transmission Control
A unit loss can matter differently under local transmission constraints.
Fuse W23T.

## W67N-M17 — ROP Lag Gate
Inspection/performance indicators are slower structural context, not intraday event feeds.

## W67N-M18 — Part 21 Scope
A Part 21 defect report is potential common-mode exposure; verify applicability to each unit.

## W67N-M19 — Aggregate-Outage Deduplication
If W24A already sees the MW outage, W67N must add unit cause/recovery information rather than double-count it.

## W67N-M20 — Physical Promotion Gate
Before financial alpha require OOS improvement in:
unit MW,
outage duration,
restart,
replacement generation,
reserve or regional gas/power flow.
