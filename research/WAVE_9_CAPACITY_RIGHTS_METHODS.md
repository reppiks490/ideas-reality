# Wave 9C Research Methods

Namespace: **W9C**

## W9C-M01 — Rights-vs-Reality Separation
Never treat a license, patent, permit, lease or queue position as realized production. Every record receives a lifecycle state.

## W9C-M02 — Public Recordation Clock
Store execution/action date separately from agency recordation/publication/first-seen date. Only public availability can drive historical features.

## W9C-M03 — Conversion Hazard
Estimate probability and timing of transition from right/permit to operational state.

## W9C-M04 — Withdrawal / Abandonment Modeling
Explicitly model permit expiration, queue withdrawal, lease relinquishment and unused rights. Survivorship-only samples overstate realized capacity.

## W9C-M05 — Economic Unit Conversion
Convert raw rights into economic units:
MHz-pop,
MW,
expected wells/BOE,
acreage/tract value,
probability-weighted patent technology exposure.

## W9C-M06 — Entity Ownership History
Rights may move between subsidiaries and parents. Maintain legal-owner -> parent-issuer mapping with effective dates.

## W9C-M07 — Internal Reorganization Filter
Patent/license transfers among entities under common control are not equivalent to external acquisitions. Detect and label internal moves.

## W9C-M08 — Duplicate / Amendment Chain
Applications can be amended, extended or refiled. Link versions instead of counting each filing as a fresh commitment.

## W9C-M09 — Realization Truth Ladder
Validate against next layer:
permit -> spud,
queue -> construction,
patent assignment -> disclosed product/M&A/IP event,
spectrum -> buildout,
lease -> exploration/development.

## W9C-M10 — Operator Historical Conversion Prior
For drilling/projects, operator-specific conversion history is often more predictive than industry average.

## W9C-M11 — Cost-Adjusted Queue Survival
Interconnection study/network upgrade cost should enter project survival probability where publicly available.

## W9C-M12 — Rights Portfolio Concentration
Measure whether future capacity commitments are concentrated in one basin/band/technology/region or diversified.

## W9C-M13 — Competing-Rights Substitution
A firm may acquire rights then abandon older alternatives. Model net commitment, not gross filings.

## W9C-M14 — Permit Cycle Seasonality
Control for annual leasing rounds, budget cycles, filing batches, quarter-end permitting and regulatory deadlines.

## W9C-M15 — Vintage Preliminary Data
EIA-860M and mutable agency datasets must be archived by release vintage. Later corrected status cannot overwrite historical information.

## W9C-M16 — Geography-First Exposure
Use exact project/band/basin/tract/POI geography before assigning commodity or issuer exposure.

## W9C-M17 — Project Materiality Gate
A legally real project may still be immaterial to the public issuer. Normalize by existing capacity, enterprise value, production or revenue.

## W9C-M18 — Rights-Price Endogeneity Control
Companies acquire more rights when industry conditions are already strong. Control for contemporaneous prices, rates, policy and sector momentum.

## W9C-M19 — Batch Filing Detection
Detect bulk filings caused by administrative processes so a batch does not masquerade as sudden strategic acceleration.

## W9C-M20 — Prospective State Archive
For systems whose historical state snapshots are incomplete, begin prospectively archiving public state transitions before running live-edge claims.
