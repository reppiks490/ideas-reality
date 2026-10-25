# Wave 75A — Source Notes

Namespace: **W75A**

Status vocabulary: VERIFIED = primary artifact content read this session (2026-10-11); PARTIAL = page read but requested field absent; UNVERIFIED / PROVENANCE_PENDING = not confirmed, must be checked before any dependency.

## W75A-D01 — SEC EDGAR APIs
Primary: https://www.sec.gov/edgar/sec-api-documentation
Owner: U.S. SEC
Cadence/latency class: PUBLIC_NEAR_REALTIME; submissions delay typically <1s, XBRL APIs <1 min, bulk ZIP rebuilt nightly ~3:00 a.m. ET
Revision behavior: Filings are append-only; amendments are new accessions; bulk files rebuilt nightly
Rights status: Public; fair access applies
Verification note: VERIFIED (content read 2026-10-11); CORS not supported; rate limit not stated on this page

## W75A-D02 — SEC Developer Resources and Fair Access
Primary: https://www.sec.gov/about/developer-resources
Owner: U.S. SEC
Cadence/latency class: Policy
Revision behavior: n/a
Rights status: Public
Verification note: VERIFIED: 10 requests/second per user across machines; User-Agent rule and EDGAR hours not stated on the page, UNVERIFIED

## W75A-D03 — Form 8-K Item Taxonomy
Primary: https://www.sec.gov/files/form8-k.pdf
Owner: U.S. SEC
Cadence/latency class: PUBLIC_EVENT_DRIVEN
Revision behavior: Form revisions by rule
Rights status: Public
Verification note: PARTIAL: PDF not text-extractable by fetch; Item numbering cross-checked against Financial_Datasets list_filing_item_types (1.01-9.01 without 1.05). Deadline text UNVERIFIED => PROVENANCE_PENDING

## W75A-D04 — FOMC Calendars and Minutes
Primary: https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm
Owner: Federal Reserve Board
Cadence/latency class: PUBLIC_SCHEDULED
Revision behavior: Dates tentative until confirmed; minutes 3 weeks after decision
Rights status: Public
Verification note: VERIFIED: 2026 dates and minute dates read; statement release time not on page (UNVERIFIED)

## W75A-D05 — ECB Press Conferences
Primary: https://www.ecb.europa.eu/press/pressconf/html/index.en.html
Owner: European Central Bank
Cadence/latency class: PUBLIC_SCHEDULED
Revision behavior: n/a
Rights status: Public
Verification note: PARTIAL: live press conference 14:45 CET stated; decision release time UNVERIFIED

## W75A-D06 — GDELT Project Data
Primary: https://www.gdeltproject.org/data.html
Owner: GDELT Project
Cadence/latency class: PUBLIC_NEAR_REALTIME, 15-minute Events/GKG updates
Revision behavior: Records stored by date found; reprocessing possible
Rights status: Open with citation (terms UNVERIFIED)
Verification note: VERIFIED cadence and 65 translated languages; field-level timestamps UNVERIFIED

## W75A-D07 — Wikimedia Pageviews API
Primary: https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html
Owner: Wikimedia Foundation
Cadence/latency class: PUBLIC_BATCH
Revision behavior: Data from 2015-07-01; later corrections possible
Rights status: Open; access policy page not read
Verification note: PARTIAL: start date verified; granularity, latency, rate limit UNVERIFIED

## W75A-D08 — Google Trends
Primary: https://trends.google.com/
Owner: Google
Cadence/latency class: UNKNOWN_MEASURED; sampled and normalized
Revision behavior: Resampled per request; not vintage-stable
Rights status: Google terms; UNVERIFIED
Verification note: UNVERIFIED: developers.google.com Trends API page returned 404; PROVENANCE_PENDING

## W75A-D09 — Alpha Vantage News and Transcripts
Primary: https://www.alphavantage.co/documentation/
Owner: Alpha Vantage
Cadence/latency class: PAID_REALTIME for premium endpoints
Revision behavior: Vendor may rescore
Rights status: Licensed; premium gate observed
Verification note: PARTIAL: connector schema verified (tickers, topics, time_from YYYYMMDDTHHMM, limit<=1000, sort); live call hit premium/rate limit 2026-10-11; response fields UNVERIFIED

## W75A-D10 — FMP News and Transcripts
Primary: https://site.financialmodelingprep.com/developer/docs
Owner: Financial Modeling Prep
Cadence/latency class: PAID_REALTIME; transcripts need Ultimate/Enterprise
Revision behavior: Unknown
Rights status: Licensed
Verification note: PARTIAL: connector schema verified; news endpoint ACCESS DENIED on current plan 2026-10-11; latency UNVERIFIED

## W75A-D11 — Quartr Events and Transcripts
Primary: https://quartr.com/
Owner: Quartr
Cadence/latency class: LICENSED_REALTIME; live and final transcript variants
Revision behavior: Best variant auto-served; live transcript superseded by final
Rights status: Licensed
Verification note: PARTIAL: tool schema verified (section=qna, fromTimestamp, incremental live reads); no live call made; latency UNVERIFIED

## W75A-D12 — LunarCrush API
Primary: https://lunarcrush.com/developers/api/endpoints
Owner: LunarCrush
Cadence/latency class: PAID_REALTIME (assumed)
Revision behavior: Metric definitions may change
Rights status: Licensed
Verification note: PARTIAL: docs page returned no content; connector tool names exist (topic_time_series, stocks, cryptocurrencies); fields UNVERIFIED

## W75A-D13 — X Developer Terms
Primary: https://developer.x.com/en/developer-terms/more-on-restricted-use-cases
Owner: X Corp.
Cadence/latency class: Policy
Revision behavior: Terms change
Rights status: Restrictive/paid
Verification note: UNVERIFIED: HTTP 402; PROVENANCE_PENDING

## W75A-D14 — Reddit Data API Wiki
Primary: https://support.reddithelp.com/hc/en-us/articles/16160319875092-Reddit-Data-API-Wiki
Owner: Reddit
Cadence/latency class: Policy
Revision behavior: Terms change
Rights status: Commercial use requires terms (UNVERIFIED)
Verification note: UNVERIFIED: HTTP 403; PROVENANCE_PENDING

## W75A-D15 — Nasdaq Trading Halts
Primary: https://www.nasdaqtrader.com/Trader.aspx?id=TradeHaltCodes
Owner: Nasdaq
Cadence/latency class: PUBLIC_EVENT_DRIVEN
Revision behavior: Codes versioned
Rights status: Public
Verification note: UNVERIFIED this session (carried from W27V-D03)
