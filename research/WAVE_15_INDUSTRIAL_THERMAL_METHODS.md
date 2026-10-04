# Wave 15X — Research Methods

Namespace: **W15X**

## W15X-M01 — Four-Clock Incident Ledger
Store:
physical event time
reporting deadline
public source time
first ingest time.

Never use final-report timestamps as if known at event onset.

## W15X-M02 — Initial-vs-Final Report Versioning
TCEQ and similar sources can revise quantities/causes/duration.

Archive every public version.

## W15X-M03 — Planned/Unplanned Hard Split
Maintenance/startup/shutdown and unplanned process upset are different populations.

Model separately before any pooling.

## W15X-M04 — Unit Ontology
Map free-text narratives and emission-point names to a versioned unit taxonomy with confidence.

No forced classification when ambiguous.

## W15X-M05 — Throughput Relevance Gate
A reportable emissions event is not automatically a production outage.

Require evidence tying the event to a throughput/yield unit or later physical output.

## W15X-M06 — Jurisdiction Threshold Normalization
TCEQ and AQMD reportability thresholds differ.

Model source-specific selection effects explicitly.

## W15X-M07 — Satellite Observation Mask
FIRMS is not continuous.

Store:
sensor
overpass time
latency class URT/RT/NRT/SP
cloud/quality context where available
missing-data status.

## W15X-M08 — Facility Geofence Discipline
Use vetted facility polygons/flare-stack coordinates.

Avoid attributing nearby wildfire/industrial sources to the wrong plant.

## W15X-M09 — Persistent Hotspot Baseline
Estimate facility/sensor/day-night normal thermal pattern before flagging anomalies.

## W15X-M10 — Multi-Sensor Confirmation
Where practical require confirmation across NOAA-20/21/S-NPP or consecutive overpasses for disappearance-style signals.

## W15X-M11 — Fire/Flare Disambiguation
Use persistence, facility context, temperature/radiative characteristics and wildfire layers.

Do not assume every FIRMS hotspot at an industrial site is a flare.

## W15X-M12 — Storm Common-Cause Control
BSEE shut-ins, refinery disruptions, port closures and pipeline outages may share the same storm.

Do not count them as independent evidence without causal decomposition.

## W15X-M13 — Peak-vs-Recovery Separation
For storm/industrial outages estimate both:
peak lost capacity
and restoration trajectory.

## W15X-M14 — Expected Restoration Curve
Build comparable-event restart baselines by facility/unit/storm severity.

Research the residual recovery delay.

## W15X-M15 — Production Consequence Validation
Validate incident states against:
EIA refinery utilization/product inventories
pipeline nominations/flows
company disclosures
port flows
regional basis/spreads.

## W15X-M16 — Public-Availability Rights Gate
Separate:
public real time
public near real time
public delayed
government-only real time
retrospective public.

## W15X-M17 — Negative-Latency Gate
EPA CAMPD quarterly and OSHA six-month-lag data are forbidden as live triggers.

They may enter only historical feature/label pipelines at their actual publication times.

## W15X-M18 — Duplicate Incident Reconciliation
One physical event can appear in TCEQ, FENS, NRC, company news and satellite data.

Create a parent incident ID and preserve all source children.

## W15X-M19 — Narrative Leakage Control
Later root-cause/final-report text cannot train a model using features unavailable at initial alert time.

## W15X-M20 — Intermediate Outcome Promotion Gate
Promote only after showing OOS prediction of a physical intermediate:
unit outage,
throughput loss,
restart duration,
product balance,
or substitute flow.
