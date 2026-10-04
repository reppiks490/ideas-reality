# Wave 4 Discoveries

Wave 4 targets official balance-sheet operations, funding/collateral plumbing, government procurement, ownership/capital-supply events, and public regulatory infrastructure.

All items are hypotheses until falsified and promoted under RESEARCH_PROTOCOL.md.

## E81 — Treasury Buyback Pressure Surface

Source:
U.S. Treasury / FiscalData Treasury Securities Buybacks.

Status:
LIVE.

Official facts:
- Treasury publishes tentative buyback schedules around quarterly refunding.
- Operations have explicit start, close, and settlement times.
- FiscalData exposes operation data through an API.
- Final eligible securities are announced on operation day.
- Results include offered/accepted par and accepted pricing by security.

Mechanism:
Buybacks mechanically remove off-the-run nominal coupons/TIPS from private hands and can alter local liquidity, dealer inventory, and relative-value pressure.

Features:
- scheduled max redemption / eligible float
- accepted / offered ratio
- security-level acceptance concentration
- weighted-average accepted-price concession
- maturity-bucket intensity
- liquidity-support vs cash-management type
- operation surprise vs tentative schedule
- settlement-day liquidity interaction

Primary:
https://treasurydirect.gov/auctions/announcements-data-results/buy-backs/
https://fiscaldata.treasury.gov/datasets/treasury-securities-buybacks/

Priority: S

## E82 — SOMA Securities Lending Specialness Map

Source:
Federal Reserve Bank of New York Securities Lending Operations.

Status:
LIVE.

Official mechanics:
- business-day auctions generally at noon ET
- public result summaries follow the operation
- results include propositions received, accepted, and weighted-average rate per issue

Mechanism:
Demand to borrow a Treasury issue from SOMA is a direct scarcity/specialness signal.

Features:
- propositions / theoretical available
- accepted / received
- lending-rate surprise
- issue scarcity persistence
- maturity-bucket scarcity breadth
- scarcity vs dealer fails / repo / TRACE

Primary:
https://www.newyorkfed.org/markets/desk-operations/securities-lending

Priority: S

## E83 — Standing Repo / ON RRP Funding Pressure State

Source:
New York Fed repo/reverse-repo operations.

Status:
LIVE.

Mechanism:
SRF take-up can reveal demand for cash against collateral at the Fed backstop; ON RRP take-up reflects cash parked at the floor facility.

Research controls:
quarter/month end, tax dates, Treasury settlement, reserve level, bill supply, money-market assets, policy corridor.

Features:
- SRF take-up surprise
- ON RRP take-up surprise
- take-up / reserves
- take-up / settlement size
- private-repo vs facility-rate basis
- lagged counterparty-type mix where public

Priority: S-

## E84 — GCF Repo Dealer Funding Basis

Source:
DTCC GCF Repo Index.

Status:
LIVE.

Official data:
daily par-weighted overnight GCF repo rates and par values for Treasury and agency-MBS collateral. DTCC documentation states daily publication around 3:30 PM ET.

Features:
- GCF Treasury - SOFR
- GCF Treasury - IORB
- GCF volume surprise
- Treasury-vs-MBS GCF basis
- quarter-end basis
- basis × dealer inventory

Primary:
https://www.dtcc.com/charts/dtcc-gcf-repo-index

Priority: A+

## E85 — Treasury Scarcity Spectrum

Fuse:
SOMA securities lending + primary-dealer fails + GCF/SOFR + TRACE flow + auction/buyback calendar.

Output:
ABUNDANT / NORMAL / SCARCE / DISLOCATED by issue and maturity bucket.

Use:
condition rates/Treasury signals before any equity spillover research.

Priority: S

## E86 — Federal Procurement Demand Pipeline

Source:
SAM.gov Contract Opportunities Public API.

Status:
LIVE; API key required.

Opportunity types include:
sources sought, pre-solicitation, solicitation, combined synopsis/solicitation, sole-source/special notices, award notices and amendments.

Mechanism:
Procurement begins before an award. Public opportunity transitions provide a forward view of potential government demand.

Features:
- opportunity acceleration by NAICS/PSC/agency
- amendment velocity
- response-deadline revisions
- sole-source status
- procurement stage transition
- mission/geographic concentration
- incumbent/exposure match

Important:
Sources-sought != solicitation != award.

Primary:
https://open.gsa.gov/api/get-opportunities-public-api/

Priority: S-

## E87 — Contract Award Surprise Graph

Sources:
USAspending + SAM.gov + issuer/entity graph.

Status:
LIVE with reporting-lag caveats.

Key rule:
Use first-public availability, never contract action date as information availability.

Candidate:
award_materiality = unexpected_obligation / issuer_revenue_or_market_cap

Condition on:
- prior solicitation probability
- incumbent status
- award modification vs new award
- obligated amount vs ceiling
- revenue recognition horizon
- contract type/margin class

Priority: A+

## E88 — Procurement Amendment Information Velocity

Mechanism:
The revision path of a procurement may contain more information than the first posting.

Track:
- statement-of-work changes
- deadline extensions
- eligibility/set-aside changes
- Q&A density
- scorecard revisions
- scope/ceiling changes where disclosed
- award-date slippage

Output:
probability and expected-value revision.

Priority: A

## E89 — Schedule 13D/13G Ownership Shock

Source:
SEC EDGAR.

Status:
LIVE via filing dissemination.

Features:
- first threshold crossing
- ownership delta
- 13D vs 13G
- amendment direction
- filer identity/history
- purpose-of-transaction extraction
- issuer float/liquidity interaction

Hard timing:
EDGAR acceptance/public dissemination time.

Priority: A

## E90 — Discretionary Insider Signal with 10b5-1 Separation

Source:
SEC Forms 3/4/5 XML.

Status:
LIVE filings; quarterly flattened research datasets also available.

Useful SEC field:
AFF10B5ONE identifies Rule 10b5-1 attribution where reported.

Research:
separate planned from discretionary trades.

Features:
- discretionary purchase materiality
- clustered insider breadth
- officer/director role
- ownership delta
- transaction price vs market
- first/repeat purchase
- derivative vs non-derivative
- 10b5-1 flag

Priority: A

## E91 — Equity Supply Runway / Dilution Capacity

Sources:
SEC S-3/F-3, EFFECT, 424B, 8-K, 10-Q/10-K.

Mechanism:
Compute legally available and economically plausible new-share supply rather than infer dilution from price action.

State:
- effective shelf capacity
- ATM authorization/capacity
- recent issuance velocity
- float-relative capacity
- offering discount
- cash-runway need
- shelf age/expiry

Caution:
An effective shelf is optional capacity, not proof of current selling.

Priority: S- for equities

## E92 — Capital Supply × Short Crowding Interaction

Fuse:
E91 supply runway + FINRA short-pressure/crowding + FTD + options/liquidity state.

Question:
Does squeeze probability/persistence change when an issuer has large effective unused equity-supply capacity?

Priority: A+

## E93 — Fed Outright Operation Pressure

Source:
New York Fed Treasury outright schedules/results.

Status:
LIVE.

Mechanism:
Reinvestment and reserve-management purchases create scheduled mechanical demand.

Features:
- operation amount / eligible float
- maturity bucket
- purchase concentration
- accepted distribution vs expected
- interaction with issuance and Treasury buybacks

Priority: A

## E94 — Official Operation Collision Calendar

Fuse scheduled:
Treasury auctions, Treasury buybacks, Fed outright purchases, major settlements, tax dates/TGA flows, SOMA lending.

Output:
expected cash/collateral pressure by day and maturity.

Question:
Do coincident mechanical flows create nonlinear liquidity effects?

Priority: S

## E95 — FERC Gas/LNG Regulatory Event Graph

Source:
FERC eLibrary.

Status:
LIVE public filing system.

Useful metadata:
filed, posted and first-received times; docket; class/type; gas-related categories.

Lifecycle:
application -> notice -> intervention -> environmental review -> certificate/order -> amendment/vacatur.

Targets:
operator/project and regional gas basis first.

Priority: A

## E96 — Pipeline Incident Ground-Truth Layer

Source:
PHMSA.

Status:
DELAYED for trading; valuable for history/labels.

Operators generally have up to 30 days to submit written incident reports.

Use:
severity ground truth and event-study labeling, not low-latency first alert.

Priority: B as source, A as validation layer

## E97 — CFTC Positioning Regime

Source:
CFTC Commitments of Traders / Socrata.

Status:
LIVE weekly with reporting lag.

Use:
slow positioning/crowding state.

Features:
producer/merchant, swap dealer, managed money, other reportables, normalized net position, weekly acceleration, long-history percentile.

Priority: A-

## E98 — CME Open-Interest Migration State

Source:
CME official market-statistics data; latency/licensing depends on product.

Features:
- front/deferred OI migration
- futures/options OI ratio
- OI change conditional on price
- strike OI concentration where licensed
- roll anomaly
- block-volume share

Priority: A

## E99 — Opportunity-to-Award Conversion Model

Train lifecycle transitions using SAM.gov + USAspending.

Output probabilities:
NO_AWARD / INCUMBENT / NEW_WINNER / DELAYED / CANCELLED / MATERIAL_MODIFICATION.

Award "surprise" is measured against ex-ante conversion probability.

Priority: A+

## E100 — Public Balance-Sheet Mechanics Graph

Nodes:
Treasury, Fed, primary dealers, banks, money funds, FICC, rates/futures.

Edges:
issuance, buybacks, repo, reverse repo, SOMA lending, outright purchases, tax/spending flows, settlement.

Goal:
replace generic "liquidity" narratives with explicit cash/collateral transfers.

Priority: S

## Highest-priority Wave 4 tests

1. E81 Treasury Buyback Pressure Surface
2. E82 SOMA Securities Lending Specialness Map
3. E85 Treasury Scarcity Spectrum
4. E86 Federal Procurement Demand Pipeline
5. E87 Contract Award Surprise Graph
6. E90 Discretionary Insider Signal
7. E91 Equity Supply Runway
8. E94 Official Operation Collision Calendar
9. E95 FERC Gas/LNG Regulatory Event Graph
10. E100 Public Balance-Sheet Mechanics Graph
