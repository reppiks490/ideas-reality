# Wave 2 Discoveries

This file extends the first research tranche with additional live sources, regulatory/event feeds, short-pressure data, and new composite hypotheses.

## New edge candidates

### E41 — Same-Day Off-Exchange Short Pressure
Source:
FINRA Daily Short Sale Volume files / Query API.

Availability:
FINRA states daily files are posted no later than 6:00 PM ET on the same trade date.

Mechanism:
Use short volume only as a state variable, not as a naive "high short volume = bearish" rule.

Candidate features:
- short-volume share residual vs symbol baseline
- short-exempt share
- same-day cross-sectional z-score
- short-volume acceleration
- divergence vs lit-exchange volume
- sector breadth of abnormal shorting

Best use:
next-day or multi-day state; combine with borrow/FTD/options/liquidity context.

Primary source:
https://www.finra.org/finra-data/browse-catalog/short-sale-volume-data/daily-short-sale-volume-files

### E42 — Consolidated Short Interest Crowding State
Source:
FINRA Consolidated Short Interest.

Mechanism:
Slow-moving crowding/positioning measure.

Features:
- SI acceleration
- days-to-cover change
- crowding percentile
- sector concentration
- SI vs realized borrow/FTD stress

Use:
positioning state, squeeze vulnerability, factor exposure.

Source:
https://developer.finra.org/catalog

### E43 — Fails-to-Deliver Stress State
Source:
SEC fails-to-deliver data.

Mechanism:
FTD is a stock of unsettled shares, not a daily flow. Treat spikes/persistence as settlement/borrow stress and market-friction state.

Features:
- FTD / float
- persistence
- age proxy only where safely inferable
- FTD acceleration
- FTD vs short-volume divergence
- FTD vs borrow-rate proxy when available

Caution:
Do not interpret FTD as proof of naked shorting or manipulation.

Source:
https://www.sec.gov/data/foiadocsfailsdatahtm

### E44 — Reg SHO Threshold Transition State
Mechanism:
Threshold-list entry/exit may indicate persistent settlement stress.

Features:
- first entry
- days on threshold list
- exit after persistence
- interaction with SI/short volume/FTD/options liquidity

Use:
event-state conditioning, not standalone directional alpha.

### E45 — Federal Register Public Inspection Edge
Status:
LIVE and public.

The Federal Register exposes Public Inspection documents before formal publication. Official docs say regular filings are routinely placed on public inspection around 8:45 AM ET, often for next-day Federal Register publication, and special filings may appear at other times.

Mechanism:
Machine-detect sector/company-relevant regulatory changes at the first lawful public-inspection availability timestamp, not the later publication date.

Potential targets:
healthcare, energy, autos, aerospace, agriculture, tariffs/trade, telecom, banks.

Hard requirement:
Use filed/public-inspection timestamp as the event time. Never pretend later publication was first availability.

Sources:
https://www.federalregister.gov/reader-aids/developer-resources/rest-api
https://www.federalregister.gov/reader-aids/using-federalregister-gov/understanding-public-inspection

### E46 — Regulatory Supply-Chain Shock Graph
Fuse:
Federal Register public-inspection docs + company supplier/customer graph + NAICS/product exposure.

Example:
new rule/tariff/airworthiness directive -> directly affected producer -> supplier/customer spillover -> sector/index effect.

Goal:
research second-order effects before they are obvious in headline tagging.

### E47 — Weekly Business Formation Pulse
Source:
U.S. Census BFS.

Current status:
Weekly estimates continue to be produced but are published as part of the monthly BFS release; weekly-by-industry data are also available historically and were updated in 2026.

Features:
- business application acceleration
- sector breadth
- state diffusion
- high-propensity business applications
- formation pipeline by industry

Use:
small-cap, labor, credit, local economy, sector nowcasts.

Source:
https://www.census.gov/econ/bfs/data/weekly.html
https://www.census.gov/econ/bfs/data/weeklynaics.html

### E48 — Real-Time Consumer Demand Mosaic
Source:
Opportunity Insights Economic Tracker.

Inputs:
credit/debit spending, employment, job postings, small-business revenue/openings.

Features:
- income-quartile spending divergence
- sector demand breadth
- geography diffusion
- high-income vs low-income consumption split
- goods vs services transition
- employment/spending disagreement

Use:
retail/consumer macro nowcasting before direct futures research.

Source:
https://github.com/OpportunityInsights/EconomicTracker

### E49 — Spending/Employment Reality Gap
Mechanism:
Compare real-time spending acceleration to employment/payroll acceleration.

States:
- spending leads hiring
- hiring leads spending
- both accelerate
- both contract
- decoupling

Potential use:
consumer discretionary, services, macro release surprise models.

### E50 — Short Pressure × Gamma Phase Interaction
Fuse:
FINRA same-day short volume + options gamma phase + underlying liquidity.

Hypothesis:
High shorting under positive-gamma/high-liquidity may be absorbed; high shorting under negative-gamma/poor-liquidity may propagate differently.

Test:
interaction must beat each component alone OOS.

### E51 — Settlement Stress Triangle
Fuse:
short volume + short interest + FTD.

Purpose:
separate transient intraday shorting from persistent crowded short exposure and actual settlement stress.

Output:
TRANSIENT / CROWDED / SETTLEMENT_STRESS / SQUEEZE_VULNERABLE.

### E52 — Public-Inspection Surprise-to-Price Latency
Research question:
How quickly do market prices react after a Federal Register document becomes publicly inspectable?

Method:
Event time = public-inspection filing time.
Measure sector/company reaction at 1m/5m/15m/1h/close/next day.

This can identify whether there is exploitable lag or merely immediate efficient repricing.

### E53 — Federal Rule Impact Embedding
Instead of generic NLP sentiment, extract:
- regulated entity type
- effective date
- compliance cost direction
- quantity restrictions
- tariff/tax/subsidy change
- affected product codes
- geography
- enforcement severity

Map directly to issuer exposure graph.

### E54 — Regulatory Calendar Revision Edge
Track rule lifecycle:
proposed rule -> comment period -> final rule -> effective date -> delay/withdrawal/correction.

Candidate:
probability of implementation and timing revisions may matter more than text sentiment.

### E55 — Off-Exchange Share Regime
Source:
FINRA ATS/non-ATS summary data.

Features:
- ATS share
- non-ATS share
- symbol-level weekly changes
- block activity
- dealer concentration where available

Use:
liquidity/crowding/market-structure state.

Source:
https://developer.finra.org/products/query-api

### E56 — Short Pressure Breadth Across Index Constituents
For NQ/ES:
aggregate abnormal short-volume/short-interest signals across constituents using index weights and sector buckets.

Question:
Does breadth of short pressure contain information not in index return/order flow?

### E57 — Regulatory-to-Commodity Transmission
Examples:
EPA/USDA/DOT/DOE rules affecting refinery specs, biofuels, agriculture, trucking, pipelines, aviation.

Build:
document -> physical constraint -> inventory/flow -> futures impact.

Require:
physical intermediate validation before return testing.

### E58 — Business Formation × Bank Credit Interaction
Fuse:
Census BFS + H.8 bank credit + rates.

Hypothesis:
Business applications only translate into economic impulse when financing conditions permit.

Potential use:
small-cap/growth cycle state.

### E59 — Consumer Spend × Port Imports Interaction
Fuse:
Opportunity Insights spending + Port of LA forward imports.

Research:
Does spending acceleration plus forward inbound inventory predict retail inventory/sales surprises better than either alone?

### E60 — Regulation Reality Gap
Compare:
market-implied expectation before public-inspection release vs measured actual rule severity after structured parsing.

Output:
underpriced / fair / overpriced regulatory shock.

## New source additions

D41 FINRA Daily Short Sale Volume — same-day by 6 PM ET.
D42 FINRA Consolidated Short Interest — slower crowding state.
D43 SEC Fails-to-Deliver — settlement stress history.
D44 Federal Register Public Inspection API — pre-publication public documents.
D45 Federal Register Documents API — published rules/notices.
D46 Census Business Formation Statistics — weekly/monthly high-frequency business applications.
D47 Opportunity Insights Economic Tracker — spending/employment/job postings/small-business.
D48 FINRA ATS/OTC summary datasets — market-structure state.

## Highest-priority Wave 2 tests

1. E45 Federal Register Public Inspection Edge
2. E41 Same-Day Off-Exchange Short Pressure
3. E51 Settlement Stress Triangle
4. E47 Weekly Business Formation Pulse
5. E48 Real-Time Consumer Demand Mosaic
6. E59 Consumer Spend × Port Imports Interaction

## Why E45 is special

This is not leaked/private information.
The Federal Register explicitly exposes public-inspection documents before publication and provides API endpoints for them.

That makes it a clean test of whether lawful public regulatory information diffuses into sector/company prices with measurable latency.
