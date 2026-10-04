# Wave 6 Discoveries

Wave 6 explores digital adoption telemetry, open-source ecosystems, AI-model demand, gaming engagement, government commodity intervention, credit-market price discovery, municipal local-economy signals, livestock throughput, and natural-gas physical balances.

All entries are hypotheses, not proven edges.

## E123 — Public Developer Adoption Pulse

Sources:
GitHub public repository APIs/events and repository statistics.

Status:
LIVE but endpoint-specific.

Official GitHub facts:
- public repo events are accessible, but event endpoints are not guaranteed real-time and GitHub documents latency from seconds to hours
- public event history is limited
- repository statistics expose weekly commit/participation data
- traffic/clones/views endpoints require write access to the repository and therefore cannot be used as a general public-company external signal

Use only public external metrics:
stars, forks, releases, issues, pull requests, contributors, commits, repository events.

Mechanism:
For developer-facing firms/products, open-source adoption and contribution can lead commercial usage, hiring and ecosystem lock-in.

Feature family:
- star/fork velocity
- unique contributor acceleration
- issue creation/closure rate
- PR merge rate
- release cadence
- release-to-adoption lag
- external-contributor share
- dependency ecosystem breadth

Priority: A

## E124 — Package Download Adoption Field

Primary:
PyPI public BigQuery download dataset.

Status:
LIVE-ish public dataset; query economics and data quality matter.

Official packaging docs state Linehaul streams PyPI download logs to the public BigQuery table with timestamped file/project/version and environment metadata.

Features:
- package download velocity
- unique environment proxy
- version migration speed
- release adoption half-life
- ecosystem share vs competitors
- dependency-family breadth
- geography/platform mix where compliant and available

Caveat:
downloads include CI, mirrors and automated systems. Raw count is not equal to human users or revenue.

Priority: A+

## E125 — AI Model Ecosystem Adoption Pulse

Source:
Hugging Face Hub API.

Status:
LIVE public metadata subject to rate limits.

Official API exposes model/dataset metadata including downloads, all-time downloads, likes, last-modified and trending score; Hub also supports webhooks for repo changes.

Features:
- download acceleration
- model-family share
- new derivative/fine-tune count
- provider availability breadth
- likes/download ratio
- release-to-fork/derivative propagation
- task/category migration

Use:
AI ecosystem/company/product adoption research, especially for public firms with identifiable open models.

Do not equate model downloads directly with paid inference revenue.

Priority: A+

## E126 — Open-Source Commercialization Gap

Mechanism:
Open-source popularity and commercial performance need not move together.

Construct:
commercialization_gap =
developer adoption growth
minus
public commercial KPI / paid-usage proxy growth.

Hypotheses:
- adoption leads monetization
- rapid adoption without monetization signals margin/cost pressure
- commercial growth without ecosystem growth signals weaker moat

Targets:
developer-platform/cloud/software firms.

Priority: A

## E127 — Release Diffusion Velocity

Fuse:
GitHub release/tag
+ PyPI/npm package publication
+ Hugging Face model update
+ downstream project/version adoption.

Output:
time required for a release to diffuse through the ecosystem.

Research question:
Does unusually fast/slow diffusion nowcast product success, developer retention, vulnerability remediation or future revenue commentary?

Priority: A

## E128 — Dependency Graph Demand Share

Construct a graph:
package/library/model
-> downstream dependent repositories/packages
-> corporate products/issuers.

Measure:
- dependency additions/removals
- competing-library substitution
- transitive dependency centrality
- ecosystem concentration
- version lock-in

Potentially more meaningful than raw downloads.

Priority: A

## E129 — Cyber Vulnerability × Dependency Exposure

Fuse:
CISA KEV
+ package/dependency graph
+ company technology exposure.

Question:
Does a newly exploited vulnerability create heterogeneous economic risk based on actual dependency exposure rather than vendor-name matching?

No exploit procedure is needed.

Priority: A

## E130 — Gaming Engagement Nowcast

Source:
Steamworks current-player API and public Steam product/review metadata where terms permit.

Official Steamworks endpoint exposes the number of currently active connected players for an app.

Build historical archive prospectively:
- current player snapshots
- peak/median/daypart
- review count/velocity
- price/promotional calendar
- release/DLC events

Targets:
public game publishers with material title exposure.

Priority: A

## E131 — Game Engagement-to-Revenue Translation

Mechanism differs by business model.

Segment:
premium one-time purchase
free-to-play live service
subscription
DLC-heavy
microtransaction-heavy.

Research:
Does concurrent-player retention, review velocity and release-event response improve revenue/booking estimates after controlling for pricing and title age?

Priority: A

## E132 — Strategic Petroleum Reserve Mechanical Flow

Sources:
DOE SPR solicitations/contracts + EIA/DOE inventory.

Status:
LIVE/event-driven + weekly inventory.

Mechanism:
Government purchases, sales and exchanges are known or partially known physical crude demand/supply.

Features:
- announced barrels
- delivery window
- crude quality
- site/location
- solicitation-to-award revision
- awarded quantity
- delivery schedule
- exchange return obligation
- barrels/day relative to regional flow

Do not use headline total alone; timing and delivery profile determine market pressure.

Priority: S-

## E133 — SPR Solicitation/Award Revision Edge

State machine:
policy announcement
-> solicitation
-> offer deadline
-> award
-> delivery nominations
-> actual receipt/inventory.

Surprise:
actual award/delivery profile minus pre-solicitation market expectation.

This separates political headline volume from realizable physical flow.

Priority: A+

## E134 — Government Commodity Intervention Collision

Generalize E132 beyond crude when official programs apply.

Research calendars where public-sector:
purchase,
sale,
release,
loan,
stockpile,
auction
interact with futures/physical markets.

Only include interventions with explicit mechanical commodity flows.

Priority: B+

## E135 — TRACE Corporate Credit Pulse

Source:
FINRA TRACE.

Status:
LIVE public trade information for eligible corporate/agency bonds and several securitized products.

FINRA states:
- execution time, quantity, price and yield are disseminated for eligible fixed income
- corporate/agency trades must generally be reported within 15 minutes
- FINRA notes most are available much faster
- large trade sizes are capped in public display

Candidate features:
- issuer bond return before equity
- yield-spread shock
- trade intensity
- size-capped block frequency
- cross-bond breadth by issuer
- sector credit breadth
- HY vs IG stress
- bond-equity disagreement

Priority: S

## E136 — Bond-Equity Information Leadership State

Question:
For a given issuer/state, which market currently leads:
equity
corporate bond
CDS if licensed
options
ETF?

Output:
credit_leads / equity_leads / synchronized / fragmented.

Trade/research only lagged, causally available cross-market signals.

Priority: S-

## E137 — Credit Breadth Before Equity Index

Construct cross-sectional credit deterioration/improvement:
percentage of index constituents with abnormal TRACE yield/price deterioration, weighted by market cap and debt liquidity.

Hypothesis:
broad issuer-level credit stress may contain information about equity-index risk before index price fully reflects it.

Targets:
ES/NQ only after issuer-level mechanism is proven.

Priority: A+

## E138 — Securitized Funding Pulse

FINRA also provides TRACE transparency for several securitized products.

Research:
TBA/MBS/ABS/CMO trade state as signals of mortgage/consumer/funding conditions.

Do not combine disparate products without duration/prepayment/credit controls.

Priority: B+

## E139 — Municipal Local-Economy Risk Surface

Source:
MSRB municipal transaction/disclosure data, plus Treasury curve and local issuer mapping.

Status:
access/licensing varies by product; TERMS_REVIEW.

Empirical literature indicates municipal spreads/curve shape contain information about local economic conditions and risk of locally exposed firms.

Research state:
state/metro municipal spread residual after:
Treasury rates,
tax policy,
credit rating,
duration,
liquidity.

Output:
local fiscal/economic risk factor.

Priority: A

## E140 — Regional Equity × Municipal Stress

Map public companies to:
headquarters,
facilities,
revenue,
labor force,
customers
by state/metro.

Question:
Does local muni stress matter most for genuinely localized firms rather than nominal headquarters?

Priority: A

## E141 — Daily Livestock Throughput Pulse

Source:
USDA AMS Daily Livestock and Poultry Slaughter.

Status:
LIVE daily estimates with subsequent revisions/actuals.

Official reports contain:
daily/WTD/YTD cattle, hog, sheep, calf and poultry slaughter, plus comparisons with prior week/year; related reports include weights and meat production.

Mechanism:
slaughter throughput is a direct physical processing measure.

Research uses:
- livestock supply/demand imbalance
- packer utilization
- meat production nowcast
- feed-demand linkage
- holiday/weather/plant-disruption effects

Targets:
cattle/hog futures and protein-related equities before broader agriculture.

Priority: A+

## E142 — Slaughter × Weight × Cash Basis Field

Raw headcount misses production.

Fuse:
slaughter head
× live/dressed weight
× cutout/cash prices
× futures
× feed costs.

Output:
physical protein production surprise and margin pressure.

Priority: A+

## E143 — Natural Gas Balance Residual Engine

Sources:
EIA storage, production, imports/exports, LNG, power-sector/grid data and other official balance components.

Mechanism:
Reconcile:
beginning storage
+ production
+ imports
- exports
- power burn
- industrial/residential/commercial demand
= ending storage.

Residual is both:
- a latent-demand/supply candidate
- a data-quality diagnostic.

Priority: S

## E144 — LNG / Pipeline Constraint Transmission

Build explicit flow graph:
basin production
-> pipeline takeaway
-> storage
-> LNG feedgas/export
-> power demand
-> regional basis
-> Henry Hub.

Research:
constraint activation and release, not generic LNG headlines.

Priority: S-

## E145 — Digital Adoption Truth Ladder

For software/AI/game products, rank observations by distance from economic reality:

L0 social attention
L1 repo stars/likes
L2 downloads
L3 active usage/concurrent players
L4 dependency adoption
L5 paid/enterprise usage proxy
L6 reported revenue/bookings

Research edges where a lower-lag layer reliably predicts a higher-truth layer.

Priority: S research architecture

## E146 — Adoption Surprise Relative to Release

Many digital metrics are strongly driven by release calendars.

Candidate:
adoption_surprise =
observed post-release usage
-
expected usage from historical release type, project age, day-of-week, launch size and marketing.

Use residual, not raw launch spike.

Priority: A+

## Strongest Wave 6 tests

1. E135 TRACE Corporate Credit Pulse
2. E136 Bond-Equity Leadership State
3. E143 Natural Gas Balance Residual
4. E132 SPR Mechanical Flow
5. E124 Package Download Adoption
6. E125 AI Model Ecosystem Adoption
7. E128 Dependency Graph Demand Share
8. E141 Daily Livestock Throughput
9. E139 Municipal Local-Economy Risk
10. E145 Digital Adoption Truth Ladder
