# Wave 18G — Research Methods

Namespace: **W18G**

## W18G-M01 — Earthquake Product Version Ledger
Store every USGS event/product version:
event origin
product creation/update
first seen
source network
review status
content hash.

## W18G-M02 — ShakeMap Point-in-Time Sampling
Sample only the ShakeMap version public at the decision timestamp.

Later station/source refinements remain unavailable until their product update time.

## W18G-M03 — Facility Coordinate Confidence
Maintain canonical asset coordinates/polygons, effective dates and source confidence.

A geospatial miss of a few kilometers can materially change shaking exposure.

## W18G-M04 — Magnitude/Distance Negative Control
Always compare facility-intensity models to simple magnitude/depth/distance baselines.

Promote only if ShakeMap adds OOS value.

## W18G-M05 — Shaking Uncertainty Preservation
Retain ShakeMap uncertainty rather than reducing hazard to a single deterministic intensity.

## W18G-M06 — PAGER Vintage Discipline
PAGER alert/loss estimates are versioned and can change as shaking/source information improves.

Never train initial-event models with later PAGER versions.

## W18G-M07 — Aftershock Forecast Vintage Ledger
USGS OAF begins soon after qualifying events and updates on a defined schedule.

Store each forecast's release time, model type, parameters and horizon probabilities.

## W18G-M08 — Aftershock Conditional Recovery
Aftershock risk matters only in the context of existing exposure/damage/restart state.

Avoid generic earthquake-aftershock market features.

## W18G-M09 — Tsunami CAP/ATOM Versioning
Archive every Warning Center message with:
issue time
alert level
zones
forecast ETA/height
observations
cancellation/update lineage.

## W18G-M10 — Forecast-vs-Observed Tsunami Separation
Do not overwrite early forecast height with later gauge observations.

They are separate information events.

## W18G-M11 — Coastal Elevation/Exposure Gate
A coastal alert zone is not equivalent to facility inundation.

Use elevation, distance to water and local hazard mapping where defensible.

## W18G-M12 — Volcanic Ash 3D Intersection
Ash hazard requires horizontal plume geometry AND altitude/flight level.

A 2D route crossing alone is insufficient.

## W18G-M13 — Ash Advisory Versioning
Archive advisory number, observation time, forecast periods, next advisory and "no further advisories" transitions.

## W18G-M14 — SWPC Forecast/Observed Separation
WATCH, WARNING and ALERT are different states.

Do not backfill an observed G-level into the earlier forecast window.

## W18G-M15 — Solar-Wind Propagation Clock
Store spacecraft observation time, public availability, propagated-Earth time and geospace-response time separately.

## W18G-M16 — Southward-Bz Duration
Use sign/duration/integrated southward IMF measures, not only total field magnitude.

## W18G-M17 — Geomagnetic Spatial Vulnerability
Global Kp/G-scale is a driver; infrastructure exposure is spatially heterogeneous.

Condition on geomagnetic latitude/geology/grid topology.

## W18G-M18 — Mitigation-Action Confounding
Grid/airline operators can reduce damage by acting on forecasts.

Observed low disruption may reflect successful mitigation rather than weak hazard.

## W18G-M19 — Rare-Event Research Design
Use event studies, matched controls and physical intermediate targets before flexible ML.

## W18G-M20 — Physical Intermediate Promotion Gate
Require OOS prediction of:
facility shutdown,
grid mitigation,
port/airport restriction,
communications degradation,
or substitute-flow change
before financial-return promotion.
