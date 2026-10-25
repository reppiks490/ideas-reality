# Wave 81E — Source Notes

Namespace: **W81E**

Status key: VERIFIED = primary page or document fetched and read in this session; PARTIAL = confirmed via search snippet or abstract only; PROVENANCE_PENDING = not verified, do not rely.

## W81E-D01 — NYSE Opening and Closing Auctions Fact Sheet

Primary: https://www.nyse.com/publicdocs/nyse/NYSE_Auctions_Closing_Process_Fact_Sheet.pdf

Owner: NYSE (Intercontinental Exchange)

Cadence/latency class: PUBLIC_SCHEDULED document

Revision behavior: Revised with rule changes (copyright 2024 on version read)

Rights status: Public fact sheet

Verification: VERIFIED: PDF downloaded and text read; opening info from 8:00 a.m. every second; MOC/LOC cutoff 3:50 p.m.; imbalance publication every second from 3:50 if changed; Closing Offset order rules; opening 10% algorithmic range

## W81E-D02 — NYSE Pillar Order Imbalances Client Specification v2.2k

Primary: https://nyse.com/publicdocs/nyse/data/Pillar_Order_Imbalances_Client_Specification_v2.2k.pdf

Owner: NYSE (ICE Data Services)

Cadence/latency class: PAID_REALTIME; messages every second if changed during auctions

Revision behavior: Versioned; later revision 2.2l referenced in change log (not read)

Rights status: Paid market data product; spec public

Verification: VERIFIED: PDF downloaded and text read; fields Auction Type (C, P, R, M, O, H), ImbalanceSide, PairedQty, TotalImbalanceQty, Unpaired Qty/Side, Significant Imbalance, AuctionStatus, FreezeStatus; publication windows by venue

## W81E-D03 — Nasdaq Closing Cross FAQ

Primary: https://www.nasdaqtrader.com/content/productsservices/Trading/ClosingCrossfaq.pdf

Owner: Nasdaq

Cadence/latency class: Document; defines cutoffs and NOII cadence

Revision behavior: Dated (copyright 2019); rules changed in the past (2018 move to 3:55 and 2019 early dissemination)

Rights status: Public document

Verification: VERIFIED but DATED: text read; 3:50 early dissemination every 10 seconds, 3:55 stop MOC and every-second NOII, LOC to 3:58, IO to 4:00; current Nasdaq rule text PROVENANCE_PENDING

## W81E-D04 — Nasdaq NOIView Interface Specification v2.0

Primary: https://www.nasdaqtrader.com/content/technicalsupport/specifications/dataproducts/Noiview-v2spec.pdf

Owner: Nasdaq

Cadence/latency class: PAID_REALTIME data product; spec public

Revision behavior: Version 2.00 dated 11/11/2010; field set may have changed

Rights status: Public spec, paid data

Verification: VERIFIED but DATED: text read; NOII fields, Cross Type, Price Variation Indicator; cadence in this doc (5 seconds) conflicts with 2019 FAQ (10 seconds then 1 second) so use FAQ and current ITCH 5.0 spec PROVENANCE_PENDING

## W81E-D05 — Nasdaq-100 Index Methodology

Primary: https://indexes.nasdaqomx.com/docs/Methodology_NDX.pdf

Owner: Nasdaq Indexes

Cadence/latency class: PUBLIC_BATCH document

Revision behavior: Copyright 2026 version read; methodology amended periodically

Rights status: Public document

Verification: VERIFIED: PDF downloaded and text read; weight constraints 24% and 4.5%/48% to 40%; special rebalance; Fast Entry top 40; IPO rule seventh trading day; dissemination once per second 09:30:01 to 17:16:00 ET with corrections until 17:15

## W81E-D06 — SEC Exchange-Traded Funds Small Entity Compliance Guide (Rule 6c-11)

Primary: https://www.sec.gov/investment/exchange-traded-funds-small-entity-compliance-guide

Owner: U.S. Securities and Exchange Commission

Cadence/latency class: Regulatory document

Revision behavior: Static; rule effective Dec 23 2019

Rights status: Public domain

Verification: VERIFIED: page read; daily website disclosures, 2%/7-day premium discount disclosure, 30-day median spread, custom baskets policies

## W81E-D07 — FINRA Daily Short Sale Volume Files

Primary: https://www.finra.org/finra-data/browse-catalog/short-sale-volume-data/daily-short-sale-volume-files

Owner: FINRA

Cadence/latency class: PUBLIC_BATCH posted by 6:00 pm ET trade date

Revision behavior: Files may be updated later; both versions shown

Rights status: Public with FINRA terms; Equity API on developer.finra.org per page

Verification: VERIFIED: page read (via fetch summary); consolidated NMS and TRF/ADF/ORF files; media-reported trades only; starts Aug 2018

## W81E-D08 — FINRA Regulation SHO Short Sale Trade Data (monthly transaction files)

Primary: https://www.finra.org/filing-reporting/trf/trf-regulation-sho-2020

Owner: FINRA

Cadence/latency class: PUBLIC_DELAYED monthly

Revision behavior: Static monthly files

Rights status: Public

Verification: PARTIAL: URL from search results; content not read directly

## W81E-D09 — Bogousslavsky and Muravyev, Who trades at the close?

Primary: Journal of Financial Markets 66 (2023); no URL verified (publisher page not fetched)

Owner: Academic

Cadence/latency class: RETROSPECTIVE_ONLY

Revision behavior: Static

Rights status: Academic

Verification: PARTIAL: citation confirmed by search; 7.3% closing-auction volume share (2018) and ETF association come from a working-paper seminar listing; full text not read

## W81E-D10 — Cheng and Madhavan, The Dynamics of Leveraged and Inverse ETFs

Primary: https://joim.com/dynamics-leveraged-inverse-exchange-traded-funds

Owner: Journal of Investment Management 7(4) 2009

Cadence/latency class: RETROSPECTIVE_ONLY

Revision behavior: Static

Rights status: Academic; full text behind login

Verification: PARTIAL: abstract-level via search; flow formula not verified

## W81E-D11 — SEC SRO Rule Filings for Closing Auction Changes

Primary: https://www.sec.gov/files/rules/sro/nyse/2018/34-84804.pdf ; https://sec.gov/files/rules/sro/nyse/2019/34-85021.pdf ; https://www.sec.gov/files/rules/sro/nasdaq/2019/34-85292.pdf ; https://www.sec.gov/file/34-91096

Owner: SEC / NYSE / Nasdaq

Cadence/latency class: PUBLIC_EVENT_DRIVEN

Revision behavior: Amended by later filings

Rights status: Public domain

Verification: PARTIAL: URLs surfaced by search; documents not read

## W81E-D12 — Index Provider Constituent Weights (S&P Dow Jones Indices, Nasdaq)

Primary: No factsheet fetched; S&P DJI site not reached

Owner: S&P Dow Jones Indices; Nasdaq Indexes

Cadence/latency class: PUBLIC_BATCH / LICENSED

Revision behavior: Weights change daily

Rights status: Licensed or restricted redistribution

Verification: PROVENANCE_PENDING: concentration figures seen only in third-party blogs; do not use

## W81E-D13 — CME Equity Index Futures Hours and Specs

Primary: https://www.cmegroup.com/trading-hours.html

Owner: CME Group

Cadence/latency class: PUBLIC_SCHEDULED

Revision behavior: Holiday modifications

Rights status: CME terms

Verification: PROVENANCE_PENDING: fetch returned HTTP 503

## W81E-D14 — FINRA Short Interest Reporting

Primary: https://www.finra.org/filing-reporting/regulatory-reporting/short-interest

Owner: FINRA

Cadence/latency class: PUBLIC_DELAYED (semi-monthly)

Revision behavior: Static cycles

Rights status: Public

Verification: PROVENANCE_PENDING: fetch returned HTTP 404
