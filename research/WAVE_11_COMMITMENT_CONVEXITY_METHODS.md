# Wave 11C — Research Methods

Namespace: **W11C**

## W11C-M01 — Mandatory-Disclosure Availability Clock
Store:
economic_event_time
reporting_deadline
source_received_time where observable
public_release_time
first_ingested_time.

Never backdate a mandatory report to transaction execution.

## W11C-M02 — Announcement vs Effective-Time Event Study
For margin/rule changes, treat notice and effective time as separate events.

Estimate pre-positioning and post-effective mechanical adjustment independently.

## W11C-M03 — Endogenous Policy-Change Control
Margins rise because volatility/risk changed.

Use matched unaffected products, volatility controls, cross-exchange differences and event-specific designs before attributing returns to the margin change itself.

## W11C-M04 — Collateral Burden Normalization
Normalize new margin by:
contract notional
realized volatility
expected shortfall proxy
open interest
typical account equity where defensible.

A $5,000 increase means different things across contracts.

## W11C-M05 — Daily-to-Weekly Export Reconciliation
Link USDA flash sales to later weekly records and shipment data.

Prevent:
double counting,
destination-change duplication,
cancellation omission,
marketing-year misclassification.

## W11C-M06 — Export Flash Expectation Model
Pre-register an expectation model before testing the 9:00 a.m. release.

Research surprise, not raw announcement size.

## W11C-M07 — TRACE Reporting-Delay Mask
For each securitized-product category, encode the exact then-current reporting deadline and dissemination rule.

Trade time != public time.

## W11C-M08 — Dissemination-Cap Censoring
TRACE may cap displayed size for some products.

Treat capped observations as censored, not exact notionals.

Use Tobit-like, interval or count/intensity approaches where appropriate.

## W11C-M09 — TBA Transaction-State Classification
Separate:
outright TBA
specified pool
stipulation
dollar roll
correction/reversal/as-of reporting.

Do not blend distinct financing/settlement economics.

## W11C-M10 — Convexity Intermediate Validation
Before testing NQ:
convexity state must explain incremental Treasury/swap duration pressure after macro news, rates level and volatility controls.

## W11C-M11 — Mortgage Vintage Integrity
GSE factor/prepayment and pool data are revisable/periodic.

Preserve publication vintage and never expose later factor information early.

## W11C-M12 — Small-Value Fed Operation Placebo
Because 2026 agency-MBS Desk operations are small readiness exercises, use them as timestamped placebo/identification events unless evidence shows economically meaningful size.

## W11C-M13 — Sparse Municipal Trade Handling
Municipal bonds trade irregularly.

Use:
matched-curve residuals,
last-trade staleness,
trade-size buckets,
issuer pooling,
hierarchical models.

Never forward-fill a stale muni quote as a live price.

## W11C-M14 — Municipal Exposure Confidence
Issuer geography/name similarity is insufficient.

Map CUSIP/issuer/obligor/insurer/holding exposure with confidence and effective dates.

## W11C-M15 — Emergency-State Survival Model
Model time-to-next-transition and time-to-recovery for PJM/ERCOT.

The target is a transition hazard, not a hindsight emergency dummy.

## W11C-M16 — Intervention Sign Decomposition
Grid emergency actions can:
raise scarcity prices,
reduce load,
activate backup generation,
change fuel burn,
interrupt industrial activity.

Model each channel separately.

## W11C-M17 — Cross-Market Common-News Neutralization
For TBA/Treasury/NQ or muni/equity tests, control for scheduled macro, rates and broad risk shocks before claiming venue leadership.

## W11C-M18 — Source-Rights Gate
Tag:
PUBLIC_WEB
PUBLIC_API
PAID_SUBSCRIPTION
LICENSED_REALTIME
DELAYED
RETROSPECTIVE.

A research edge may be valid yet unavailable for production at the required latency.

## W11C-M19 — Mandatory-vs-Voluntary Disclosure Test
Compare whether legally required disclosures have cleaner information content than voluntary company/news disclosures for the same underlying event.

## W11C-M20 — Commitment Realization Score
For every commitment event estimate:
probability of physical/financial completion
expected delay
expected cancellation/revision rate
capacity needed for completion.

Trade/research the change in realization probability, not merely the headline.
