# Wave 30W — Research Methods

Namespace: **W30W**

## W30W-M01 — Hydrology Availability Clock
Store sensor observation, telemetry/public time, ingest time and provisional/final status.

## W30W-M02 — Station-to-Intake Mapping
Use verified intake/source mapping; nearest gauge is not automatically the facility source.

## W30W-M03 — Upstream/Downstream Logic
Account for reservoir releases, tributaries, withdrawals and travel time between gauge and intake.

## W30W-M04 — Water-Temperature Sensor QA
Detect sensor freeze, missingness and impossible jumps.

## W30W-M05 — NPDES Permit Versioning
Thermal/effluent permit limits change by permit/effective date.

## W30W-M06 — Permit-Limit Semantics
Temperature limits can be absolute, differential, seasonal, mixing-zone or conditional.

No generic national threshold.

## W30W-M07 — Cooling-System Taxonomy
Separate once-through, recirculating, dry/hybrid and other systems.

## W30W-M08 — Historical Water-Use Denominator
Use EIA/USGS reported/reanalyzed water use as structural exposure, not current withdrawal.

## W30W-M09 — Load Common-Cause Control
Hot weather raises power demand and water temperature simultaneously.

Control weather/load before claiming water causality.

## W30W-M10 — Facility Derate Validation
Validate against actual unit generation/outage/dispatch before market testing.

## W30W-M11 — Drought Weekly Vintage
Archive every U.S. Drought Monitor release/shapefile.

## W30W-M12 — Drought Context Only
USDM category is not an operational shutdown trigger unless a verified rule connects it to facility water availability.

## W30W-M13 — Curtailment Order Vintage
Archive every order/addendum/public status with issue/effective time.

## W30W-M14 — Right-Priority Entity Resolution
Map facility to water right/diversion only with legal/source evidence.

## W30W-M15 — Exceptions/Conditional Diversions
Curtailment orders may include health/safety, non-consumptive or other exceptions.

Model them explicitly.

## W30W-M16 — Groundwater Substitution
Surface-water curtailment may be offset by lawful groundwater or recycled water.

## W30W-M17 — Agricultural Growth-Stage Control
Irrigation shortfall impact depends on crop and phenological stage.

## W30W-M18 — Forecast Vintage
Archive every Reclamation/flow forecast vintage used in a decision.

## W30W-M19 — Constraint-vs-Outcome Separation
Water stress is exposure; derating/output loss is outcome.

## W30W-M20 — Physical Promotion Gate
Before financial alpha, require OOS prediction of:
water availability,
facility derate,
generation substitution,
crop/industrial output,
or physical inventory response.
