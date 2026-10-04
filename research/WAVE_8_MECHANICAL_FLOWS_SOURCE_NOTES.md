# Wave 8M — Primary Source Notes

Namespace: W8M

## W8M-D01 — SEC Form 144 / EDGAR
https://www.sec.gov/submit-filings/filer-support-resources/how-do-i-guides/file-form-144-electronically
https://www.sec.gov/submit-filings/technical-specifications

Electronic Form 144 is a public notice of proposed sale. Same-day EDGAR dissemination and approximate-sale-date semantics make point-in-time reconstruction possible.

## W8M-D02 — Treasury Daily Treasury Statement
https://fiscaldata.treasury.gov/datasets/daily-treasury-statement/deposits-and-withdrawals-of-operating-cash
https://fiscaldata.treasury.gov/datasets/daily-treasury-statement/operating-cash-balance

Daily official cash/debt operations. DTS is on a modified-cash basis; weekends/federal holidays flow into the next business-day statement.

## W8M-D03 — USDA MyMarketNews
https://mymarketnews.ams.usda.gov/mymarketnews-api
https://mymarketnews.ams.usda.gov/mymarketnews-api/reports

API host:
https://marsapi.ams.usda.gov/services/v1.2/

Report-specific raw agricultural cash-market data. Preserve report identity and publication metadata.

## W8M-D04 — PJM Data Miner 2
https://dataminer2.pjm.com/

Examples include five-minute LMPs and instantaneous load. The instantaneous-load feed documents five-minute posting/update cadence. System-to-system API use requires a PJM account.

## W8M-D05 — ERCOT Market Information
https://www.ercot.com/mktinfo/rtm
https://www.ercot.com/mktinfo/prices
https://www.ercot.com/services/mdt/data-portal

SCED LMPs and reserve/scarcity measures update at real-time market cadence. Data Portal API access has registration/terms requirements.

## W8M-D06 — CFTC Swap Data Repositories
https://www.cftc.gov/IndustryOversight/DataRepositories/index.htm
https://www.cftc.gov/MarketReports/SwapsReports/index.htm

CFTC Part 43 requires public dissemination of certain swap transaction and pricing data through registered SDRs.

## W8M-D07 — CME Repository Services Public SDR
CME Repository Services publicly disseminates CFTC-regulated swap transaction/pricing data by asset class. Public records carry execution timestamps; dissemination may be delayed where regulations require it. Review commercial reuse terms before production redistribution.

## W8M-D08 — DTCC / ICE / Other Registered Repositories
Repository-specific public dissemination systems may cover CFTC swaps and/or SEC security-based swaps. Product taxonomies, action types, caps and correction semantics must be normalized before cross-source use.
