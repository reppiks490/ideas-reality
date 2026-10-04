# RDX07 — Aircraft Transfer & Fleet Realization

Thesis: aircraft orders/backlogs are not realized fleet. FAA public records can expose a staged process from registration/security-document receipt to final valid registration, deregistration/export, and legal operating status. The useful edge is actual aircraft/fleet realization by manufacturer serial number and operator exposure—not headline order announcements.

## RDX07-E01 — Daily Registry Document-Receipt Pulse
Use FAA Aircraft Document Index receipt date, collateral/N-number, party, document ID/type.

## RDX07-E02 — New-Aircraft Registration Application Precursor
Classify document types consistent with registration/ownership transfer; do not treat every received document as a delivery.

## RDX07-E03 — Document Receipt-to-Registration Clock
Receipt date -> final valid registration / master-file state.

## RDX07-E04 — Registration Processing Backlog
Current registry processing delay as a measurement-lag state; distinguish underlying fleet event from final master update latency.

## RDX07-E05 — Manufacturer Serial Identity
Map N-number to manufacturer/model/serial number using FAA reference/master data.

## RDX07-E06 — OEM Delivery Candidate
New serial number enters U.S. registry workflow and subsequently becomes validly registered to airline/lessor/customer.

## RDX07-E07 — Delivery Confirmation State
DOCUMENT_RECEIVED -> REGISTRATION_PENDING -> VALID -> AIRWORTHINESS/OPERABLE confirmation where public.

## RDX07-E08 — False Delivery Filter
Reject events that are address changes, liens/security-only filings, N-number changes, trusts or administrative renewals.

## RDX07-E09 — Airline Fleet Entry
Aircraft becomes validly registered/operable and mapped to actual Part 121/135 operator or verified lessee/operator.

## RDX07-E10 — Lessor-vs-Operator Separation
Registered owner may be a lessor/trust/SPV rather than airline operator. Maintain owner, lessee and operator as separate entities.

## RDX07-E11 — Manufacturer Delivery Velocity
Confirmed serial deliveries per day/week/month by OEM/model.

## RDX07-E12 — Delivery Acceleration / Deceleration
Change in realized delivery cadence versus OEM guidance/order backlog.

## RDX07-E13 — Backlog Burn Rate
Confirmed deliveries / point-in-time firm backlog by family/customer.

## RDX07-E14 — Airline Fleet Growth
Net newly operable aircraft minus deregistrations/exports/retirements by operator.

## RDX07-E15 — Aircraft Export State
FAA registration cancellation for export, destination country and serial identity.

## RDX07-E16 — Export Delivery Confirmation
U.S.-registered aircraft sold/exported to foreign operator; model as fleet transfer, not necessarily OEM new delivery.

## RDX07-E17 — Import Registration State
Previously foreign-registered aircraft entering U.S. registry; separate used import from new OEM delivery.

## RDX07-E18 — Deregistration Reason
Export / destroyed / dismantled / retired / owner request carry different capacity implications.

## RDX07-E19 — Fleet Retirement Pulse
Permanent retirement/dismantling/deregistration mapped to operator/fleet age.

## RDX07-E20 — Registration-In-Question Capacity
Sale reported / registration pending aircraft can have restricted/temporary operating status; do not count as fully available fleet automatically.

## RDX07-E21 — Document Receipt as Early Transfer Signal
FAA Document Index is updated each federal working day and exposes filing receipt before final master processing.

## RDX07-E22 — Receipt-to-Operational-Lag Distribution
Estimate by transaction type, aircraft age, domestic/imported status and applicant class.

## RDX07-E23 — OEM Quarter-End Delivery Pressure
Realized delivery cadence and document receipts approaching quarter-end versus guidance.

## RDX07-E24 — Delivery Miss Hazard
Expected remaining deliveries to meet guidance / days remaining × historical feasible delivery pace.

## RDX07-E25 — Delivery Surprise
Actual confirmed fleet realization minus prior expected deliveries.

## RDX07-E26 — Model-Mix Surprise
Widebody/narrowbody/variant delivery mix versus expected mix, mapped to revenue/margin differences.

## RDX07-E27 — Customer Concentration
Delivery timing to strategically important airline/lessor customers.

## RDX07-E28 — Airline Capacity Realization
Aircraft delivery becomes meaningful only after entry into service; validate with schedule/operation/fleet sources where available.

## RDX07-E29 — Delivery-to-Utilization Lag
Valid registration/transfer -> first observed commercial operations.

## RDX07-E30 — Spare/Stored Aircraft State
Registered aircraft not necessarily actively utilized; combine operational evidence.

## RDX07-E31 — Security/Lien Filing Stress
Document Index/security records can reveal financing events; research separately from delivery and never infer distress from lien existence alone.

## RDX07-E32 — Repossession Event
FAA Certificate of Repossession/ownership transfer can indicate lessor-credit event when mapped correctly.

## RDX07-E33 — Lessor Fleet Reallocation
Aircraft transfers between operators/regions through ownership/registration/export changes.

## RDX07-E34 — Manufacturer Serial Bottleneck
Clusters of serials entering registration workflow but failing to reach valid/operable state may signal certification/documentation/delivery friction.

## RDX07-E35 — Fleet Realization × Maintenance Constraint
New deliveries can offset grounded/AD-constrained fleet only if model/crew/maintenance compatibility exists.

## RDX07-E36 — Fleet Realization × Labor Constraint
Aircraft capacity may arrive before pilots/mechanics/slots; map delivery to usable capacity.

## RDX07-E37 — Fleet Supply Quotient
FSQ = newly operable aircraft capacity / net required capacity after retirements/groundings/demand growth.

## RDX07-E38 — OEM Guidance Reality Gap
Company reported deliveries/guidance versus independent FAA registration/operation evidence.

## RDX07-E39 — Airline Capacity Reality Gap
Announced fleet growth versus legally/operationally realized fleet.

## RDX07-E40 — Fleet Truth Ladder
ORDER/BACKLOG -> SERIAL BUILT -> OWNERSHIP/REGISTRATION DOCUMENT RECEIVED -> VALID REGISTRATION/AIRWORTHINESS -> OPERATOR ASSIGNMENT -> ENTRY INTO SERVICE -> UTILIZATION/REVENUE.

## Highest-priority tests
E03, E06, E11, E14, E21, E24, E25, E29, E38, E40.
