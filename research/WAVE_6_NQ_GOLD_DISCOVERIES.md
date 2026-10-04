# Wave 6N — NQ, Gold, Credit, Procurement, Sanctions, Gulf Energy

This wave uses canonical IDs directly. Every item is a falsifiable research candidate, not a claim of alpha.

## NQ / semiconductor physical-fundamental research

### W6N-E01 — Taiwan Monthly Revenue Semiconductor Pulse
Source:
Taiwan MOPS/TWSE/TPEx monthly operating-revenue disclosures.

Mechanism:
Taiwan-listed foundries, packaging/test firms, server ODMs, PCB/substrate suppliers, networking firms, memory/component producers and electronics manufacturers disclose operating revenue monthly. This creates a higher-frequency fundamental layer than U.S. quarterly reporting.

Build:
- weighted YoY/MoM acceleration
- positive-surprise breadth
- foundry vs ODM divergence
- AI-server vs consumer-electronics divergence
- packaging/test vs front-end divergence
- revenue concentration and dispersion

Research order:
Taiwan signal -> U.S. semiconductor/company revenue surprise -> sector -> NQ.

Point-in-time warning:
reporting month is NOT availability time. Preserve actual company disclosure/publication time.

Priority: S

### W6N-E02 — AI Hardware Supply-Chain Revenue Graph
Map Taiwan/Korea physical revenue/export nodes to:
NVIDIA, AMD, Broadcom, Apple, hyperscalers, networking, server and storage demand.

Every supplier/customer edge requires a source, confidence, estimated materiality, effective_from and effective_to.

Output:
expected revenue impulse by U.S. company and sector.

Priority: S

### W6N-E03 — Semiconductor Revenue Diffusion Order
Question:
Which supply-chain layer turns first?

Candidate chain:
end demand -> server/ODM -> component -> packaging/test -> foundry -> U.S. expectations.

Estimate directed lead/lag per layer rather than forcing a single composite.

Priority: A

### W6N-E04 — Monthly Revenue Surprise Surface
Estimate point-in-time expected monthly revenue per Taiwan issuer from:
seasonality, prior monthly path, disclosed guidance, industry state and clean historical vintages.

Surprise =
disclosed revenue - point-in-time expected revenue.

Aggregate by economic exposure, not only market capitalization.

Priority: A

### W6N-E05 — NQ Physical Fundamental Confirmation Score
Fuse:
- Taiwan monthly revenue
- Korea first-10/20-day semiconductor exports
- U.S. EDGAR structured disclosures
- tech corporate TRACE credit breadth
- federal AI/semiconductor procurement where material
- validated data-center/grid activity

Output:
PHYSICAL_CONFIRMATION / NARROW_FINANCIAL_RALLY / FUNDAMENTAL_DIVERGENCE / BROAD_ACCELERATION.

Priority: S

### W6N-E06 — Semiconductor Export-Control State
Fuse:
BIS restrictions/Federal Register lifecycle with Taiwan/Korea physical demand.

Question:
Does an export-control change have different market impact when physical demand is accelerating, slowing, or rerouting?

Priority: S

## Gold / silver physical-market research

### W6N-E07 — COMEX Physical Inventory Migration
Source:
CME NYMEX/COMEX Delivery Notices & Stocks.

Archive the exact official inventory categories and depository-level changes.

Features:
- registered/deliverable-style inventory share according to current CME schema
- receipts and withdrawals
- category conversion
- depository concentration
- inventory velocity
- delivery-cycle normalization
- interaction with nearby OI and futures/spot basis

Do not interpret warehouse outflow as consumption without destination evidence.

Priority: S

### W6N-E08 — COMEX Delivery Concentration Pressure
Source:
CME Metals Issues and Stops Report.

Features:
- daily deliveries
- issues/stops concentration by clearing firm
- delivery / OI
- repeated firm-level issue/stop concentration
- contract-month seasonality
- first-notice-day state

Caution:
clearing-firm identity is not beneficial-owner intent.

Priority: A

### W6N-E09 — Gold ETF Physical Demand Pulse
Primary:
GLD and IAU issuer/trust disclosures.

Archive:
shares outstanding, ounces in trust, publication timestamp, trust/bar settlement state where applicable.

GLD explicitly distinguishes trade-date trust ounces from settlement-date bar-list ounces, making timing separation mandatory.

Output:
physical ETF creation/redemption pressure.

Priority: S

### W6N-E10 — Gold Physical Absorption Quotient
GPAQ =
(ETF metal demand + futures delivery demand + identifiable import pressure)
/
(exchange deliverable inventory + transferable physical capacity + market liquidity)

Hypothesis:
physical demand becomes more price-relevant when absorption capacity is constrained.

Priority: S

### W6N-E11 — COMEX–London Dislocation State
Fuse:
COMEX futures vs London spot basis, CME inventory movement, ETF physical flow, delivery intensity, transport/tariff conditions.

Classify:
- true physical tightness
- tariff/logistics relocation
- arbitrage transfer
- financial positioning

Motivation:
historical episodes show large inventory migration and unusual futures/spot spreads can arise from logistics/tariff concerns rather than simple scarcity.

Priority: S

### W6N-E12 — Gold Physical vs Financial Divergence
Financial layer:
GC futures/options, real yields, USD, volatility.

Investment-physical layer:
GLD/IAU shares and ounces.

Settlement layer:
COMEX stocks/deliveries.

Research:
does disagreement predict convergence, volatility or regime transition?

Priority: A

### W6N-E13 — Gold Four-Layer State
Layer 1: macro (real yields, USD, rates)
Layer 2: derivatives (GC futures/options/basis)
Layer 3: investment physical (ETF ounces/shares)
Layer 4: settlement physical (COMEX inventory/deliveries)

Use state combinations rather than one monolithic gold signal.

Priority: S

### W6N-E14 — Gold ETF Settlement-Lag Model
Separate:
creation notification -> share issuance -> trade-date trust holdings -> settlement-date bar holdings -> public update.

Purpose:
prevent false causal ordering between ETF flow and GC.

Priority: A

## Corporate credit -> equity / NQ

### W6N-E15 — Real-Time Corporate TRACE Credit Shock
FINRA states corporate/agency TRACE trade activity includes real-time transaction information such as execution time, quantity, price and yield.

For issuer bonds derive:
- Treasury/sector-neutral yield shock
- abnormal price impact
- trading-intensity surprise
- liquidity deterioration
- block activity
- maturity-curve deformation

Test whether residual bond stress leads issuer equity, sector, or NQ after common-news controls.

Priority: S

### W6N-E16 — Credit–Equity Causal Graph
Nodes:
single-name bonds, issuer equity, sector ETF, NQ/ES, and public credit-derivative risk transfer where usable.

Estimate leader probabilities by regime and event class.

Priority: S

### W6N-E17 — NQ Constituent Credit Breadth
Aggregate abnormal credit deterioration across large NQ technology issuers.

Weight alternatives:
market cap, debt outstanding, equal issuer, sector.

Question:
does credit breadth add risk information after rates/VIX/index return are controlled?

Priority: A

### W6N-E18 — Credit Liquidity Fracture
A yield move accompanied by disappearing fixed-income liquidity may represent a different state from a liquid repricing.

State =
credit shock × liquidity impairment.

Use:
tail-risk and regime detection.

Priority: A

## Federal procurement / forward demand

### W6N-E19 — SAM Forward Procurement Demand Pipeline
GSA SAM.gov public Opportunities API exposes published pre-solicitations, solicitations, sources-sought, notices and award notices. API key is required.

Build by:
agency, NAICS, PSC, capability, geography, deadline, amendment count, procurement type.

Goal:
measure forward government demand before awards.

Priority: S

### W6N-E20 — Solicitation-to-Award Conversion Model
Lifecycle:
sources sought -> pre-solicitation -> solicitation -> amendment -> award -> modification -> obligation -> outlay.

Estimate transition probabilities and durations.

Never treat a solicitation ceiling as booked revenue.

Priority: A

### W6N-E21 — USAspending Revenue Pulse
Map award transactions to public-company parents using stable identifiers and point-in-time subsidiary ownership.

Features:
new obligations, de-obligations, modifications, option exercises, agency/capability mix, period of performance.

Critical:
action_date != first public availability. Measure first_seen/last_modified lag.

Priority: A

### W6N-E22 — Defense Industrial Demand Pulse
Fuse:
SAM opportunities + USAspending transactions + DoD contract announcements + budget/program documents.

Capability buckets:
missiles/munitions, aircraft, shipbuilding, space, AI/cloud/cyber, semiconductors, rare earths.

Priority: A

### W6N-E23 — Government Demand Reality Gap
Compare:
authorized/budgeted demand -> published solicitation -> award -> obligation -> outlay.

The conversion gap itself is a feature.

Priority: A

### W6N-E24 — Government Demand + Innovation Pipeline
Fuse:
scientific/patent capability + SAM procurement intent + USAspending funded awards.

Question:
which firms progress from technical capability -> government demand -> funded revenue?

Priority: A

## Gulf energy / storm mechanics

### W6N-E25 — BSEE Hurricane Shut-In Pulse
BSEE reports Gulf storm-driven offshore oil/gas shut-in and evacuation statistics daily during active events.

Features:
oil shut-in, gas shut-in, platform/rig evacuation, daily change, restart velocity.

Priority: S for energy research

### W6N-E26 — Forecast-to-Shut-In Model
Use point-in-time NOAA forecast vintages and geospatial asset exposure to forecast expected BSEE shut-in BEFORE the BSEE realization.

Research the forecast error, not hindsight final-track fit.

Priority: A

### W6N-E27 — Gulf Infrastructure Stress Graph
Map:
offshore production -> pipeline -> LNG -> refinery -> port -> grid.

Fuse weather, BSEE, pipeline/LNG, grid and port information.

Separate oil supply, gas supply, refinery demand and LNG export effects.

Priority: S

### W6N-E28 — Production Restoration Half-Life
Estimate restart curves after storm passage.

Hypothesis:
duration mispricing may be more valuable than initial-shutdown prediction.

Priority: A

### W6N-E29 — Storm Directionality Decomposition
A storm can simultaneously:
remove production, reduce refinery demand, halt LNG exports, close ports, reduce power demand and damage infrastructure.

Model every physical channel separately. Never encode "hurricane = bullish energy."

Priority: S

## Sanctions / export controls / supply chains

### W6N-E30 — OFAC Sanctions Delta Graph
OFAC Sanctions List Service provides structured current lists and archived delta publications.

Archive each version and compute:
new entity, removal, program change, alias/address/vessel linkage.

Map to issuers, commodities, shipping, banks and supply chains.

Priority: A

### W6N-E31 — Sanctioned Vessel / Commodity Route Shock
Where a public sanction identifies vessels/operators:
map to lawful public shipping/port information and commodity-route exposure.

Test physical route impairment before return impact.

Priority: A

### W6N-E32 — BIS Technology Restriction Shock
Use BIS Entity List / Consolidated Screening List plus Federal Register public-inspection lifecycle.

Map to:
AI accelerators, semiconductor equipment, networking, aerospace and industrial technology.

Priority: S

### W6N-E33 — Semiconductor Export-Control Exposure Graph
Graph:
restricted end user/geography -> chip designer -> foundry -> equipment -> ODM/server -> revenue exposure.

Combine with W6N-E01/W6N-E02 physical demand.

Priority: S

### W6N-E34 — Policy-to-Physical Validation
For sanctions/export-control hypotheses require:
policy delta -> measurable trade/revenue/routing change -> expectation revision -> market response.

If physical effect is absent, downgrade.

Priority: S

## Cross-domain master candidates

### W6N-E35 — Institutional vs Physical Reality Divergence
Compare financial expectations with physical/fundamental measurements.

NQ example:
options/price bullish while semiconductor revenue/credit weak.

Gold example:
futures bullish while ETF/settlement physical flow weak.

Output may predict volatility/regime change even when direction is uncertain.

Priority: S

### W6N-E36 — Information Channel Rotation Detector
Estimate which information channel currently leads:
market microstructure, derivatives mechanics, credit, corporate fundamentals, physical telemetry or regulatory/public events.

Use as dynamic model-routing state.

Priority: S

## Highest-priority W6N queue

1. W6N-E01 Taiwan Monthly Revenue Semiconductor Pulse
2. W6N-E02 AI Hardware Supply-Chain Revenue Graph
3. W6N-E05 NQ Physical Fundamental Confirmation Score
4. W6N-E07 COMEX Physical Inventory Migration
5. W6N-E09 Gold ETF Physical Demand Pulse
6. W6N-E10 Gold Physical Absorption Quotient
7. W6N-E11 COMEX–London Dislocation State
8. W6N-E15 Real-Time Corporate TRACE Credit Shock
9. W6N-E17 NQ Constituent Credit Breadth
10. W6N-E19 SAM Forward Procurement Demand Pipeline
11. W6N-E25 BSEE Hurricane Shut-In Pulse
12. W6N-E33 Semiconductor Export-Control Exposure Graph
