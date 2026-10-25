# Wave 72X — Source Notes

Namespace: **W72X**

## W72X-D01 — LSEG WM/Refinitiv FX Benchmarks overview factsheet
Primary: https://www.lseg.com/content/dam/ftse-russell/en_us/documents/factsheets/wmr-overview-and-request-for-feedback.pdf
Owner: LSEG (Refinitiv Benchmark Services Ltd, WMR)
Cadence/latency class: Static factsheet (2022 vintage); benchmark itself is scheduled daily/hourly
Revision behavior: Factsheet revised ad hoc; benchmark republications 0.03% overall and 0.26% for 4pm over 2015-2020 per the document; 98.8% of all fixes and 99.4% of 4pm fixes published within 8 minutes
Rights status: Factsheet public; benchmark data licensed
Verification: VERIFIED by full PDF text extraction 2026-10-11: 5-minute calculation window, time-sliced capture, median, up to 47 intraday fix times, 3pm to 4pm EUR/USD average abs move 0.1209% (Q1 2020-Q1 2021). Window centering offsets NOT stated; PROVENANCE_PENDING for centering and for the window-change date.

## W72X-D02 — LSEG WMR FX benchmarks availability page
Primary: https://www.lseg.com/en/ftse-russell/benchmarks/wmr-fx-benchmarks
Owner: LSEG
Cadence/latency class: Static web page
Revision behavior: Page can change without notice; snapshot hash required
Rights status: Public page; rates licensed
Verification: VERIFIED via search excerpt: closing spot 4pm London Mon-Fri; intraday spot on the hour from Mon 06:00 HK/SG to Fri 22:00 London; 79 forward and 11 NDF currencies. Full page not fetched.

## W72X-D03 — ECB euro foreign exchange reference rates
Primary: https://www.ecb.europa.eu/stats/policy_and_exchange_rates/euro_reference_exchange_rates/html/index.en.html
Owner: European Central Bank
Cadence/latency class: Daily on TARGET working days; publication around 16:00 CET
Revision behavior: Corrections possible; framework document linked on the page not read
Rights status: Public, informational use only; ECB strongly discourages transaction use; CSV/XML/SDMX downloads
Verification: VERIFIED by fetch 2026-10-11: concertation 'normally ... around 14:10 CET', update ~16:00 CET, 29 currencies, EUR/RUB suspended. Older ECB/Banca d'Italia text says 14:15 CET: conflict noted, use current page.

## W72X-D04 — CME Group FX Markers article
Primary: https://www.cmegroup.com/articles/2026/fx-markers-price-reference-points-for-global-currency-exposure.html
Owner: CME Group
Cadence/latency class: Markers daily at 16:00 NY, 16:00 London, 15:00 Tokyo; 14:00 CT daily settlement
Revision behavior: Methodology can be amended by CME notice
Rights status: Public article; market data licensed
Verification: VERIFIED by fetch 2026-10-11 (article dated 16 Mar 2026): 30-second window, Tier 1 VWAP if 3+ trades, Tier 2 bid/ask mid, Tier 3 vendor spot and forward points. Whether tier-used is published per marker: PROVENANCE_PENDING.

## W72X-D05 — CME Group FX Fixing Price Methodology Guide
Primary: https://www.cmegroup.com/trading/fx/currfixprice.html
Owner: CME Group
Cadence/latency class: Daily at 10:00 a.m. New York time (60-second interval 9:59:00-9:59:59)
Revision behavior: Amended by CME; options expiry moved to 10:00 NY on 9 June 2019
Rights status: Public methodology; MDP 3.0 channel 320 licensed
Verification: VERIFIED by fetch 2026-10-11: 21 contracts, tier thresholds (20 contracts), MDEntryType W, vendor codes, auto-exercise table.

## W72X-D06 — CME Euro FX contract specs and FX Product Guide (BTIC, eFIX)
Primary: https://www.cmegroup.com/markets/fx/g10/euro-fx.contractSpecs.html
Owner: CME Group
Cadence/latency class: Spec page; Product Guide at https://www.cmegroup.com/markets/fx/fx-product-guide
Revision behavior: Specs revised via CME notices
Rights status: Public spec; feed licensed
Verification: VERIFIED by fetch 2026-10-11 (spec): Globex hours, tick 0.00005=$6.25, BTIC close 3:40-4:30 pm London, last trade 9:16 a.m. CT two business days before third Wednesday, daily settlement 14:00 CT stated in markers article. Product Guide read via search excerpt only: EURUSD BTIC references next WMR 4pm London, BTIC+ month-end WMR, eFIX WMR hourly and Tokyo 09:55 on EBS Market; PARTIALLY VERIFIED.

## W72X-D07 — CLSSettlement operational timeline and T+1 note
Primary: https://www.cls-group.com/media/qxalffzp/clssettlement_overview_feb2022.pdf
Owner: CLS Group
Cadence/latency class: Daily settlement cycle; operating 5.5 days; closes 02:00 CET Saturday, reopens 22:00 CET Sunday
Revision behavior: Schedule changes by CLS notice; T+1 note at https://www.cls-group.com/news/update-on-the-potential-change-to-clssettlement-timelines-following-the-move-to-tplus1-securities-settlement/ dated 9 April 2024
Rights status: Deck states exclusive use of recipient; do not redistribute; facts only
Verification: VERIFIED by PDF extraction (Feb 2022 vintage): 00:00 initial pay-in schedule, 06:30 revised, settlement 07:00-09:00 CET, early-closing funding target 10:00, late-closing 12:00, 18 eligible currencies. T+1 note VERIFIED by fetch. Currency-of-record in 2026 PROVENANCE_PENDING (check current CLS pages).

## W72X-D08 — CLS FX trading activity monthly reports and data suite
Primary: https://www.cls-group.com/products/data/
Owner: CLS Group
Cadence/latency class: Monthly report (lag to be measured); intraday spot volume product per third-party description
Revision behavior: Monthly figures may be restated
Rights status: Monthly summaries public; CLSMarketData products licensed
Verification: PARTIALLY VERIFIED via search excerpt: monthly list shows e.g. USD 2.83T June 2026 and USD 2.96T March 2026 total daily traded volume submitted; intraday product details and rights PROVENANCE_PENDING.

## W72X-D09 — GFXC Last Look guidance and FX Global Code Principle 17
Primary: https://www.globalfxc.org/docs/gfxc_report_last_look.pdf
Owner: Global Foreign Exchange Committee
Cadence/latency class: Static guidance (three-year review kept Principle 17 text); press release https://www.globalfxc.org/press/p171219.htm (19 Dec 2017)
Revision behavior: Code reviews every three years
Rights status: Public
Verification: VERIFIED by PDF extraction: recommendations on fair last look, ex-ante disclosures (symmetry of price check, window max/min length, cover and deal), information on handling of trade requests. Full Principle 17 text read in Appendix A of the PDF extract; 2017 release summary VERIFIED.

## W72X-D10 — CME Group article on EBS Market enhancements (2024)
Primary: https://www.cmegroup.com/articles/2024/strengthening-fx-primary-liquidity-on-ebs.html
Owner: CME Group
Cadence/latency class: Marketing article dated 17 Jun 2024; measurements from Q1 2024 rollouts
Revision behavior: Not revised; vendor-reported statistics
Rights status: Public article; EBS data licensed
Verification: VERIFIED by fetch 2026-10-11: top-of-book average 0.63 pip (30% reduction), 25% VWAP spread reduction for 10m, 17% lower median spread over US CPI, >20% EUR/USD volume on quarter/3-quarter pips, price points traded ~90% vs ~60%, +22% depth to 2.5 pips. Vendor statistics, treat as claims.

## W72X-D11 — BIS Triennial Central Bank Survey FX turnover April 2025
Primary: https://www.bis.org/statistics/rpfx25_fx.htm
Owner: Bank for International Settlements
Cadence/latency class: Every three years; preliminary Sept 2025, final later
Revision behavior: Preliminary figures revised; sources conflict on final release date (Dec 2025 vs Jun 2026)
Rights status: Public, BIS terms
Verification: VERIFIED by fetch (preliminary 30 Sept 2025 commentary): USD 9.6T/day, spot 31%, swaps 42%, USD 89.2%, EUR 28.9%, JPY 16.8%, GBP 10.2%, CNY 8.5%, CHF 6.4%. Final-vintage numbers and final release date PROVENANCE_PENDING.

## W72X-D12 — BIS Quarterly Review: Covered interest parity lost
Primary: https://www.bis.org/publications/qr-201609/covered-interest-parity-lost-understanding-cross-currency-basis
Owner: Bank for International Settlements
Cadence/latency class: One-off Sept 2016 article
Revision behavior: Static
Rights status: Public
Verification: VERIFIED by fetch: since 2014 basis exhibits quarter-end spikes along with repo rates; regulatory reporting and balance-sheet constraints; JPY example. Post-2016 behaviour not covered, must be re-tested.

## W72X-D13 — CFTC Commitments of Traders release schedule, notes and PRE API
Primary: https://www.cftc.gov/MarketReports/CommitmentsofTraders/ReleaseSchedule/index.htm
Owner: CFTC
Cadence/latency class: Weekly, usually Friday 3:30 pm ET with prior-Tuesday data; holiday delays
Revision behavior: Positions can be revised by CFTC; reporting levels change
Rights status: Public domain; API at https://publicreporting.cftc.gov/ dataset gpe5-46if (TFF Futures Only)
Verification: VERIFIED by fetch 2026-10-11 (schedule, explanatory notes, dataset JSON fields: dealer/asset_mgr/lev_money/other_rept positions long/short/spread).

## W72X-D14 — Evans (2018) Forex Trading and the WMR Fix
Primary: https://mpra.ub.uni-muenchen.de/81583/1/MPRA_paper_81583.pdf
Owner: Martin D.D. Evans / Journal of Banking and Finance 87, 233-247
Cadence/latency class: Static paper (MPRA No. 81583, 25 Sept 2017)
Revision behavior: Static
Rights status: Open working paper
Verification: VERIFIED by PDF extraction: 21 currencies, a decade, pre-fix volatility spikes and negative pre/post-fix correlation, concentrated at month-end; fix then a one-minute window; EBS data windows; effect size claims 'large enough to support attractive strategies' are the author's, untested for costs here.

## W72X-D15 — Krohn, Mueller, Whelan: FX fixings and returns around the clock
Primary: https://www.econstor.eu/bitstream/10419/248309/1/swp2021-48.pdf
Owner: Bank of Canada Staff Working Paper 2021-48
Cadence/latency class: Static 2021
Revision behavior: Possibly superseded by journal version; not checked
Rights status: Open working paper
Verification: PARTIALLY VERIFIED: authors and series verified from PDF first page; W-shape, Tokyo/ECB/London fixes and USD appreciation into fixes read from a search excerpt of the INSEAD copy; numeric results not independently reread.

## W72X-D16 — Ito and Yamada: Puzzles in the Tokyo fixing
Primary: https://academiccommons.columbia.edu/doi/10.7916/D86W9KQQ/download
Owner: Takatoshi Ito, Masahiro Yamada; J. Int. Economics 109 (2017) 214-234
Cadence/latency class: Static
Revision behavior: Static
Rights status: Open repository copy
Verification: PARTIALLY VERIFIED via search excerpt: 9:55 JST concentration, spike and reversal, importer-driven USD buying; gotobi date set is truncated in the excerpt so the date list is PROVENANCE_PENDING.

## W72X-D17 — Melvin and Prins: Equity hedging and exchange rates at the London 4pm fix
Primary: https://ideas.repec.org/a/eee/finmar/v22y2015icp50-72.html
Owner: J. Financial Markets 22, 2015, 50-72
Cadence/latency class: Static
Revision behavior: Static
Rights status: Full text restricted; abstract only
Verification: PARTIALLY VERIFIED: abstract-level only (equity gains over month predict currency depreciation before month-end fix; ECB workshop slides list authors Michael Melvin and John Prins). Full text not read.

## W72X-D18 — Fed central bank liquidity swaps
Primary: https://www.federalreserve.gov/monetarypolicy/bst_liquidityswaps.htm
Owner: Board of Governors of the Federal Reserve System
Cadence/latency class: Weekly H.4.1; ad hoc announcements
Revision behavior: Terms changed by FOMC
Rights status: Public
Verification: PARTIALLY VERIFIED via search excerpts: standing lines with ECB, BoJ, BoE, BoC, SNB; OIS+25bp after 15 March 2020 action. H.4.1 usage line item and current pricing PROVENANCE_PENDING.

## W72X-D19 — CME FX Link and FX Spot+
Primary: https://www.cmegroup.com/markets/fx/fx-spot-plus
Owner: CME Group
Cadence/latency class: Product pages
Revision behavior: Product status can change
Rights status: Public marketing; feeds licensed
Verification: PARTIALLY VERIFIED via search excerpt only: FX Link spreads between spot and futures on Globex; FX Spot+ described as all-to-all spot CLOB. Launch status of FX Spot+ UNVERIFIED -> PROVENANCE_PENDING.

## W72X-D20 — LSEG FX Matching
Primary: https://www.lseg.com/en/fx/venues/spot-matching-forwards-matching
Owner: LSEG
Cadence/latency class: Product page
Revision behavior: Product text revised
Rights status: Public
Verification: PARTIALLY VERIFIED via search excerpt: no last-look in Spot Matching; Matching launched 1992 as first electronic CLOB for spot FX. Full page not fetched.

## W72X-D21 — FX option expiry-cut conventions (secondary)
Primary: https://www.forex.com/en-us/glossary/option-expiry-date-price/
Owner: StoneX/forex.com; investingLive daily expiry lists
Cadence/latency class: Daily lists at 10:00 NY cut
Revision behavior: Lists change daily
Rights status: Secondary commentary; not primary
Verification: UNVERIFIED as primary: 10:00 ET and 15:00 Tokyo conventions corroborated by CME's own 10:00 NY alignment statement in D05. OTC strike/size lists are secondary commentary: PROVENANCE_PENDING.
