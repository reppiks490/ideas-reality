# Wave 25R — Reserve, Ramp & Flexibility Scarcity

Namespace: **W25R**

Thesis: a system can have enough installed and available MW yet still be operationally fragile because it lacks sufficiently fast, sustained, deliverable response. Reserve and ramp markets directly price that flexibility.

All candidates are research hypotheses only. Claude owns implementation.

## W25R-E01 — ERCOT Real-Time Ancillary Service Price Surface
Track real-time clearing prices for each ancillary-service product under RTC+B.
Priority: S

## W25R-E02 — Ancillary Service Demand-Curve Position
Use ERCOT DAM/SCED AS demand curves to locate the system on the nonlinear scarcity curve.
Priority: S

## W25R-E03 — Real-Time AS Capability Headroom
available AS capability - cleared AS requirement/award.
Priority: S

## W25R-E04 — Reserve Capability Compression
AS headroom / requirement and its interval-to-interval change.
States: ABUNDANT / NORMAL / TIGHT / SCARCE / SHORT.
Priority: S

## W25R-E05 — Energy-vs-Reserve Opportunity Cost
Compare energy scarcity price, AS price and remaining feasible capability under co-optimization.
Priority: A+

## W25R-E06 — Battery State-of-Charge Flexibility Tax
RTC+B incorporates SOC, capability, ramp and duration. Nominal battery MW can overstate reserve value when duration/SOC is depleted.
Priority: S

## W25R-E07 — Duration-Adjusted Reserve Capability
Convert qualified/available MW into duration-feasible reserve by product-specific sustainment requirements.
Priority: S

## W25R-E08 — Regulation Scarcity
Track regulation requirement, awards/capability and clearing price.
Priority: A+

## W25R-E09 — Responsive Reserve Scarcity
Track responsive-reserve supply/demand state and price intensity.
Priority: A+

## W25R-E10 — Contingency Reserve Scarcity
Track contingency reserve relative to forced-outage/largest-contingency conditions.
Priority: S-

## W25R-E11 — Non-Spinning Duration Stress
High non-spin scarcity may indicate multi-hour flexibility shortage, not merely instantaneous MW scarcity.
Priority: A+

## W25R-E12 — Real-Time Price Adder State
Track ERCOT reliability/online deployment price adders under current RTC+B semantics.
Priority: S-

## W25R-E13 — Day-Ahead-to-Real-Time AS Surprise
DAM AS outcome versus RT AS outcome = unexpected flexibility scarcity/abundance.
Priority: S

## W25R-E14 — Reserve Migration Across Resource Classes
Study reallocation among storage, thermal and other qualified resources where public data permit.
Priority: A

## W25R-E15 — Reserve Deliverability Risk
Fuse nominal AS availability with W23T transmission topology to estimate reserve trapped behind constraints.
Priority: S

## W25R-E16 — Reserve Scarcity × Forced Outage Collision
Fuse W25R reserve headroom with W24A forced-outage surprise.
Priority: S

## W25R-E17 — Reserve Scarcity × Gas Constraint Collision
Fuse W25R with W22G to identify reserve-providing gas units exposed to transport scarcity.
Priority: S-

## W25R-E18 — PJM Reserve Requirement / Price State
Normalize current PJM synchronized/non-synchronized/secondary reserve requirement, schedule, price and shortfall semantics.
Priority: A+

## W25R-E19 — PJM Reserve Shortfall Event
Identify intervals where reserve procurement fails to satisfy requirement or shortage pricing activates.
Priority: S-

## W25R-E20 — PJM Reserve-to-Emergency-Max Dependence
Reserve requirement + available reserve + W24A emergency-max dependence.
Priority: A+

## W25R-E21 — CAISO Imbalance Reserve Up/Down State
Track 2026 DAME/EDAM imbalance reserve up/down requirement, award, price and shortfall where public.
Priority: S-

## W25R-E22 — CAISO Reliability Capacity Up/Down State
Track reliability capacity up/down separately from imbalance reserve.
Priority: A+

## W25R-E23 — CAISO Fast Ramp / Uncertainty State
Track current fast-flexibility products/requirements against forecast uncertainty using current market definitions.
Priority: A+

## W25R-E24 — Net-Load Forecast Error Pressure
(actual net load - forecast net load) scaled by available upward/downward reserve and ramp.
Priority: S

## W25R-E25 — Ramp Deficit Hazard
required next-interval ramp - feasible available ramp, separately upward/downward.
Priority: S

## W25R-E26 — Renewable Ramp Collision
Solar/wind forecast change/error × available ramp × storage SOC × transmission limits.
Priority: S-

## W25R-E27 — Reserve Price Without Energy Scarcity
Intervals where AS price spikes while energy remains moderate may indicate flexibility shortage before energy shortage.
Priority: S

## W25R-E28 — Energy Price Without Reserve Scarcity
Negative control for fuel/congestion-driven price spikes.
Priority: A

## W25R-E29 — Reserve Scarcity Lead-Lag
Test whether reserve/ramp stress precedes energy spike, emergency state, forced-outage escalation or congestion.
Priority: S

## W25R-E30 — Fast-Flexibility Substitution Quotient
FFSQ = required rapid-response capability / available deliverable duration-feasible rapid-response capability.
Priority: S

## W25R-E31 — Reserve Quality Vector
Weight reserve by response speed, duration, deliverability, SOC/fuel sufficiency, ramp and start status.
Priority: S

## W25R-E32 — Flexibility Scarcity State Vector
Combine AS_HEADROOM, AS_PRICE, PRICE_ADDER, RAMP_HEADROOM, FORECAST_ERROR, SOC_DURATION, TRANSMISSION_DELIVERABILITY and FORCED_OUTAGES.
Output: FLEXIBLE / NORMAL / TIGHT / FRAGILE / SCARCE.
Priority: S

## Highest-priority tests
W25R-E03, E04, E06, E13, E15, E16, E24, E25, E30, E32.
