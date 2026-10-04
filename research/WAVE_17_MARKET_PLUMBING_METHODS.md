# Wave 17P — Research Methods

Namespace: **W17P**

## W17P-M01 — Status Transition Archive
Poll/archive public service-status pages with:
first_seen
last_seen
severity
message
service
source hash.

Current status pages often do not provide complete historical incident series.

## W17P-M02 — Public-vs-Client Rights Gate
Tag every timestamp:
PUBLIC
SUBSCRIBER
MEMBER_ONLY
POST_EVENT_PUBLIC.

Never backtest with member/client-only alerts as public information.

## W17P-M03 — Service Criticality Weight
Weight by settlement/payment role rather than equal-counting all services.

## W17P-M04 — Clock-Aware Severity
Model exact proximity to service cutoffs and settlement deadlines.

## W17P-M05 — Restoration-vs-Catchup
Separate service restoration from participant backlog/reconciliation completion.

## W17P-M06 — Planned Maintenance Mask
Scheduled maintenance, testing and migration are not outages.

## W17P-M07 — Incident Parent/Child Model
One infrastructure event can affect multiple services/venues.

Preserve a parent incident and child service states.

## W17P-M08 — Venue Market-Share Normalization
Operational breadth should be weighted by relevant product/venue share.

## W17P-M09 — SIP-vs-Direct-Feed Distinction
A SIP issue may have different impact on participants using direct feeds.

Do not treat all market participants as having identical information paths.

## W17P-M10 — Execution-vs-Data-vs-Posttrade Taxonomy
Classify impairment layer exactly:
DATA
ORDER_ENTRY
MATCHING
DROP_COPY
CLEARING
SETTLEMENT
PAYMENT.

## W17P-M11 — DTCC Vintage Discipline
Public Important Notices can describe prior-day incidents.

Availability begins at notice publication, unless a contemporaneous public source exists.

## W17P-M12 — Funding Consequence Validation
For settlement disruptions test:
repo rates
fails
intraday liquidity
clearing-fund changes
bank reserves
dealer balance-sheet proxies.

## W17P-M13 — Alternate-Rail/Alternate-Venue Control
Venue-specific failures may route around; payment/settlement failures may not.

Estimate substitutability.

## W17P-M14 — Event Rarity Handling
Use event studies, case-control matching and Bayesian priors rather than data-hungry black-box models for rare systemic incidents.

## W17P-M15 — Same-Cause Dependency
Cloud/network/power incidents may impair multiple venues simultaneously.

Do not count correlated outages as independent evidence.

## W17P-M16 — Market Open/Closed Context
A service disruption outside active settlement/trading windows may have lower immediate impact but can create backlog risk.

## W17P-M17 — Counterfactual Cutoff Simulation
Estimate whether the disruption would have mattered absent an extension or contingency action.

## W17P-M18 — Operational Halt Price Control
Halts mechanically suppress observed trading; do not interpret zero volume as lack of demand.

## W17P-M19 — Risk-Gate Evaluation
Evaluate whether plumbing status improves:
slippage
fill quality
tail loss
failed-order rate
model calibration
before testing directional PnL.

## W17P-M20 — Audit-Grade Incident Bundle
Persist source snapshots, timestamps, affected services, rights class, resolution and downstream confirmation for every promoted incident.
