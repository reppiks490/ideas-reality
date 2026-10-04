# Wave 11C — Source Notes

Namespace: **W11C**

## W11C-D01 — USDA Export Sales Reporting Program
Primary:
https://www.fas.usda.gov/programs/export-sales-reporting-program

Key timing:
qualifying daily sales are reported by exporters to USDA by 3:00 p.m. ET on the following business day and published by FAS at 9:00 a.m. ET on the subsequent business day.

Use:
mandatory forward physical-demand confirmation.

## W11C-D02 — CME Performance Bond / Margin Advisories
Primary:
https://www.cmegroup.com/notices/clearing.html
https://www.cmegroup.com/solutions/risk-management/performance-bonds-margins/faq-performance-bonds-margins.html

CME states public margin changes are announced through clearing advisories and historical margin PDFs are available back to 2003.

Preserve:
notice timestamp,
effective timestamp,
old/new initial and maintenance,
SPAN parameter changes,
product/tier.

## W11C-D03 — ICE Clearing Margin Notices
Primary:
https://www.ice.com/clearing/clear-us/notices

ICE Clear U.S. publishes product-level margin-parameter update notices with effective dates.

Use as cross-exchange comparison, subject to current terms.

## W11C-D04 — FINRA TRACE Securitized Products
Primary:
https://www.finra.org/filing-reporting/trace
https://developer.finra.org/

FINRA TRACE covers agency pass-through MBS/TBA and other securitized products. In July 2026 FINRA announced additional securitized-product datasets on its API platform, including Agency Pass-Thru TBA pricing.

Current reporting/dissemination rules must be versioned by date. Historical rule text documents 15-minute reporting for TBA good-delivery after the transition and different timing for other categories.

## W11C-D05 — GSE MBS Disclosures
Primary issuer sources:
https://capitalmarkets.fanniemae.com/
https://capitalmarkets.freddiemac.com/
https://www.ginniemae.gov/investors/disclosures_and_reports/

Potential research fields:
issuance,
pool/security characteristics,
factors/prepayments,
coupon/vintage structure.

Exact feed cadence and redistribution rights must be verified per product.

## W11C-D06 — New York Fed Agency MBS Operations
Primary:
https://www.newyorkfed.org/markets/desk-operations/ambs
https://www.newyorkfed.org/markets/ambs/ambs_schedule

The Desk publishes tentative schedules and post-operation results. In 2026 small-value operations continue for readiness; treat size accordingly.

## W11C-D07 — MSRB RTRS / EMMA
Primary:
https://www.msrb.org/Trade-Data
https://emma.msrb.org/tradedata

Most municipal trades are required to be reported within 15 minutes and transaction information is made public on EMMA / to subscribers shortly after receipt and automated checks.

Machine real-time subscription:
https://www.msrb.org/Market-Data-and-Research/Trade-Data-Subscriptions

As of 2025/2026 documentation, the real-time subscription is a paid product and supports web-service delivery.

## W11C-D08 — PJM Emergency Procedures
Primary:
https://www.pjm.com/

Research public alerts/emergency procedure state and load-management actions. Version exact emergency definitions over time.

## W11C-D09 — ERCOT Public Notices / EEA
Primary:
https://www.ercot.com/services/comm/mkt_notices/notices
https://developer.ercot.com/

ERCOT publishes public emergency notices and data products for EEA levels, reserve/scarcity and operating messages.

## W11C-D10 — Federal Reserve Mortgage-Convexity Evidence
Federal Reserve research:
https://www.federalreserve.gov/pubs/feds/2003/200349/200349pap.pdf

Historical evidence supports the mechanism that MBS duration/prepayment hedging can amplify movements in long-term rates. This is mechanism evidence, not proof that the proposed W11C signals currently earn alpha.

## Source-status rules

1. Preserve public-availability timestamps.
2. Version reporting rules by historical date.
3. Treat capped notionals as censored.
4. Record data/feed licensing separately from scientific validity.
5. Archive every mutable notice/feed version used in a backtest.
