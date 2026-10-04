# Wave 3 Discoveries

Wave 3 focuses on crypto capital-routing, physical natural-gas balance, nuclear/gas substitution, innovation disclosure, patent ownership, and export commitments.

All items remain hypotheses until independently falsified and promoted under RESEARCH_PROTOCOL.md.

## Crypto / cross-venue structural edges

### E61 — Stablecoin Liquidity Migration Field
Mechanism:
Stablecoins are transferable dollar-like collateral and settlement assets across crypto venues/chains. Net supply expansion, mint/burn, bridge migration and chain-level balance changes can reveal where deployable crypto liquidity is accumulating.

Candidate features:
- net stablecoin supply change
- mint minus burn
- chain inflow/outflow
- bridge-adjusted migration
- external stablecoin share vs native/algorithmic share
- stablecoin velocity
- aggregate expansion regime
- concentration by issuer

Important:
Do not use vendor wallet labels as ground truth unless independently reproducible. Separate actual issuance from exchange/internal wallet reshuffling.

Targets:
BTC/ETH first as liquidity-state variables; L1 cross-sectional returns only as separate research.

Evidence inspiration:
2026 practitioner research reported strong cross-sectional L1 results from stablecoin migration, but this is not sufficient evidence for ICARUS. Replicate independently.

Priority: A

### E62 — Stablecoin Expansion Regime
Mechanism:
A flow feature may only matter when total stablecoin supply is expanding materially.

State:
EXPANDING / FLAT / CONTRACTING

Research:
Does the predictive value of chain-level stablecoin flows depend on aggregate supply regime?

This is a conditioning feature, not a trade signal by itself.

Priority: A-

### E63 — Stablecoin Flight-to-Safety Velocity
Mechanism:
During crypto stress, stablecoin transfer velocity and migration can reflect demand for liquid dollar settlement.

Research:
Estimate chain-specific and venue-specific stablecoin velocity, then test whether it predicts persistence, deleveraging or recovery after crypto shocks.

Caution:
Transfer volume is highly contaminated by exchange/internal routing. Entity filtering must be timestamp-safe and reproducible.

Priority: B+

### E64 — CME Institutional Basis Pressure
Source:
CME publishes Bitcoin futures/options volume, open interest, settlements and official bulletins; CME also provides BasisWatch / implied-rate tools.

Candidate:
CME institutional pressure = futures basis × OI change × volume surprise × term-structure slope.

Question:
Does rising basis with rising CME OI represent new institutional long demand, while rising basis with falling OI reflects unwind/short-cover dynamics?

Targets:
BTC spot/futures, crypto volatility.

Primary:
https://www.cmegroup.com/market-data/volume-open-interest.html

Priority: A

### E65 — CME vs Offshore Leverage Dispersion
Fuse:
CME dated-futures basis/OI with offshore perpetual funding/OI.

States:
- CME premium + neutral offshore
- offshore leverage excess
- institutional/offshore disagreement
- synchronized leverage expansion
- synchronized deleveraging

Hypothesis:
Venue disagreement may identify fragile rallies, squeeze risk or institutional accumulation.

Priority: A

### E66 — ETF–CME–Spot Causal Graph
Fuse:
spot Bitcoin ETF holdings/shares/flows where reproducible + CME futures/OI/basis + regulated spot venue prices + offshore perp state.

Goal:
infer which venue is leading price discovery by regime.

Do not assume ETF flow causes same-day returns. Test lead/lag and common-news confounding.

Priority: A

### E67 — ETF Creation/Redemption Absorption State
Mechanism:
Spot ETF primary-market activity may generate underlying Bitcoin acquisition/sale demand. Estimate expected primary-market flow and compare with available crypto spot liquidity.

Candidate:
ETF_pressure / spot_absorption_capacity

Analogous to E03 mechanical pressure / adaptive liquidity.

Source caution:
Use issuer/SEC primary data where possible. Do not rely on scraped flow tables as the sole historical record.

Priority: A-

### E68 — Bitcoin Volatility Surface State
CME launched dedicated Bitcoin Volatility futures in 2026 and maintains crypto options markets.

Research:
Combine regulated BTC options skew/term structure with spot/futures liquidity.

Features:
- front/back implied-vol spread
- skew
- wing steepness
- realized vs implied
- volatility-of-vol
- basis × vol interaction

Goal:
state conditioning for BTC strategies, not another generic volatility indicator.

Priority: A-

### E69 — Crypto Collateral Stress Triangle
Fuse:
stablecoin contraction + offshore funding stress + CME basis compression.

Hypothesis:
When all three agree, deleveraging risk is stronger than any single measure.

Add:
liquidation data only where source methodology and timestamp can be verified.

Priority: A

### E70 — BTC Institutionalization Regime
Research:
Estimate the fraction of activity represented by CME/ETF channels versus offshore/on-chain channels.

Question:
Do historically successful on-chain signals decay as price discovery migrates toward regulated ETF/futures infrastructure?

Purpose:
prevent using old-cycle crypto signals after market structure changes.

Priority: A

## Natural gas / physical energy edges

### E71 — Natural Gas Physical Balance Nowcast
Fuse:
weather-normalized demand + dry-gas production + storage + LNG export pull + pipeline constraints + power-sector gas burn + imports/exports.

Goal:
forecast physical balance before scheduled storage information.

Research sequence:
physical variables -> implied storage change -> EIA storage surprise -> futures reaction.

Do not jump directly from weather to price.

Priority: S

### E72 — Storage Surprise Engine
Mechanism:
Build a bottom-up estimate of weekly storage injection/withdrawal from observed physical balance.

Output:
expected EIA storage surprise distribution.

Research:
1. forecast storage print
2. compare with survey expectation
3. only then test if residual surprise predicts/conditions futures reaction.

Priority: S

### E73 — Nuclear-to-Gas Substitution Pulse
Source:
NRC publishes daily U.S. power reactor status; data are collected each day, with unit power percentages and outage reasons.

Mechanism:
Unexpected nuclear generation loss can increase marginal thermal generation needs, including natural gas, depending on region/load/weather.

Candidate:
lost_nuclear_MW × regional_heat_rate × load_stress × gas_pipeline_constraint

Targets:
regional power first, Henry Hub second.

Priority: A

### E74 — Nuclear Outage Surprise
Separate planned refueling/coastdown from forced trip/scram/unplanned reduction.

Hypothesis:
Unplanned outage MW under tight load/weather conditions carries more gas-demand information than total nuclear outage MW.

Priority: A

### E75 — Pipeline Constraint Graph
Sources:
public pipeline operational postings/critical notices where available, plus FERC filings/eLibrary.

Graph:
pipeline segment -> receipt/delivery zones -> LNG terminals/storage/power markets -> basis hubs.

Feature:
capacity impairment weighted by downstream dependency.

Research target:
regional basis first; Henry Hub only if transmission exists.

Priority: A

### E76 — FERC Gas Infrastructure Event Feed
Source:
FERC eLibrary provides public filing/posting timestamps for gas infrastructure notices, approvals and project filings.

Events:
capacity expansions, temporary workspace/maintenance-related filings, blanket authorizations, LNG/pipeline regulatory steps.

Use:
slow-to-medium horizon physical capacity/event graph.

Do not confuse regulatory filing with actual operational flow.

Priority: B

### E77 — LNG Export Pull State
Mechanism:
U.S. LNG exports convert global gas demand into Gulf Coast feedgas demand.

Fuse:
terminal availability + feedgas/exports + vessel schedule/arrivals where lawful/available + global LNG price spread + pipeline constraints.

Output:
incremental Gulf gas demand.

Priority: A

### E78 — LNG Terminal Outage Shock
Feature:
unexpected terminal capacity loss × expected utilization × regional gas balance tightness.

Potential direction:
reduced feedgas can loosen U.S. gas supply even while being globally bullish for LNG.

This opposite-sign mechanism is exactly why physical modeling matters.

Priority: A

### E79 — Grid-to-Gas Residual Demand
Fuse:
load forecast error + renewable output error + nuclear outage + coal availability.

Output:
residual thermal generation requirement attributable to gas.

Research:
regional gas burn / power prices first.

Priority: A

### E80 — Gas Weather Surprise Tensor
Instead of raw HDD/CDD:
forecast revision × population/gas-heating exposure × power-region exposure × pipeline tightness × storage regime.

Candidate:
weighted weather demand surprise, separated into residential/commercial and power burn.

Priority: A

## Innovation / public intellectual-property edges

### E81 — Innovation Disclosure Ladder
Information stages:
scientific publication -> patent pre-grant publication -> patent grant -> assignment/licensing -> commercialization/filing.

Research:
Measure incremental information at each stage rather than treating patent grant as the first public event.

Evidence motivation:
2025 research on pharmaceutical firms found meaningful market reactions at scientific-publication and pre-grant patent-publication stages.

Priority: B+

### E82 — Science-to-Patent Diffusion Graph
Map:
scientific authors -> inventors -> assignee/company -> product/technology -> supplier/competitor.

Question:
Can public scientific disclosure reveal valuable company-relevant technology before formal patent publication or corporate messaging?

Strict:
Only public publication timestamps; no use of application filing dates before public disclosure.

Priority: B

### E83 — Patent Novelty Surprise
At pre-grant publication:
estimate novelty relative to historical claims/text and technology class.

Features:
- semantic novelty
- claim breadth proxy
- inventor novelty
- assignee technology-distance
- science linkage
- early citation/reuse later only for retrospective validation, never as contemporaneous input

Priority: B

### E84 — Patent Assignment / IP Ownership Shock
Source:
USPTO Open Data Portal exposes patent assignment data; some assignment endpoints are refreshed daily.

Events:
assignment, security interest, merger/name change, transfer.

Research:
Identify economically meaningful ownership transfers after separating administrative/legal noise.

Potential use:
M&A/licensing/collateral/strategic-IP state.

Priority: B-

### E85 — Innovation Pipeline Acceleration
Measure per company/sector:
scientific publications -> pre-grant publications -> grants -> assignments.

Goal:
slow-horizon innovation-state feature for semiconductors, biotech, industrial tech.

Do not claim short-horizon alpha without evidence.

Priority: B

## Agriculture/export-flow edges

### E86 — Export Commitment Surprise
Source:
USDA Foreign Agricultural Service weekly Export Sales.

Features:
- new sales surprise
- cancellations
- outstanding sales
- cumulative exports
- destination concentration
- pace vs USDA official projection
- marketing-year seasonality

Targets:
corn, soybeans, wheat, cotton, beef/pork where liquid proxies exist.

Priority: A

### E87 — Export Sales × River Constraint Interaction
Fuse:
USDA export commitments with USACE/USGS river logistics.

Hypothesis:
Strong export demand under constrained inland logistics widens basis/freight stress and may alter futures response.

Priority: A

### E88 — Commitment-to-Shipment Conversion Risk
Track:
outstanding commitments -> actual exports.

Feature:
conversion slowdown or acceleration by destination/commodity.

Mechanism:
A large sales book that cannot physically ship is different from realized demand.

Priority: A-

## Cross-domain higher-order edges

### E89 — Institutional vs Physical Reality Divergence
Compare:
financial-market expectation (options/futures/prediction markets)
against
physical-system nowcast (ports/grid/gas/exports).

Hypothesis:
largest opportunities may occur when market pricing and physical reality disagree materially.

Priority: S

### E90 — Information Channel Rotation Detector
For each market, estimate which channel currently leads:
price/order flow
options/dealer hedging
institutional transaction flow
physical telemetry
public regulatory/corporate events

Use:
dynamic routing of research/model weight by information regime.

Priority: S

## Wave 3 source additions

D49 CME Volume & Open Interest Reports — official futures/options OI/volume.
D50 CME Cryptocurrency Daily Bulletin / settlements — regulated BTC futures/options state.
D51 iShares IBIT issuer page/filings — primary ETF shares/holdings information; archive vintages.
D52 NRC Daily Power Reactor Status — daily reactor output/outage state.
D53 FERC eLibrary — public gas infrastructure filings with filed/posted timestamps.
D54 USPTO Open Data Portal / PatentsView bulk data — patents/pre-grant publications; API migration ongoing in 2026.
D55 USPTO Patent Assignment API — assignment information, some data refreshed daily; API key/account may be required.
D56 USDA FAS Weekly Export Sales — weekly commitments/exports.
D57 Public-chain stablecoin contract data — source must be contract-level and reproducible.
D58 CME BasisWatch / Implied Rate tools — institutional crypto basis visualization; verify historical exportability before production use.
D59 Pipeline operational postings / EBBs — access and terms differ by operator; connector design TBD per pipeline.
D60 EIA natural-gas datasets — production/storage/consumption/LNG and related official physical data; cadence varies by series.

## Highest-priority Wave 3 tests

1. E71 Natural Gas Physical Balance Nowcast
2. E72 Storage Surprise Engine
3. E73 Nuclear-to-Gas Substitution Pulse
4. E64 CME Institutional Basis Pressure
5. E65 CME vs Offshore Leverage Dispersion
6. E66 ETF–CME–Spot Causal Graph
7. E61 Stablecoin Liquidity Migration Field
8. E81 Innovation Disclosure Ladder
9. E86 Export Commitment Surprise
10. E89 Institutional vs Physical Reality Divergence

## Strongest unifying principle from Wave 3

Do not ask only "what predicts price?"

Ask:
1. Where is capital moving?
2. Where is physical demand/supply moving?
3. Where is information first becoming public?
4. What mechanism converts that state into forced or likely market activity?
5. How much adaptive liquidity exists to absorb it?
