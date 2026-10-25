# Wave 70B — Source Notes

Namespace: **W70B**

## W70B-D01 — MDP 3.0 Incremental Refresh MBP and MBOFD
Primary: https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD
Owner: CME Group
Cadence/latency class: Spec page; updated per CME release cycle (page shows 'Updated Apr 20'); real-time feed itself is event-driven
Revision behavior: Wiki can change without notice; archive hash
Rights status: Spec page readable; feed is licensed (PAID_REALTIME)
Verification: VERIFIED by full page fetch 2026-10-11: tags 60, 5799 bit map, 268/270/271/48/83/346/1023/279/269/37719, MBO group 37705 with 37/37707/37706/9633/37708.

## W70B-D02 — MDP 3.0 Trade Summary
Primary: https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary
Owner: CME Group
Cadence/latency class: Spec page; event-driven feed
Revision behavior: Wiki versions
Rights status: Spec readable, feed licensed
Verification: PARTIALLY VERIFIED via search excerpt only (not full-page fetch): AggressorSide 5797 values 0/1/2, no-aggressor cases, NumberOfOrders 346, MDTradeEntryID 37711. Full text re-read needed.

## W70B-D03 — iLink Order Types
Primary: https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types
Owner: CME Group
Cadence/latency class: Spec; updated Apr 22 2025 stamp
Revision behavior: Wiki versions
Rights status: Spec readable
Verification: VERIFIED by full page fetch: OrdType 1 MWP, 2 limit, 3 stop with protection, 4 stop-limit, K market-limit; state restrictions; protection price limit mechanics.

## W70B-D04 — Globex Self-Match Prevention FAQ
Primary: https://cmegroup.com/globex/trade-on-cme-globex/self-match-faq.html
Owner: CME Group
Cadence/latency class: Static FAQ
Revision behavior: Edited without version history
Rights status: Public
Verification: PARTIALLY VERIFIED via search excerpt: tags 7928 (iLink 2)/2362 (iLink 3), tag 8000 values O/N, activation 16:30 CT Mon-Thu and 09:30 CT Sun, MEP weight 3. Page not fully fetched.

## W70B-D05 — Rule 534 Wash Trades advisory RA1614-5
Primary: https://www.cmegroup.com/tools-information/lookups/advisories/market-regulation/ra1614-5.html
Owner: CME Market Regulation
Cadence/latency class: Advisory notice, static
Revision behavior: Superseding advisories possible
Rights status: Public
Verification: PARTIALLY VERIFIED via search excerpt; also notes SMP does not prevent self-matches at opening if orders entered in Pre-Open.

## W70B-D06 — E-mini S&P 500 contract specifications
Primary: https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html
Owner: CME Group
Cadence/latency class: Static spec updated by exchange notice
Revision behavior: Spec changes via SER notices
Rights status: Public
Verification: VERIFIED by full fetch 2026-10-11: tick 0.25 = $12.50, calendar spread 0.05, hours, termination 9:30 ET 3rd Friday, rulebook chapter CME 358. Page showed ESZ6 at 7866.00 (delayed).

## W70B-D07 — S&P 500 Price Limits FAQ
Primary: https://www.cmegroup.com/trading/equity-index/sp-500-price-limits-faq.html
Owner: CME Group
Cadence/latency class: Static FAQ; effective dates in text (e.g., Oct 12, 2020 overnight change)
Revision behavior: Revised on rule change
Rights status: Public
Verification: PARTIALLY VERIFIED via search excerpt: reference price VWAP 14:59:30-15:00 CT, 7% overnight limit, 3.5% dynamic breaker with 2-minute pause, NYSE Rule 7.12 coupling. Re-read full page before use.

## W70B-D08 — Rule 588.H Non-Reviewable Ranges notices
Primary: https://www.cmegroup.com/notices/ser/2018/06/SER-8164.html
Owner: CME Group
Cadence/latency class: Event-driven Special Executive Reports; CFTC rule filings
Revision behavior: Table amended by filing
Rights status: Public
Verification: PARTIALLY VERIFIED: SER-8164 exists (2018 NRR adjustment) per search. A filing dated 2026-09-25, CME Submission 26-444, was shown in a search result at https://www.cftc.gov/filings/orgrules/rules09252630032.pdf; mapping of that URL to the submission NOT verified. Values not read.

## W70B-D09 — Messaging Efficiency Program
Primary: https://cmegroup.com/globex/trade-on-cme-globex/messaging-efficiency-program.html
Owner: CME Group
Cadence/latency class: Policy page; benchmarks recalculated periodically
Revision behavior: Version-numbered policy (v11.6 mentioned by search)
Rights status: Public
Verification: PARTIALLY VERIFIED via search excerpt; MEP PDF not opened; Treasury roll 3,000:1 benchmark from secondary press (fxnewsgroup.com). Weights/benchmarks PROVENANCE_PENDING.

## W70B-D10 — Databento GLBX.MDP3 documentation
Primary: https://databento.com/docs/venues-and-datasets/glbx-mdp3
Owner: Databento
Cadence/latency class: Docs; historical and live data product
Revision behavior: Docs revised
Rights status: Docs public; data licensed
Verification: SECONDARY; used only for mapping TransactTime->ts_event, SendingTime->ts_in_delta, F_LAST semantics (per search excerpt).

## W70B-D11 — MDP 3.0 SBE Technical Headers
Primary: https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457638617/MDP+3.0+-+SBE+Technical+Headers
Owner: CME Group
Cadence/latency class: Spec page
Revision behavior: Wiki versions
Rights status: Spec readable
Verification: PARTIALLY VERIFIED via search excerpt: SendingTime 64-bit ns since epoch, clock-synced to microsecond accuracy. Full page not fetched.

## W70B-D12 — arXiv microstructure papers
Primary: https://arxiv.org/abs/1011.6402 ; https://arxiv.org/abs/1312.0563 ; https://arxiv.org/abs/1312.0514 ; https://arxiv.org/abs/0904.0900 ; https://arxiv.org/abs/1207.6325 ; https://arxiv.org/abs/1012.0349 ; https://arxiv.org/abs/1610.00261
Owner: arXiv / authors
Cadence/latency class: Static preprints
Revision behavior: Versioned (v1..vN)
Rights status: Open access
Verification: VERIFIED titles and existence via arXiv API 2026-10-11 (Cont-Kukanov-Stoikov; Huang-Lehalle-Rosenbaum; Lipton et al.; Eisler-Bouchaud-Kockelkoren; Dayri-Rosenbaum; Gould et al.; Lehalle-Mounjid). Claims inside papers not re-derived.

## W70B-D13 — Stoikov micro-price
Primary: https://ideas.repec.org/a/taf/quantf/v18y2018i12p1959-1966.html
Owner: Taylor and Francis, Quantitative Finance 18(12)
Cadence/latency class: Static
Revision behavior: Corrections possible
Rights status: Paywalled
Verification: VERIFIED bibliographic record (vol 18, no 12, pp 1959-1966, DOI 10.1080/14697688.2018.1489139); full text not read; a Frankfurt thesis reports no improvement at most horizons (secondary).

## W70B-D14 — Moallemi and Yuan queue position valuation
Primary: https://drupalgsb-test.paas.cc.columbia.edu/sites/default/files-efs/pubfiles/25461/queue-value-2016.pdf
Owner: Columbia Business School
Cadence/latency class: Working paper (Dec 2016, rev Jun 2017)
Revision behavior: Versions
Rights status: Open copy
Verification: VERIFIED existence via search; full text not read; value-order-of-half-spread claim from secondary citing paper.

## W70B-D15 — Easley, Lopez de Prado, O'Hara VPIN
Primary: https://papers.ssrn.com/abstract=1695596
Owner: SSRN / RFS
Cadence/latency class: Static
Revision behavior: RFS version vs SSRN
Rights status: SSRN open abstract
Verification: VERIFIED bibliographic record (RFS 25(5):1457-1493); methods not re-derived.

## W70B-D16 — Kirilenko, Kyle, Samadi, Tuzun Flash Crash
Primary: https://papers.ssrn.com/ab_id=1686004
Owner: SSRN / J. Finance 72(3)
Cadence/latency class: Static
Revision behavior: Version differences 2010 vs 2017
Rights status: Open abstract
Verification: VERIFIED bibliographic record via search; uses E-mini S&P audit-trail data (CFTC-restricted data not available to us).

## W70B-D17 — Bessembinder et al. and Frey-Sandas hidden liquidity
Primary: https://papers.ssrn.com/ab_id=956476 ; https://ideas.repec.org/p/zbw/cfrwps/0906.html
Owner: SSRN / CFR Cologne
Cadence/latency class: Static
Revision behavior: Working paper vs journal
Rights status: Open abstracts
Verification: VERIFIED existence via search; equity (Euronext, Xetra) evidence only; futures transfer untested.

## W70B-D18 — CME ZN / CL / GC contract specs
Primary: https://cmegroup.com/trading/interest-rates/us-treasury/10-year-us-treasury-note_contractSpecs_futures.html ; https://cmegroup.com/trading/energy/crude-oil/light-sweet-crude_contractSpecs_futures.html ; https://cmegroup.com/trading/metals/precious/gold_contractSpecs_futures
Owner: CME Group
Cadence/latency class: Static spec
Revision behavior: SER notices
Rights status: Public
Verification: VERIFIED via search excerpts (ZN tick 1/2 of 1/32 = $15.625; CL $0.01 = $10; GC $0.10 = $10); pages not fully fetched.

## W70B-D19 — CME Rule 575 Disruptive Practices
Primary: https://www.cmegroup.com/rulebook/CME/V/500/575/575.pdf (URL pattern UNVERIFIED)
Owner: CME Group Rulebook
Cadence/latency class: Rulebook chapter 5
Revision behavior: Amended by filing
Rights status: Public
Verification: UNVERIFIED / PROVENANCE_PENDING: only secondary vendor blog text was seen. Do not cite rule elements until the rulebook PDF is archived.

## W70B-D20 — Obizhaeva and Wang
Primary: (no URL retrieved)
Owner: J. Financial Markets 16(1)
Cadence/latency class: Static
Revision behavior: n/a
Rights status: Journal
Verification: UNVERIFIED / PROVENANCE_PENDING: cited from memory; locate DOI and archive.
