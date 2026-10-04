# Wave 5 Discoveries

Wave 5 moves further away from conventional market indicators into physical deliverability, offshore energy interruption, sanctions, money-market internals, option-clearing breadth, public cyber events, cloud infrastructure, port operability, and tariff implementation.

All items are research hypotheses, not claims of alpha.

## E101 — COMEX Deliverable Inventory Pressure

Primary source:
CME Registrar metals depository/delivery data.

Status:
LIVE/TERMS_REVIEW_REQUIRED for production use.

CME documentation describes daily metals files containing:
- registered inventory
- eligible inventory
- receipts
- withdrawals
- net changes
- delivery point
- product
- prior/current totals

Mechanism:
Registered inventory is the stock already warranted/available for delivery; eligible inventory meets specifications but is not necessarily warranted. Changes in deliverable supply may matter differently from total warehouse stock.

Candidate features:
- registered / total
- registered / nearby open interest
- registered inventory velocity
- eligible-to-registered conversion
- withdrawal acceleration
- inventory concentration by depository
- inventory shock conditional on delivery month
- inventory shock conditional on spread/basis

Targets:
GC, SI, HG first.

Do not infer scarcity from low registered stock alone. Delivery economics, eligible conversion, imports, EFPs and spread structure matter.

Priority: A+

## E102 — Delivery-Month Physical Squeeze State

Fuse:
- E101 deliverable inventory
- nearby/deferred futures spread
- delivery notices where accessible
- open interest migration
- registered inventory changes
- warehouse deposits/withdrawals
- volatility/liquidity

Output:
NORMAL / TIGHTENING / DELIVERY_STRESS / RELEASE.

Hypothesis:
A physical squeeze is more credible when deliverable stock, spread behavior and delivery mechanics agree.

Priority: S-

## E103 — Gulf Offshore Shut-In Trajectory

Source:
Bureau of Safety and Environmental Enforcement Hurricane Activity Updates.

Status:
LIVE during relevant storms.

Official BSEE pages state that during threatening severe weather the Gulf hurricane response team monitors offshore operator reports and publishes production shut-in / evacuation updates daily, generally around early afternoon.

Fields include:
- platforms evacuated
- rigs evacuated
- dynamically positioned rigs moved
- oil BOPD shut in
- gas MMCFD shut in
- percent of Gulf production shut in

Mechanism:
This is realized physical production loss, not a forecast.

Feature family:
- shut-in oil trajectory
- shut-in gas trajectory
- acceleration/deceleration
- restoration half-life
- realized shut-in / pre-storm expected shut-in
- production-weighted geographic exposure

Targets:
CL, NG and regional energy equities first.

Priority: S

## E104 — Hurricane Energy Impact Graph

Fuse:
- NOAA/NHC forecast track and cone vintages
- facility/platform geolocation and production exposure
- BSEE realized shut-in
- LNG terminal state
- refinery status
- USCG port conditions/notices
- NOAA PORTS observations
- pipeline/terminal constraints
- EIA physical balances

Critical sign logic:
A Gulf storm can be bullish crude from offshore production loss while simultaneously reducing refinery crude demand; gas effects can differ again if LNG/feedgas or onshore demand is disrupted.

Output:
oil supply loss, gas supply loss, refinery demand loss, export loss, logistics impairment, restoration state.

Priority: S

## E105 — OFAC Sanctions Exposure Graph

Source:
U.S. Treasury OFAC Sanctions List Service and Recent Actions.

Status:
LIVE/event-driven.

Official machine-readable formats include XML/CSV and richer enhanced/advanced schemas.

Research graph:
sanctioned entity
-> parent/subsidiary
-> bank
-> vessel/operator
-> commodity
-> supplier/customer
-> public issuer
-> geography.

Feature:
economic exposure × designation severity × network centrality × substitutability.

Hard requirement:
preserve first-public timestamp and content hash for every list version.

Priority: S-

## E106 — Sanctions Network Propagation

The first-order designated company may be less important than the network around it.

Research:
- shipping/vessel rerouting
- bank de-risking
- commodity export/import displacement
- supplier/customer substitution
- country-risk repricing
- insurance/freight effect

Test:
Does network exposure explain cross-sectional return/commodity reactions better than issuer-name matching?

Priority: A+

## E107 — Money-Market Fund Liquidity Reservoir Microstate

Source:
SEC Form N-MFP/N-MFP3.

Status:
MONTHLY DISCLOSURE of prior-period data.

Official SEC facts:
- Form N-MFP is filed by the fifth business day of the following month.
- N-MFP3 contains daily subseries from the prior month, including shareholder flows and liquid-asset measures.

Candidate state:
- daily gross subscriptions/redemptions reconstructed after filing
- daily/weekly liquid asset ratios
- yield and shadow-NAV state
- portfolio maturity/liquidity
- Treasury/agency/repo allocation
- fund-class segmentation

Critical anti-leakage rule:
A daily value for last month was not public on that historical day merely because the form contains a daily series. Availability begins only at filing/publication time.

Priority: A

## E108 — N-MFP Repo Counterparty / Collateral Concentration

Source:
SEC N-MFP portfolio and repo-related disclosures.

Research:
Measure money-fund reliance on repo counterparties/collateral categories and concentration changes.

Composite:
money-fund cash reservoir
× repo counterparty concentration
× dealer funding stress
× Treasury collateral state.

Use:
slow funding fragility/regime variable.

Priority: A

## E109 — OCC Options Participation Breadth

Source:
Options Clearing Corporation daily volume and open-interest reports.

Status:
LIVE daily reports/downloads.

Research:
Instead of only using one exchange's option feed, construct clearing-level participation/breadth measures.

Features:
- total options volume by product class
- open-interest change
- ETF vs equity vs index option share
- options/futures activity ratio
- concentration across underlyings
- unusual volume relative to OI

Priority: A

## E110 — Option OI Migration × Hedge Mechanics

Fuse:
OCC clearing-level OI/volume
+ CME/exchange-specific detailed option data where licensed
+ gamma/vanna/charm phase
+ underlying liquidity.

Question:
Is mechanical hedge pressure more predictive when fresh OI accumulation confirms that exposures are being built rather than merely traded intraday?

Priority: S-

## E111 — CISA Known-Exploited-Vulnerability Exposure Shock

Source:
CISA Known Exploited Vulnerabilities Catalog.

Status:
LIVE public JSON/CSV.

Official feed fields include:
catalog version/release date,
CVE,
vendor/project,
product,
date added,
required action,
due date,
known ransomware-campaign use indicator.

Mechanism:
KEV addition confirms active exploitation in the wild. Map affected vendor/product to public-company and customer/dependency exposure.

Research only:
No exploit instructions are needed or useful.

Features:
- new KEV count by vendor
- severity/exposure proxy
- product criticality
- customer dependency breadth
- cloud/on-prem deployment relevance
- ransomware-use flag
- remediation-window pressure

Priority: A

## E112 — Cloud Infrastructure Outage Exposure Map

Sources:
public AWS service health,
Google Cloud Service Health,
Azure public status/history,
Cloudflare status/Radar where appropriate.

Status:
LIVE public incident communication, scope varies by provider.

Mechanism:
Cloud outages can create real revenue/transaction/service interruptions in dependent firms.

Graph:
provider -> service -> region -> dependent company/product -> revenue/process exposure.

Features:
- incident start/duration
- region breadth
- service criticality
- affected dependency count
- degradation vs full outage
- recovery velocity

Priority: A

## E113 — Multi-Cloud Substitution / Contagion State

Question:
When one cloud fails, which services shift load successfully and which fail jointly because of shared dependencies?

Research:
classify:
ISOLATED_PROVIDER
SHARED_NETWORK
DEPENDENCY_CONTAGION
SUCCESSFUL_FAILOVER
MULTI_PROVIDER_SYSTEMIC.

Potential target:
cloud vendors, SaaS basket, e-commerce/payment infrastructure, later broad index only if material.

Priority: B+

## E114 — SEC MIDAS Market-Structure Regime Atlas

Source:
SEC Market Structure Data / MIDAS.

Status:
RETROSPECTIVE/DELAYED research data.

Official downloadable individual-security/exchange metrics include:
- cancels
- trades
- lit trades
- odd lots
- hidden executions
- order volume
- trade volume
- odd-lot volume
- hidden volume
- market-cap/turnover/volatility/price ranks

Use:
discover persistent market-structure regimes and explanatory features.

Do not treat quarterly/retrospective datasets as a live feed.

Priority: A as research infrastructure

## E115 — Hidden/Odd-Lot Microstructure State

Offline discovery:
Use SEC MIDAS to test whether hidden-trade share, odd-lot share, cancel/trade ratios and trade/order volume identify liquidity regimes that improve prediction or execution.

If validated:
reconstruct equivalent variables live from properly licensed/current market data.

This is a retrospective-to-live transfer candidate, not a direct connector.

Priority: A

## E116 — CBP CSMS Trade-Implementation Edge

Source:
U.S. Customs and Border Protection Cargo Systems Messaging Service.

Status:
LIVE public operational messages/archives.

Messages include:
HTS updates,
tariff implementation guidance,
quota bulletins,
ACE changes,
entry/cargo guidance and effective dates.

Mechanism:
Legal policy announcement and actual customs implementation are distinct events. CSMS can reveal the operational layer that importers/brokers must implement.

Research:
measure information at:
policy announcement
-> USTR/Federal Register rule
-> CBP CSMS implementation guidance
-> effective timestamp
-> customs receipts/import response.

Priority: A+

## E117 — USTR / HTS Tariff Exposure Tensor

Sources:
USTR notices + Federal Register + HTS/CBP implementation.

Dimensions:
origin country
× HTS code
× tariff delta
× exemption status
× effective time
× company input/output exposure
× substitutability.

Use:
company/sector/commodity exposure, not generic "tariff sentiment."

Priority: S-

## E118 — Tariff Rule-to-Physical Diffusion Chain

Fuse:
USTR legal action
-> Federal Register
-> CBP CSMS
-> HTS code changes
-> customs duty receipts
-> port/import data
-> company inventory/margin outcomes.

Goal:
measure the path from legal rule to physical economic effect.

Priority: S

## E119 — Public CAT/MIDAS Aggregate Market-Stress Ledger

Important boundary:
The full CAT regulatory order-lifecycle data are not public.

Publicly available CAT/SEC materials provide aggregate statistics and SEC MIDAS provides public market-structure metrics.

Research:
use only legitimately public aggregate statistics to track market-structure change, reporting health and high-level activity.

Never describe this as public access to CAT order-level data.

Priority: B research infrastructure

## E120 — Physical Deliverability Pressure

Generalized framework:
PDP = delivery_obligation_pressure / immediately_deliverable_supply

Possible inputs by commodity:
- registered/deliverable warehouse stock
- delivery notices
- nearby open interest
- calendar spread
- cash basis
- load-out/withdrawal capacity
- imports
- storage geography

Use:
metals/grains/other physically deliverable markets only where contract mechanics are understood.

This is the physical-market analog of Market Absorption Quotient.

Priority: S

## E121 — NOAA PORTS Operability Field

Source:
NOAA CO-OPS / PORTS API.

Status:
LIVE.

Official API supports real-time/preliminary six-minute water levels at many stations, currents, wind, visibility, pressure and other observations.

Mechanism:
Vessel transit capacity can become physically constrained by water depth, currents, wind and visibility.

Features:
- water-level deviation vs prediction
- visibility shock
- current speed/direction constraint
- wind/gust constraint
- compound navigation stress
- recovery half-life

Combine with AIS/anchorage queues and port throughput.

Evidence:
2026 research on Port Houston documented measurable anchorage queue growth/recovery during fog-related channel closures.

Priority: A+

## E122 — Port Closure / Reopening State

Sources:
U.S. Coast Guard Captain of the Port notices/press releases/MSIBs where public,
plus port authority status.

Status:
PUBLIC but often semi-structured/unstructured.

Research:
extract port condition, closure, restricted operation and reopening timestamps.

Composite:
USCG status
+ NOAA PORTS physical conditions
+ AIS anchorage queue
+ port arrivals
+ inland transport.

Priority: A

## Wave 5 strongest first tests

1. E103 Gulf Offshore Shut-In Trajectory
2. E104 Hurricane Energy Impact Graph
3. E101 COMEX Deliverable Inventory Pressure
4. E120 Physical Deliverability Pressure
5. E105 OFAC Sanctions Exposure Graph
6. E107 N-MFP Liquidity Reservoir Microstate
7. E110 Option OI Migration × Hedge Mechanics
8. E116 CBP Trade-Implementation Edge
9. E118 Tariff Rule-to-Physical Diffusion Chain
10. E121 NOAA PORTS Operability Field
