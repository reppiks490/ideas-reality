# Wave 9C — Capacity Rights Before Reality

Namespace: **W9C**

Thesis: many economically important commitments become public as licenses, assignments, permits, leases, queue positions, or ownership rights before physical capacity or revenue exists. Research the transition from **legal right -> committed project -> construction -> operation**, not merely the headline filing.

All candidates remain unproven research hypotheses for Claude.

## W9C-E01 — FCC Spectrum Rights Flow

Source:
FCC Universal Licensing System (ULS) / public licensing datasets.

Status:
LIVE public data; FCC publishes daily and weekly updates for ULS data.

Potential events:
- new license
- renewal
- modification
- spectrum lease
- assignment of authorization
- transfer of control
- partition/disaggregation
- consummation
- buildout-related filings.

Mechanism:
Spectrum access is a legal prerequisite for some wireless/network capacity. Rights changes may reveal footprint expansion, consolidation, divestment or strategic spectrum deployment before operational KPIs.

Priority: A+

## W9C-E02 — FCC Assignment / Transfer Control Graph

Construct:
license/call sign/band/geography
-> current licensee
-> assignee/transferee
-> parent issuer
-> transaction status.

Important ULS states include filed/consented/consummated and full/partial assignment.

Research:
estimate economic materiality from MHz-pop, geography, existing holdings and overlap rather than raw application counts.

Priority: S-

## W9C-E03 — Spectrum Buildout Obligation State

Use FCC application/authorization records and buildout-related attachments/confirmations where publicly structured.

Question:
Does a company move from merely owning spectrum to demonstrating buildout/use?

Candidate states:
ACQUIRED_RIGHT
PENDING_BUILDOUT
BUILDOUT_CONFIRMED
EXTENSION_REQUESTED
LAPSED / RETURNED.

This can separate financial spectrum inventory from productive network capacity.

Priority: A

## W9C-E04 — Patent Assignment Ownership Flow

Source:
USPTO Open Data Portal patent assignment API / daily assignment files.

Status:
LIVE public/open-data ecosystem; API key/account required for API access.

Official assignment data include:
- assignment received date
- recorded date
- execution date
- assignor
- assignee
- conveyance text
- reel/frame
- source document link.

Dataset is refreshed daily.

Mechanism:
IP ownership transfer can represent acquisition integration, technology licensing/transfer, internal reorganization, collateralization or disposition.

Hard timing:
execution date may precede public recordation. Use public recordation/first-seen timing.

Priority: S-

## W9C-E05 — Patent Financing / Security-Interest State

Assignment conveyance text can distinguish ordinary assignment from security-interest/collateral-related records where identifiable.

Research:
Does a change in patent collateralization/secured interest contain information about financing stress, debt capacity or asset-backed funding for IP-heavy firms?

Mandatory:
separate releases/terminations/corrections from new security interests.

Priority: B+

## W9C-E06 — Patent Portfolio Ownership Migration

Build:
patent family / technology class
-> legal owner history
-> public issuer
-> acquisition/divestiture event.

Features:
- technology-class inflow/outflow
- cross-company IP migration
- acquired patent age/quality proxies
- portfolio concentration
- patent transfer clusters.

First prove relation to later product/capex/M&A disclosures before testing returns.

Priority: A

## W9C-E07 — Patent Publication Innovation Pulse

Source:
USPTO application/publication datasets.

Research:
point-in-time publication flow by assignee and CPC/technology field.

Improve beyond patent count:
- continuation/family structure
- inventor breadth
- citation quality using only then-available citations
- technology novelty
- competitor overlap
- application-to-grant conversion history.

Priority: B+

## W9C-E08 — EPA ECHO Regulatory Capacity / Compliance State

Source:
EPA ECHO web services.

Status:
LIVE public integrated regulatory data.

ECHO integrates facilities regulated under major air, water, hazardous-waste and drinking-water programs and exposes public REST-style query services.

Research roles:
1. permit/compliance/enforcement state around major facilities
2. operational/regulatory stress confirmation
3. facility-to-issuer exposure graph.

Do not assume a permit record means new construction; distinguish authorization, compliance and enforcement semantics.

Priority: B+

## W9C-E09 — USACE Permit Pipeline

Sources:
USACE Regulatory Request System / public ORM data.

Status:
LIVE public permit and milestone data.

Official public datasets include:
- pending federally complete individual permit applications
- issued/denied actions
- public notice dates
- NEPA EA/EIS milestones
- Section 408 permissions
- emergency permits
- project name/applicant/location.

Mechanism:
For ports, pipelines, transmission, mining, industrial plants and large infrastructure, an Army Corps permit can be a gating legal milestone.

Priority: A+

## W9C-E10 — Permit Milestone Velocity

For a project:
PRE_APPLICATION
-> PUBLIC_NOTICE
-> FEDERALLY_COMPLETE
-> EA/EIS
-> PERMIT_DECISION
-> CONSTRUCTION.

Features:
- elapsed time at state
- accelerated/repeated review
- new public comments/requirements
- permit scope revision
- approval/denial probability.

Output:
expected project realization date and risk.

Priority: A

## W9C-E11 — Texas Drilling Permit Intent Pulse

Source:
Railroad Commission of Texas.

Status:
VERY HIGH FREQUENCY public operational data.

Official RRC files:
- pending drilling permits: generated twice daily around 11:30 a.m. and 5:30 p.m.
- current-month permit master/trailer: nightly
- completion query: nightly
- production: monthly.

Pending files expose submitted applications before final approval.

Features:
- operator permit count
- horizontal footage/depth
- county/field/basin
- new drill vs recomplete/re-entry
- amendment/expedite status
- concentration by operator
- development vs exploratory intent.

Priority: S

## W9C-E12 — Permit-to-Spud Conversion Hazard

A permit is an option, not a drilled well.

Link:
permit application
-> approval
-> spud
-> completion
-> first production.

Estimate conversion probability and lag by operator, basin, price regime and well type.

Candidate:
expected future wells = sum(permit_i * conversion_probability_i).

Priority: S

## W9C-E13 — Permit Intent vs Company Guidance Gap

Compare point-in-time public drilling permit activity with company-stated capex/production guidance.

Hypothesis:
permit acceleration/deceleration can reveal operational intent before quarterly reported production, especially when normalized by historical conversion behavior.

Control:
public vs private operators, acreage transactions and batch permitting.

Priority: A+

## W9C-E14 — BOEM Lease-Bid Revealed Preference

Source:
Bureau of Ocean Energy Management lease sales.

Status:
LIVE event-driven public data.

BOEM publishes:
- tracts receiving bids
- bidder/company
- bid amounts
- lease-sale statistics
- later acceptance/rejection/phase decisions
- lease ownership/operator datasets.

Mechanism:
Competitive bid willingness reveals private valuation of resource rights, but must be normalized for tract geology, lease terms and bidder portfolio.

Priority: A+

## W9C-E15 — Offshore Lease Acceptance / Ownership State

State:
OFFERED
-> BID
-> ACCEPTED/REJECTED
-> LEASE_EFFECTIVE
-> OWNERSHIP_TRANSFER
-> OPERATOR_CHANGE
-> EXPIRED/RELINQUISHED.

Build project-level and issuer-level offshore acreage/rights pipeline with first-public timestamps.

Priority: A

## W9C-E16 — PJM Interconnection Queue Project State

Source:
PJM public cycle/service-request status.

Status:
LIVE public planning information.

Public project data can include:
- submitted date
- projected/actual in-service
- withdrawn date
- status
- transmission owner
- project/resource type
- MW energy/capacity
- project study reports.

State:
REQUESTED
-> STUDY_PHASE
-> READINESS/DECISION
-> AGREEMENT
-> ENGINEERING & PROCUREMENT
-> UNDER_CONSTRUCTION
-> IN_SERVICE / WITHDRAWN.

Priority: S

## W9C-E17 — Interconnection Survival Probability

Raw queue MW drastically overstates future capacity because projects withdraw.

Estimate project survival using:
- resource type
- queue/cycle
- study phase
- network upgrade cost
- requested MW
- location/transmission owner
- time in queue
- readiness milestone
- developer history.

Output:
probability-weighted future capacity by region and date.

Priority: S

## W9C-E18 — EIA-860M Realization Confirmation

Source:
EIA Preliminary Monthly Electric Generator Inventory.

Status:
LIVE monthly preliminary inventory.

EIA-860M tracks existing, proposed and retired generators >=1 MW and planned additions, using monthly surveys and research.

Use as a downstream truth layer:
interconnection queue
-> construction/owner report
-> EIA-860M planned/operating status.

Important:
EIA says monthly estimates are preliminary and can be corrected in later releases. Archive vintages.

Priority: A+

## W9C-E19 — Capacity Rights-to-Reality Gap

General state model:
LEGAL_RIGHT
-> PROJECT_COMMITMENT
-> PERMIT/STUDY
-> CONSTRUCTION
-> OPERATION
-> UTILIZATION.

Inputs can include:
FCC spectrum
USPTO IP
USACE permits
drilling permits
BOEM leases
PJM queue
EIA generator inventory.

Output:
realization probability and expected time-to-operation.

Priority: S architecture

## W9C-E20 — Rights Acquisition Breadth

Across an issuer, aggregate newly acquired future-capacity rights:
spectrum
+ patents/IP
+ drilling rights/permits
+ offshore leases
+ grid interconnection
+ major infrastructure permits.

Do not sum raw counts. Convert each to probability-weighted economic capacity/value.

Question:
Does broad cross-domain commitment acceleration predict future capex, production or revenue revisions?

Priority: A

## Highest-priority Wave 9C tests

1. W9C-E11 Texas Drilling Permit Intent Pulse
2. W9C-E12 Permit-to-Spud Conversion Hazard
3. W9C-E16 PJM Interconnection Queue State
4. W9C-E17 Interconnection Survival Probability
5. W9C-E04 Patent Assignment Ownership Flow
6. W9C-E02 FCC Assignment / Transfer Graph
7. W9C-E14 BOEM Lease-Bid Revealed Preference
8. W9C-E09 USACE Permit Pipeline
9. W9C-E19 Capacity Rights-to-Reality Gap
10. W9C-E18 EIA-860M Realization Confirmation
