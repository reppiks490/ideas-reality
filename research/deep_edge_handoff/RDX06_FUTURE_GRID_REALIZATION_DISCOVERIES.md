# RDX06 — Future Grid Supply/Demand Realization

Thesis: announced generation, interconnection-queue MW and proposed data-center load are option-like projects, not realized capacity or demand. The valuable state is the probability-weighted future balance after project maturity, delay/cancellation risk, transmission deliverability, retirement changes and large-load firmness.

## RDX06-E01 — EIA-860M Monthly Generator State
Track every proposed/operating/retired/canceled/postponed generator vintage.

## RDX06-E02 — Construction Milestone Ladder
PROPOSED -> PERMITS/PLANNING -> UNDER_CONSTRUCTION <=50% -> >50% -> CONSTRUCTION_COMPLETE_NOT_COMMERCIAL -> OPERATING.

## RDX06-E03 — Planned COD Revision
Change in planned commercial operation date across monthly vintages.

## RDX06-E04 — COD Delay Velocity
Months of delay added per reporting cycle.

## RDX06-E05 — Commissioning Hazard
P(commercial operation in next N months | current EIA status, technology, developer, region).

## RDX06-E06 — Cancellation/Postponement Hazard
Probability project moves to canceled/postponed before operation.

## RDX06-E07 — Technology-Specific Completion Prior
Solar, battery, wind, gas and nuclear/other generation receive separate realization models.

## RDX06-E08 — Developer Execution Prior
Historical completion/delay rate by developer/operator where identity is stable.

## RDX06-E09 — Transmission-Constrained Capacity
Nameplate MW × probability of timely deliverability/interconnection.

## RDX06-E10 — Firm Capacity Equivalent
Translate new resource MW into dependable/seasonal capacity contribution under relevant market accreditation rules rather than raw nameplate.

## RDX06-E11 — Planned Retirement State
Track owner-reported retirement month/year and every revision.

## RDX06-E12 — Retirement Delay
Retirement date pushed later or cancellation of retirement as positive future capacity revision.

## RDX06-E13 — Retirement Acceleration
Retirement pulled forward as negative future capacity revision.

## RDX06-E14 — Retirement Realization Hazard
Estimate P(unit actually exits at reported date).

## RDX06-E15 — Regulatory Retention Shock
Emergency/regulatory orders delaying a retirement change future supply independently of owner plan.

## RDX06-E16 — Net Future Generation Revision
Probability-weighted additions minus retirements, by zone/month/technology.

## RDX06-E17 — Interconnection Queue Maturity
For PJM/MISO/ERCOT/etc., map project phase, study agreement, executed interconnection agreement, milestones and commercial operation.

## RDX06-E18 — Queue Attrition Prior
Historical probability project reaches operation from each queue phase.

## RDX06-E19 — Queue Withdrawal Contagion
One project withdrawal can change network assumptions/costs and affect neighboring queued projects; model cluster/network exposure.

## RDX06-E20 — Restudy Risk
Project milestone regression or restudy after other withdrawals/network changes.

## RDX06-E21 — Network Upgrade Burden
Required upgrade cost/timing relative to project economics and capacity.

## RDX06-E22 — Cost-Per-MW Interconnection Shock
Use public interconnection-cost information where available to update completion hazard.

## RDX06-E23 — ERCOT GIS Progress State
Monthly generator interconnection status and planned-resource trend by fuel/project.

## RDX06-E24 — MISO Commercial-Operation Delay State
Use MISO queue/COD dashboards to distinguish waiting, delayed and online projects.

## RDX06-E25 — Large Load Proposal State
Data center/manufacturing/other large load MW must be classified by public milestone/commitment, not counted at face value.

## RDX06-E26 — PJM Firm vs Non-Firm Large Load
PJM's 2026 forecasting explicitly gives greater weight to near-term firm commitments and derates less-certain large-load adjustments.

## RDX06-E27 — Large-Load Adjustment Revision
Track MW changes across PJM load forecast/subcommittee vintages.

## RDX06-E28 — Data-Center Forecast Error
Forecast large-load MW versus later realized metered load, by zone/project class.

## RDX06-E29 — Large-Load Realization Hazard
P(load energizes by date | service agreement/construction commitment/substation/transmission milestones).

## RDX06-E30 — Bring-Your-Own-Capacity State
New load paired with committed new generation has different system impact than unbacked large load.

## RDX06-E31 — Large Load × Transmission Constraint
Expected MW × local deliverability/network-upgrade burden.

## RDX06-E32 — Future Reserve-Margin Distribution
Monte Carlo/probabilistic reserve margin using project-specific additions, retirements, load and outages.

## RDX06-E33 — Future Scarcity Revision
Change in probability of reserve margin falling below threshold over 1–36 months.

## RDX06-E34 — Gas Burn Future Revision
Probability-weighted change in gas-fired generation requirement from generation/load revisions.

## RDX06-E35 — Capacity Price Exposure
Map future capacity-balance revisions to RTO capacity-market zone when relevant.

## RDX06-E36 — Utility Capex Burden
Expected network/generation investment triggered by large load, adjusted for cost allocation/regulatory recovery.

## RDX06-E37 — Data-Center Power Availability
For data-center/AI infrastructure issuers, estimate energizable MW by date rather than announced campus MW.

## RDX06-E38 — Power Constraint on AI Revenue
Energizable compute/power capacity versus company demand/capex plan.

## RDX06-E39 — Supply/Demand Milestone Surprise
New public project milestone changes probability-weighted future balance.

## RDX06-E40 — Future Capacity Truth Ladder
ANNOUNCED -> QUEUED -> STUDIED -> CONTRACTED -> CONSTRUCTION -> ENERGIZED -> COMMERCIAL/LOAD REALIZED -> ACTUAL OUTPUT/DEMAND.

## Highest-priority tests
E03, E05, E12, E16, E18, E21, E26, E29, E33, E40.
