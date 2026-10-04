# Wave 24M — Research Methods

Namespace: **W24M**

## W24M-M01 — Marine Observation Availability Ledger
Store observation time, source-post time, first-ingest time, quality flag and later verification status.

## W24M-M02 — Preliminary-vs-Verified Water Level
NOAA real-time water levels can be preliminary; later verified values must not overwrite point-in-time history in a backtest.

## W24M-M03 — Datum Discipline
Water-level calculations must use the correct vertical datum for the route/channel. Never mix MLLW, NAVD88, LWD or chart datum silently.

## W24M-M04 — Route-Specific Bathymetry
Under-keel clearance requires the controlling route/channel depth, not station water level alone.

## W24M-M05 — Vessel Geometry Contract
Preserve vessel draft, air draft, beam, length and class separately.

No generic "large vessel" proxy where exact restrictions differ by dimension.

## W24M-M06 — Squat/Safety Allowance Model
Dynamic squat and safety margins depend on vessel speed, channel geometry and rules.

Use explicit rule/model provenance.

## W24M-M07 — Observation-vs-Prediction Separation
Tag PORTS observations, tide/current predictions and OFS model guidance separately.

## W24M-M08 — OFS Forecast Vintage Archive
Archive every model cycle and forecast horizon used.

Never use a later cycle to score an earlier decision.

## W24M-M09 — Sensor Missingness Gate
Sensor outage is not calm water, zero current or unlimited air gap.

## W24M-M10 — NDBC Time Semantics
Preserve actual observation/acquisition time; NDBC notes wave acquisition/display times can differ from standard meteorological timestamps.

## W24M-M11 — Port-Rule Versioning
Pilotage, draft, current and closure rules can change over time.

Backtests use the rule effective on the historical date.

## W24M-M12 — COTP Public-Time Contract
Use the first public USCG/Homeport/MSIB time available to the strategy.

Do not backdate to internal decision time.

## W24M-M13 — Formal Restriction != Physical Condition
Model weather/hydrodynamics and legal restriction as separate layers.

## W24M-M14 — Vessel-Class Eligibility Matrix
For every state determine which vessel classes remain operable.

Effective capacity is weighted by actual cargo mix.

## W24M-M15 — Queue Observation Lag
AIS/anchorage queue growth can occur after navigability deteriorates.

Measure lag explicitly.

## W24M-M16 — Reopening-vs-Backlog Separation
Formal reopening, first vessel movement and backlog clearance are distinct events.

## W24M-M17 — Draft-to-Tonnage Translation
Estimate cargo loss using vessel-specific hydrostatic/loading relationships where available; otherwise retain uncertainty bands.

## W24M-M18 — Port Diversion Feasibility
An alternate port counts as substitute capacity only if berth, depth, handling equipment and inland connections support the cargo/vessel.

## W24M-M19 — Common-Storm Control
Multiple ports can degrade under the same storm. Do not count correlated port shocks as independent evidence.

## W24M-M20 — Intermediate Promotion Gate
Before financial testing require improvement in prediction of:
transit eligibility,
queue growth,
throughput,
vessel delay,
cargo tonnage,
or diversion.
