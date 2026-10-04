# Wave 14I — Research Methods

Namespace: **W14I**

## W14I-M01 — Capacity-to-MW Normalization
Convert reactor percent power to estimated MW only using point-in-time nameplate/net capacity metadata.

## W14I-M02 — NRC Event Availability Ledger
Store:
event_time,
licensee_notification_time,
NRC_publication/first_seen_time,
update times,
daily-status appearance time.

## W14I-M03 — Forced-vs-Planned Outage Classifier
Pre-register planned outage/coastdown semantics. Never let known refueling periods count as surprise outage alpha.

## W14I-M04 — Replacement-Mix Identification
For each RTO/BA estimate which resources actually replace lost generation from observed dispatch/interchange, not a fixed "nuclear -> gas" rule.

## W14I-M05 — Outage Duration Survival Model
Use censoring correctly for outages still ongoing at sample end.

## W14I-M06 — Same-Weather Common Cause Control
Nuclear trips, grid outages and gas demand can share a weather cause. Condition on weather/system events.

## W14I-M07 — Reservoir Item-Specific Cadence
RISE items have different update schedules/units. Store source item ID, timestep, update time and unit explicitly.

## W14I-M08 — Water-Level-to-Power Nonlinearity
Hydro capability depends nonlinearly on head, turbine limits, water obligations and plant configuration.

Avoid linear storage-to-MWh assumptions.

## W14I-M09 — Operational-Obligation Control
Reservoir releases can be driven by flood control, environmental flows, irrigation or municipal requirements, not electricity economics.

## W14I-M10 — Seasonal Water-Year Baseline
Normalize reservoir state by water year, snow/inflow season and operating rules.

## W14I-M11 — Panama Advisory Vintage Archive
Archive each ACP Advisory to Shipping and its effective dates.

Postponements and reversals are new information.

## W14I-M12 — Slot-vs-Transit Separation
Booked slot availability != realized daily transits.

Store both when available and study the gap.

## W14I-M13 — Draft-to-Cargo Capacity Model
Translate draft change to cargo capacity by vessel class using naval/shipping relationships and actual vessel characteristics where licensed/public.

## W14I-M14 — Route Substitution Cost
Alternative routing impact must include:
extra nautical miles,
speed,
fuel,
canal/port fees,
vessel-days,
insurance/risk,
cargo timing.

## W14I-M15 — Cargo-Class Exposure
Panama constraints have different economics for LNG, LPG, containers, vehicles and bulkers.

Do not pool them blindly.

## W14I-M16 — Ice Geography, Not Lake Average
Use route/channel-specific ice data when possible.

Lake-wide average can hide severe local chokepoints.

## W14I-M17 — Icebreaker Mitigation Control
Ice cover alone is not effective capacity loss.

Condition on Coast Guard assistance, vessel ice class, convoy/escort and route.

## W14I-M18 — Stockpile/Inventory Adaptation Control
Commodity users can stockpile ahead of seasonal shipping constraints.

Model inventory buffer before inferring production impact.

## W14I-M19 — Constraint Realization Ladder
For all W14I candidates test:
constraint signal
-> operational capacity
-> substitute usage
-> physical price/basis
-> financial market.

## W14I-M20 — Substitute Capacity Gate
A capacity-loss signal promotes only if the research can estimate whether substitutes were actually scarce.
