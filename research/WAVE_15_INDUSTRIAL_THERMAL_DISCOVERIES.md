# Wave 15X — Industrial Upset & Thermal Telemetry

Namespace: **W15X**

Thesis: industrial capacity often changes before production statistics catch up. The fastest lawful public evidence can come from mandatory upset/flare notifications, satellite thermal anomalies, and operational shut-in reports. This wave separates live operational sources from slower datasets that are useful only for validation.

All candidates are research hypotheses only. Claude owns any later implementation.

## W15X-E01 — TCEQ Refinery/Petrochemical Upset Pulse

Primary source:
Texas Commission on Environmental Quality Air Emission Event Report database / STEERS.

Texas requires initial notification within 24 hours of discovery for reportable emissions events. Public records expose owner/operator, regulated entity, event type, event start/end, initial notification time, compounds/quantities, emission points and event narrative.

Research:
unexpected upset
× facility throughput importance
× unit role
× event duration
× restart/recovery evidence.

Priority: S

## W15X-E02 — TCEQ Unit-Type Severity Map

Parse event narratives/emission points into operational classes:
FCCU
hydrotreater
sulfur recovery
coker
compressor
boiler
hydrogen
flare
power interruption
other.

Question:
Which unit classes historically produce measurable product-balance consequences?

Priority: S-

## W15X-E03 — TCEQ Power-Loss Cascade

Many refinery/petrochemical events explicitly identify external/internal power interruption.

Graph:
power loss
-> unit trips
-> flaring
-> restart
-> product yield disruption.

Fuse with regional grid telemetry to distinguish common-cause storm/grid events from plant-specific failures.

Priority: A+

## W15X-E04 — TCEQ Planned Startup/Shutdown Calendar

The public database distinguishes maintenance, startup and shutdown activity from unplanned emissions events.

Research:
planned operational events as a forward capacity calendar.

Hard rule:
separate planned MSS from unexpected outage signals.

Priority: A+

## W15X-E05 — TCEQ Notification Delay Feature

Store:
event discovered/start
initial notification
public first seen
final report.

Feature:
notification_delay.

Do not assume 24-hour statutory ceiling equals actual public latency.

Priority: A

## W15X-E06 — South Coast AQMD Real-Time Flare Pulse

Primary source:
South Coast AQMD Flare Event Notification System (FENS).

FENS states that flare notifications are listed in real time and are preliminary.

Rule 1118 applies to petroleum refineries and related hydrogen/sulfur recovery facilities.

Build:
planned/unplanned
start/end
facility
vent-gas/emission threshold state
event persistence.

Priority: S

## W15X-E07 — Planned-vs-Unplanned California Flare Split

Rule 1118 requires planned event notice in advance for threshold-exceeding flares and rapid notice for qualifying unplanned events.

Research separately:
PLANNED_MAINTENANCE
STARTUP_SHUTDOWN
UNPLANNED_PROCESS_UPSET
POWER_LOSS
OTHER.

Priority: S-

## W15X-E08 — Real-Time Flare Escalation Ladder

FENS public states distinguish lower/higher event thresholds.

Build a time-varying state:
NONE
MINOR_FLARE
MAJOR_FLARE
PROLONGED_MAJOR
RECOVERY.

Test whether escalation predicts unit outage duration or regional product spreads.

Priority: A+

## W15X-E09 — Cross-Jurisdiction Refinery Disturbance Consensus

Fuse Texas and California mandatory/real-time refinery disturbance feeds into a normalized ontology.

Goal:
learn unit/event severity without assuming identical reporting thresholds.

Priority: A

## W15X-E10 — NASA FIRMS Industrial Thermal Anomaly

Primary source:
NASA LANCE FIRMS VIIRS/MODIS thermal anomalies.

NASA documents global NRT availability generally within ~3 hours and faster RT/URT availability in the U.S./Canada.

Thermal anomalies can include persistent gas flares.

Research:
facility geofence
× anomaly count
× fire radiative power
× day/night
× persistence
× historical facility baseline.

Priority: S

## W15X-E11 — Thermal Flare Appearance Shock

At a known refinery/LNG/petrochemical flare location:

feature =
current thermal intensity
-
expected facility/time/sensor baseline.

Hypothesis:
sudden flare appearance/intensification can corroborate or precede operational upset reporting.

Priority: S

## W15X-E12 — Thermal Flare Disappearance Shock

Persistent industrial flare sites can also go unexpectedly dark.

Possible causes:
normal operational change,
unit shutdown,
cloud/observation gaps,
sensor geometry.

Require multi-sensor / missing-data controls before interpreting disappearance.

Priority: A+

## W15X-E13 — Satellite × Mandatory Report Confirmation

Fuse:
NASA thermal anomaly
+ TCEQ/FENS event.

States:
REGULATORY_ONLY
SATELLITE_ONLY
CONFIRMED_BY_BOTH
CONFLICTING.

Question:
Does dual-source confirmation better predict real production loss/duration?

Priority: S

## W15X-E14 — Facility Heat Footprint Change

Beyond a single flare:
measure count/spatial distribution of persistent hot pixels around known industrial complexes.

Targets:
refinery
LNG
steel
cement
chemical.

This is exploratory; facility heat may be unrelated to throughput.

Priority: A

## W15X-E15 — Industrial Thermal Recovery Half-Life

After thermal/upset shock:
peak anomaly
50% normalization
baseline re-entry
second flare/restart signature.

Test whether thermal recovery aligns with physical production recovery.

Priority: A+

## W15X-E16 — BSEE Offshore Storm Shut-In Pulse

Primary source:
Bureau of Safety and Environmental Enforcement hurricane activity updates.

During storm events BSEE reports daily:
platforms evacuated
rigs evacuated/moved
oil BOPD shut-in
gas MMCFD shut-in
percentage of Gulf production.

Priority: S

## W15X-E17 — Offshore Preemptive-vs-Damage Shut-In

Storm shut-ins can be precautionary and quickly reversible or damage-related and persistent.

Build:
PREEMPTIVE_EVAC
PEAK_SHUTIN
RAPID_RESTART
DAMAGE_DELAYED_RESTART.

Use post-storm recovery trajectory.

Priority: S-

## W15X-E18 — Offshore Recovery Deficit

Feature:
expected restart path from historical comparable storms
-
observed BSEE recovery.

Hypothesis:
slow restoration is more informative for supply than peak precautionary shut-in.

Priority: S

## W15X-E19 — Gulf Shut-In × Refinery Disruption Collision

Fuse:
offshore oil/gas production loss
+ Gulf Coast refinery upset/flare state
+ pipeline/port status.

Mechanism:
upstream supply loss and downstream processing loss can offset or amplify product/crude balances depending on which side is constrained.

Priority: S

## W15X-E20 — NOAA/USCG Pollution Incident Corroboration

National Response Center public spreadsheets contain initial incident reports for pollution/railroad/chemical events.

Important:
the NRC explicitly states public spreadsheet data are initial and unvalidated, and real-time push notifications are government-only.

Use as:
secondary corroboration / retrospective event discovery,
not assumed live-public alpha.

Priority: B+

## W15X-E21 — Pipeline Incident Slow Confirmation

PHMSA incident data may confirm pipeline ruptures/releases and severity, but public reporting cadence is generally slower than plant/state operational feeds.

Use as:
post-event validation,
cause/severity labels,
recovery studies.

Priority: B

## W15X-E22 — EPA CAMPD Historical Operating-State Validator

EPA CAMPD exposes hourly power-plant emissions/operating data including load-related fields.

However, EPA guidance says hourly emissions and operating data are due within 30 days after quarter-end.

Therefore:
use for historical validation/training, not live trading triggers.

Priority: Validation only

## W15X-E23 — OSHA Severe-Injury Historical Operational-Risk Label

OSHA requires rapid employer reporting, but OSHA states the public severe-injury dataset has roughly a six-month lag.

Use:
facility/industry historical hazard prior
and post-event research.

Do NOT use as live operational signal.

Priority: Validation only

## W15X-E24 — Industrial Disturbance Confidence Score

Score event evidence by independent corroboration:
mandatory state notice
real-time flare notice
satellite thermal anomaly
grid/power disruption
BSEE/production impact
pipeline/port consequence.

Purpose:
separate "visible flare with no throughput consequence" from true capacity loss.

Priority: S

## W15X-E25 — Capacity-Loss Realization Ladder

General chain:

UPSET/FLARE/SHUT-IN
-> unit unavailable
-> throughput/yield change
-> inventory/basis response
-> substitute production/import
-> financial market.

No candidate promotes from incident detection directly to return prediction without intermediate validation.

Priority: S research architecture

## Highest-priority W15X tests

1. W15X-E01 TCEQ Refinery/Petrochemical Upset Pulse
2. W15X-E06 South Coast AQMD Real-Time Flare Pulse
3. W15X-E10 NASA FIRMS Industrial Thermal Anomaly
4. W15X-E11 Thermal Flare Appearance Shock
5. W15X-E13 Satellite × Mandatory Report Confirmation
6. W15X-E16 BSEE Offshore Storm Shut-In Pulse
7. W15X-E18 Offshore Recovery Deficit
8. W15X-E19 Gulf Shut-In × Refinery Disruption Collision
9. W15X-E24 Industrial Disturbance Confidence Score
10. W15X-E25 Capacity-Loss Realization Ladder
