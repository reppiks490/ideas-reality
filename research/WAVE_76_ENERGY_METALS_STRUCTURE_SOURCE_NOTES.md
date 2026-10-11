# Wave 76Q — Source Notes

Namespace: **W76Q**

## W76Q-D01 — EIA Weekly Petroleum Status Report Schedule
Primary: https://www.eia.gov/petroleum/supply/weekly/schedule.php
Owner: US EIA
Cadence/latency class: Weekly Wed 10:30 ET; holiday table through Nov 2026
Revision behavior: Schedule edited via table; data revised later
Rights status: US government public domain; verify EIA copyright page
Verification: VERIFIED (page read)

## W76Q-D02 — EIA Weekly Natural Gas Storage Report Schedule
Primary: https://ir.eia.gov/ngs/schedule.html
Owner: US EIA
Cadence/latency class: Weekly Thu 10:30 ET; exceptions with '(Updated)' flags
Revision behavior: Schedule amended after publication
Rights status: Public
Verification: VERIFIED (page read)

## W76Q-D03 — EIA Open Data API v2 Documentation
Primary: https://www.eia.gov/opendata/documentation.php
Owner: US EIA
Cadence/latency class: API; free key required; latency not stated
Revision behavior: Data may change; no vintages guaranteed
Rights status: Free key, throttled; terms on EIA site
Verification: VERIFIED (page read); latency UNVERIFIED

## W76Q-D04 — EIA WPSR Sources and Methods
Primary: https://www.eia.gov/petroleum/supply/weekly/pdf/sources.pdf
Owner: US EIA
Cadence/latency class: Static
Revision behavior: Survey forms EIA-800/801/802/803/804/805/809 and blended series
Rights status: Public
Verification: SEARCH_VERIFIED (not read in full) - PP for details

## W76Q-D05 — CME WTI Crude Futures Contract Specs
Primary: https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html
Owner: CME Group / NYMEX
Cadence/latency class: Static spec page
Revision behavior: Can change by rule filing
Rights status: Spec public; market data licensed
Verification: VERIFIED (page read via scrape)

## W76Q-D06 — CME Crude Settlement Procedure
Primary: https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil
Owner: CME Group
Cadence/latency class: 14:28-14:30 ET VWAP window
Revision behavior: Page versioned in Confluence
Rights status: Public client wiki
Verification: VERIFIED (query extraction, exact text not read in full)

## W76Q-D07 — CME Gold Contract Specs and Settlement Procedure
Primary: https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html ; https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold
Owner: CME Group / COMEX
Cadence/latency class: 13:29-13:30 ET outright; 13:15-13:30 spreads (>=25 contracts Tier1)
Revision behavior: Page version 10 observed
Rights status: Public spec
Verification: VERIFIED (extraction)

## W76Q-D08 — CME Silver and Natural Gas Specs
Primary: https://www.cmegroup.com/markets/metals/precious/silver.contractSpecs.html ; https://www.cmegroup.com/markets/energy/natural-gas/natural-gas.contractSpecs.html
Owner: CME Group
Cadence/latency class: Static
Revision behavior: Rule-filing changes
Rights status: Public spec
Verification: VERIFIED (extraction); silver settlement window PP

## W76Q-D09 — ICE Brent Crude Futures
Primary: https://www.ice.com/products/219/Brent-Crude-Futures
Owner: ICE Futures Europe
Cadence/latency class: Static; hours 01:00-23:00 London
Revision behavior: Subject to ICE notices
Rights status: Spec public; data licensed
Verification: VERIFIED (extraction)

## W76Q-D10 — ICE Brent/WTI Futures Spread
Primary: https://www.ice.com/products/1242/Brent-WTI-Futures-Spread
Owner: ICE
Cadence/latency class: Static (dated 15 Jun 2026 per search)
Revision behavior: Notices
Rights status: Public spec
Verification: SEARCH_VERIFIED; PP

## W76Q-D11 — LBMA Precious Metal Prices / IBA Methodology
Primary: https://www.lbma.org.uk/prices-and-data/precious-metal-prices ; https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf
Owner: LBMA; ICE Benchmark Administration
Cadence/latency class: Auctions 10:30/15:00 gold, 12:00 silver London
Revision behavior: Methodology consultations (Dec 2016)
Rights status: IBA licence required for real-time/historical use
Verification: VERIFIED (LBMA page); methodology PDF PP

## W76Q-D12 — OPEC Press Releases
Primary: https://www.opec.org/pr-detail/593-1-march-2026.html
Owner: OPEC Secretariat
Cadence/latency class: Event driven; V8 monthly Sunday meetings Jan-Apr 2026
Revision behavior: Statements final
Rights status: Public
Verification: SEARCH_VERIFIED; calendar after Apr 2026 PP

## W76Q-D13 — CME OPEC Watch Tool
Primary: https://www.cmegroup.com/trading/energy/cme-opec-watch-tool.html
Owner: CME Group
Cadence/latency class: Web tool
Revision behavior: Unknown
Rights status: Web only
Verification: Link verified on CL page; data access PP

## W76Q-D14 — SSGA SPDR Gold Trust GLD
Primary: https://www.ssga.com/us/en/individual/etfs/funds/spdr-gold-trust-gld
Owner: State Street Global Advisors
Cadence/latency class: Daily
Revision behavior: NAV by LBMA PM; holdings field PP
Rights status: Web public
Verification: SEARCH_VERIFIED; basket size and NAV time PP

## W76Q-D15 — USO Prospectus / Roll Disclosure
Primary: https://gtlaw.com/nl/insights/2020/5/historic-decline-in-oil-may-trigger-additional-disclosures-by-fcms-and-product-restrictions (secondary); primary prospectus on SEC EDGAR PP
Owner: USCF / SEC
Cadence/latency class: Periodic
Revision behavior: Roll schedule changed May 2020
Rights status: Public SEC
Verification: UNVERIFIED primary - PROVENANCE_PENDING

## W76Q-D16 — CME Price Limits Page
Primary: https://www.cmegroup.com/trading/price-limits.html
Owner: CME Group
Cadence/latency class: Static/web
Revision behavior: Rule filings
Rights status: Web public
Verification: Page fetched; halt rule values not extracted - PP
