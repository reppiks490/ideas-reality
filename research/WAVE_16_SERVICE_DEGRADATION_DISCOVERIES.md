# Wave 16S — Service Degradation & Administrative Throughput

Namespace: **W16S**

Thesis: systems often fail economically before they fail physically. Throughput can deteriorate while railroads still run, airports remain open, customs systems remain online, or manufacturers continue shipping. Public operational/service data can expose this degradation before monthly production or trade statistics fully register it.

All candidates are research hypotheses only. Claude owns any later implementation.

## W16S-E01 — STB Rail Velocity Stress

Primary source:
U.S. Surface Transportation Board EP 724 weekly Class I rail service data.

STB requires Class I rail carriers to provide weekly service-performance reports and states the data give the public greater real-time visibility into Class I performance.

Build:
- system/train-type speed residual
- carrier percentile
- multiweek acceleration/deceleration
- commodity-train-specific deviation.

Priority: S-

## W16S-E02 — Terminal Dwell Stress

STB reports weekly average terminal dwell by major terminals.

Feature:
terminal dwell
-
historical terminal/season baseline.

Interpretation:
high dwell can indicate yard congestion, crew/equipment imbalance, weather disruption or network blockage.

Priority: S-

## W16S-E03 — 48-Hour Immobile Car Accumulation

STB Item 6 tracks loaded/empty cars in revenue service that have not moved for 48 hours or greater.

Candidate:
immobile_car_share
× duration trend
× network breadth.

This may reveal hidden congestion before average speed collapses.

Priority: S

## W16S-E04 — Trains Held by Cause

STB weekly service reports include trains held per day by train type and cause.

Build cause-specific states:
CREW
LOCOMOTIVE
POWER/MECHANICAL
TERMINAL
CUSTOMER
WEATHER
INTERCHANGE
OTHER.

Question:
Which causes have the longest persistence and strongest downstream commodity impact?

Priority: A+

## W16S-E05 — Origin Dwell for Unit Trains

Unit-train origin dwell can expose loading/release bottlenecks distinct from line-haul movement.

Research by commodity:
grain
coal
crude
ethanol
other unit service where reported.

Priority: A+

## W16S-E06 — Grain Car Order Backlog

STB service metrics include grain-car orders outstanding/filled and past-due information for relevant carriers.

Candidate:
unfilled/past-due orders
relative to
seasonal grain demand and crop/export state.

Priority: S

## W16S-E07 — Chicago Gateway Congestion State

STB reporting includes Chicago gateway information.

Build:
carrier-pair/interchange congestion
× terminal dwell
× held trains
× downstream route dependence.

Priority: A

## W16S-E08 — Rail Congestion Propagation Graph

Graph:
terminal/network bottleneck
-> commodity lane
-> plant/port destination
-> industrial inventory
-> production/export risk.

Do not map a carrier-wide slowdown directly to every customer.

Priority: A+

## W16S-E09 — Rail Recovery Half-Life

Measure:
speed trough
dwell peak
held-train peak
50% normalization
full normalization.

Hypothesis:
slow recovery after a disruption is more informative than the initial shock.

Priority: A+

## W16S-E10 — FAA Real-Time Cargo-Hub Constraint

Primary source:
FAA NAS Status.

FAA NAS Status exposes real-time airport closures, ground stops, ground delay programs, arrival/departure delays and deicing events, with machine-readable XML access.

For major cargo hubs:
build event duration, severity and reason.

Priority: S-

## W16S-E11 — FAA Forecast Constraint Lead

FAA NAS Status also exposes forecast events such as expected/possible ground stops or delay programs.

Research:
FORECAST
-> ACTIVATED
-> EXTENDED
-> RECOVERED.

Question:
Does the forecast stage provide measurable lead time for cargo-network disruption?

Priority: S

## W16S-E12 — Airport Acceptance-Rate Compression

Ground Delay Programs reflect airport acceptance-rate constraints.

Feature:
actual/expected arrival acceptance capacity
relative to
normal hour/day baseline.

Map to cargo-hub importance rather than treating passenger and freight traffic equally.

Priority: A+

## W16S-E13 — Ground Stop Severity

Build:
scope
× probability of extension
× duration
× airport cargo importance
× network centrality.

A 30-minute local stop is not equivalent to a multi-hour national-scope stop at a cargo hub.

Priority: A+

## W16S-E14 — Cargo-Hub Network Substitution

Graph:
constrained hub
-> alternate hubs
-> truck linehaul
-> remaining air lift
-> sort/transfer schedule.

Goal:
estimate whether logistics networks can absorb the disruption overnight.

Priority: A

## W16S-E15 — FAA Deicing / Weather Capacity Tax

Deicing and weather-driven traffic initiatives can reduce practical sort-window capacity even without airport closure.

Research:
weather constraint timing
relative to
overnight cargo bank.

Priority: A

## W16S-E16 — CBP ACE Processing Degradation Pulse

Primary source:
U.S. Customs and Border Protection Cargo Systems Messaging Service (CSMS).

CBP publishes timestamped messages for ACE availability, slow processing, maintenance, outages and resolution.

Candidate states:
NORMAL
DEGRADED
PARTIAL_OUTAGE
FULL_OUTAGE
BACKLOG_CLEARING
RESOLVED.

Priority: S

## W16S-E17 — ACE Modality-Specific Outage

Separate affected channels:
air
truck
ocean
rail
cargo release
entry summary
manifest
portal UI
EDI.

A portal UI issue may have little physical impact if EDI remains normal; a manifest/release backlog can be economically meaningful.

Priority: S

## W16S-E18 — ACE Backlog-Clearance Duration

Some CSMS messages explicitly note delayed response queues/backlog and later resolution.

Measure:
outage onset
acknowledgement
partial restoration
queue cleared
fully resolved.

Priority: S-

## W16S-E19 — Planned Maintenance vs Unplanned ACE Failure

CBP also announces scheduled production maintenance.

Separate:
PLANNED_MAINTENANCE
DEPLOYMENT
UNPLANNED_SLOWDOWN
UNPLANNED_OUTAGE.

Only surprise residual belongs in outage research.

Priority: A+

## W16S-E20 — Customs System × Border Queue Collision

Fuse:
ACE degradation
+ CBP commercial border wait time
+ port/terminal queue state.

Mechanism:
digital clearance degradation can turn into physical queueing depending on downtime procedures and mode.

Priority: S

## W16S-E21 — FDA National Drug Shortage Pulse

Primary source:
FDA Drug Shortage Database / openFDA.

FDA states the shortage list is updated daily with new, resolved and revised shortages and manufacturing-capacity information.

Fields include:
drug/product
company
status
availability
shortage reason
initial posting/update/change dates
therapeutic category
presentation/strength.

Priority: S-

## W16S-E22 — Drug Shortage Initiation Surprise

Classify new shortages by reason:
manufacturing/quality
demand increase
raw material/API
delay
discontinuation
other.

Feature:
new national shortage
× market concentration
× therapeutic substitutability
× company exposure.

Priority: A+

## W16S-E23 — Drug Shortage Resolution Velocity

Measure:
initial posting
manufacturer availability updates
partial availability
resolution date.

Question:
Does recovery duration reveal persistent manufacturing-capacity problems?

Priority: A

## W16S-E24 — Manufacturer Concentration Fragility

Graph:
shortage drug
-> manufacturer/applicant
-> active ingredient/API dependence
-> therapeutic substitutes
-> competing manufacturers.

Candidate:
shortage severity
× concentration
× substitute scarcity.

Priority: S-

## W16S-E25 — Shortage Cascade Across Therapeutic Substitutes

A shortage in one product can shift demand onto alternatives.

Graph:
drug A shortage
-> substitute B demand
-> B inventory/availability
-> secondary shortage.

Research only where clinical substitution relationships are sourced and non-speculative.

Priority: A

## W16S-E26 — Administrative Throughput Stress Vector

Combine independent throughput dimensions:
RAIL_NETWORK
AIR_CARGO
CUSTOMS_CLEARANCE
REGULATED_PRODUCT_SUPPLY.

Purpose:
measure economic flow impairment without requiring a facility shutdown.

Priority: S

## W16S-E27 — Service Degradation Before Hard Failure

General hypothesis:

degradation metrics
(speed↓, dwell↑, queue↑, delay↑, availability↓)
can predict
hard failure / missed production / shortage
better than binary outage indicators alone.

Priority: S research architecture

## Highest-priority W16S tests

1. W16S-E03 48-Hour Immobile Car Accumulation
2. W16S-E04 Trains Held by Cause
3. W16S-E06 Grain Car Order Backlog
4. W16S-E10 FAA Real-Time Cargo-Hub Constraint
5. W16S-E11 FAA Forecast Constraint Lead
6. W16S-E16 CBP ACE Processing Degradation Pulse
7. W16S-E18 ACE Backlog-Clearance Duration
8. W16S-E20 Customs System × Border Queue Collision
9. W16S-E21 FDA National Drug Shortage Pulse
10. W16S-E26 Administrative Throughput Stress Vector
