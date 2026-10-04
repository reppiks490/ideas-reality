# Wave 11S — Research Methods

Namespace: W11S

## W11S-M01 — State-Transition Survival Model
Estimate probability and time-to-next-stage, not one binary project flag.

## W11S-M02 — Intent Is Not Production
Permit, queue request, authorization and FID are distinct states with different conversion priors.

## W11S-M03 — Point-in-Time Project Snapshot
Archive each observed project state. Never backfill a later completion date into an earlier forecast as if known.

## W11S-M04 — Operator/Developer Fixed Effects
Conversion ability differs materially by operator/developer. Estimate history-aware priors.

## W11S-M05 — Duplicate/Amendment Identity
Track permit/project amendments under stable well/project IDs; do not count revisions as new capacity.

## W11S-M06 — Geographic Asset Join
Use API/well IDs, coordinates, counties, pipeline corridors, substations/zones and explicit project IDs.

## W11S-M07 — Completion Disclosure Lag
Distinguish physical work date from filing/submission/publication date.

## W11S-M08 — Productivity Uncertainty
Completed well count does not equal production. Carry distributions for initial productivity and decline.

## W11S-M09 — Queue Attrition Calibration
Estimate realized historical commercial-operation rate by queue phase, fuel, developer and region.

## W11S-M10 — Probability-Weighted MW / Bcf/d
Expected future capacity = project capacity × probability of realization, with time discount/distribution.

## W11S-M11 — Schedule Revision Ledger
Store every expected-COD/in-service revision and classify delay, acceleration, cancellation, scope increase/decrease.

## W11S-M12 — Preliminary-vs-Final EIA Vintage
EIA-860M is preliminary. Preserve monthly vintages and final annual reconciliation.

## W11S-M13 — Regulatory Milestone Graph
FERC project documents are linked lifecycle states, not independent events.

## W11S-M14 — FID / Authorization Separation
DOE/FERC authorization does not imply construction/FID; construction/FID does not imply on-time operation.

## W11S-M15 — First-Flow Confirmation
A project becomes operating only after an independent physical/official operating observation, not an expected date.

## W11S-M16 — Capacity-Factor Scenario
Translate generation MW to fuel demand using distributions for capacity factor and heat rate.

## W11S-M17 — Retirement / Addition Netting
Regional future supply is additions minus retirements/cancellations, not gross queue MW.

## W11S-M18 — Constraint-Aware New Capacity
New generation/pipeline capacity only matters where transmission/pipeline deliverability permits utilization.

## W11S-M19 — Commodity-Price Endogeneity
Oil/gas prices influence permit/completion decisions. Control for commodity-price regime before claiming supply signals predict prices causally.

## W11S-M20 — Intermediate Validation
Permit model must predict completion; completion model must predict production; queue model must predict commercial capacity before market-return testing.
