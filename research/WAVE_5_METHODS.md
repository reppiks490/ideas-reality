# Wave 5 Research Methods

## M71 — First-Public Diff Ledger

For feeds that publish a whole mutable file rather than a clean event stream:
store every observed version with:
- fetched_at
- source release/version time
- SHA-256/content hash
- prior hash
- structured diff
- added/removed/modified records.

Applications:
OFAC, CISA KEV, sanctions lists, static catalogs and some regulatory feeds.

## M72 — Event-Sequence Fusion

Represent long causal chains as ordered events rather than one timestamp.

Example:
tariff proposal
-> final legal notice
-> customs implementation guidance
-> effective timestamp
-> import response
-> company margin/inventory response.

Test incremental information at each transition.

## M73 — Physical Deliverability Normalization

Raw warehouse stock is not enough.

Normalize by:
nearby OI,
average delivery volume,
withdrawal/load-out capacity,
imports,
eligible stock conversion history,
seasonality,
delivery-month clock.

## M74 — Shut-In / Restart Hazard Model

For storms:
model two hazards separately:
1. probability/rate of additional production shut-in
2. probability/rate of restoration.

Inputs:
forecast track vintages, intensity, platform exposure, current BSEE shut-in, post-storm infrastructure state.

## M75 — Network Exposure Propagation

For sanctions, cyber and cloud incidents:
event -> affected technology/entity -> direct exposure -> second-order dependency -> market target.

Require explicit exposure links and confidence scores.

## M76 — Retrospective-to-Live Transfer Test

For SEC MIDAS and other delayed rich datasets:
1. discover mechanism offline
2. define an equivalent live-computable feature
3. rebuild using only contemporaneously available licensed/public data
4. test forward without reusing retrospective target information.

## M77 — Periodic-Filing Availability Mask

A filing can disclose daily historical observations.

Every observation inherits:
economic_date
and
public_availability_date.

Features are unavailable until public_availability_date regardless of their economic_date.

Mandatory for N-MFP/N-MFP3 and similar periodic reports.

## M78 — Source Calendar Model

Store source-specific:
business days,
holidays,
expected publication window,
storm/event activation rules,
maintenance windows,
late-report behavior.

Missing expected data and "not scheduled today" are different states.

## M79 — Hash-and-Diff Ingestion

For every mutable list/feed:
immutable raw payload
+ canonicalized representation
+ content hash
+ structural diff.

Do not let a replaced file erase what the market could previously know.

## M80 — Externality Sign Matrix

Before fitting disruption events enumerate possible signs for:
upstream supply,
downstream demand,
exports,
imports,
substitutes,
inventory,
freight,
basis.

Example:
Gulf hurricane can simultaneously reduce crude supply and refinery demand.

## M81 — Cross-Source Event Deduplication

One event may appear in:
Federal Register,
agency press release,
CBP/OFAC/CISA feed,
news,
company filing.

Create canonical event IDs and source-observation records instead of counting each appearance as a new event.

## M82 — Production-Rights Gate

Research availability does not imply production redistribution rights.

Every source receives:
PUBLIC_COMMERCIAL_OK
PUBLIC_NONCOMMERCIAL
ATTRIBUTION_REQUIRED
ACCOUNT_REQUIRED
PAID_LICENSE
TERMS_REVIEW
FUTURE.

Implementation cannot promote until rights are reviewed.

## M83 — Triggered-Seasonality Conditioning

Some sources only activate under special circumstances.

Examples:
BSEE hurricane reports.

Evaluate conditional on active-event windows rather than contaminating the model with years of meaningless zeros.

## M84 — Delivery-Cycle Clock Control

For physically delivered futures, explicitly encode:
first notice day,
last trade,
delivery period,
roll window,
warehouse report cadence.

Avoid mistaking normal delivery-cycle stock movements for alpha.

## M85 — Exposure-Confidence Gating

A sanctions/cyber/cloud event can only create a company-level feature if dependency mapping exceeds a predeclared confidence threshold.

Unknown exposure -> abstain.

## M86 — Operational Constraint Counterfactual

For port/airport/logistics signals:
predict the operational outcome first:
queue,
throughput,
delay,
shut-in,
closure duration.

Only then test price/return.

## M87 — Observation-vs-Prediction Residual

NOAA PORTS and weather sources often provide both predictions and realized observations.

Use:
realized - predicted
rather than raw tide/current/wind values where appropriate.

## M88 — Public-vs-Private Data Boundary Test

Document whether the apparent edge requires:
public data,
licensed exchange data,
account-specific data,
or private vendor labels.

A public research thesis cannot silently rely on nonpublic fields.

## M89 — Event-Activation Timestamp Audit

For unstructured official notices:
store:
page publication time,
document effective time,
event start time,
first-seen crawl time.

Do not collapse these into one timestamp.

## M90 — Physical Recovery Curve

Disruption alpha may lie in recovery, not initial shock.

Estimate:
time-to-50%-recovery,
time-to-90%-recovery,
recovery overshoot,
queue liquidation rate,
restart asymmetry.

Applications:
ports, BSEE shut-ins, grid outages, cloud incidents.
