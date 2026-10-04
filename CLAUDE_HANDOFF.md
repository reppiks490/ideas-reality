# Claude Handoff

## Mission

Treat this repository as an external research inbox.

Do not assume any candidate is valid because it appears here. The objective is to give Claude high-quality hypotheses and source maps that can be independently accepted, modified or rejected.

## Top research queue

1. E03 Mechanical Hedge Pressure / Absorption Capacity
2. E04 Treasury Auction Absorption Tensor
3. E05 TRACE Treasury Flow State
4. E06 Fiscal Liquidity Impulse
5. E08 Liquidity Replenishment / Resilience Field
6. E11 Port of Los Angeles Forward Cargo Field
7. E13 Mississippi Physical Logistics Graph
8. E15 NASA Black Marble Industrial Pulse
9. E20 Korea Semiconductor Export Pulse
10. E26 EDGAR Information Diffusion Graph

## Why these first

They span independent information channels:
- derivatives mechanics
- Treasury supply/demand
- government liquidity
- order-book adaptation
- forward physical trade
- inland logistics
- satellite physical observations
- semiconductor export demand
- corporate disclosures

This is preferable to testing ten variants of price momentum.

## Important current-source facts

- FINRA SLATE is a future watchlist item. FINRA says its launch is extended to September 28, 2028.
- FINRA currently provides next-day public transaction-level data for on-the-run nominal Treasury coupons and daily aggregate Treasury statistics.
- SEC EDGAR submissions APIs update throughout the day in real time; SEC documents typical processing delays under a second for submissions metadata and under a minute for XBRL, though peak times may be slower.
- Port of Los Angeles provides forward cargo visibility.
- USACE lock queue/status data can update on roughly 15-minute cadence.
- USGS offers real-time streamflow/gage data.
- NASA Black Marble offers near-real-time nighttime-light products within hours.
- Cloudflare Radar exposes outage/anomaly data and traffic time series with fine aggregation for suitable windows.
- OpenFEMA exposes some declaration datasets with roughly 20-minute update frequency.
- Indeed Hiring Lab exposes daily job-posting observations refreshed weekly.
- Korea Customs publishes preliminary partial-month trade releases including semiconductor detail.

## Implementation-neutral data contract

Every connector should preserve:
source_id
raw_payload_hash
event_time
published_time
ingested_time
revision_id/vintage
source_timezone
availability_confidence
schema_version

No feature may be generated from a value whose published_time exceeds the decision timestamp.

## The most important architectural idea

Research the ratio:

EXOGENOUS PRESSURE / ADAPTIVE LIQUIDITY

Examples:
- dealer hedge demand / ES book replenishment
- Treasury auction supply shock / dealer balance-sheet capacity
- ETF close flow / constituent close liquidity
- liquidation flow / cross-venue available depth

This gives a common framework for several otherwise unrelated "edges."

## Second most important idea

Build a Physical Economy Nervous System before attempting direct trading.

Prove:
sensor -> real-world KPI
then:
sensor -> expectation change
then:
sensor -> return

This prevents alternative-data overfitting.

## Statistical guardrail

Because the research process is continuous, investigate online multiple-testing / e-value methods rather than treating every repeated p-value as independent.

Candidate literature to inspect:
- online e-BH / e-values
- e-LOND
- e-GAI / e-LORD / e-SAFFRON
- LORD / SAFFRON under appropriate assumptions
- Model Confidence Set
- Superior Predictive Ability
- conformal prediction under change points
- invariant/environmental validation

## Explicit non-goals

- do not implement every item
- do not maximize model count
- do not claim profitability from in-sample statistics
- do not use latest revised values as historical first-release data
- do not turn physical telemetry into a direct trading rule without intermediate validation
- do not touch ICARUS merely because this repo changed

## Success definition

This repo succeeds if it gives Claude a steady supply of:
1. orthogonal hypotheses,
2. primary-source data,
3. exact falsification conditions,
4. methods that make false discoveries harder,
5. ideas that can improve existing ICARUS signals by conditioning them on causal state.
