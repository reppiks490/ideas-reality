# Wave 12F — Source Notes

Namespace: **W12F**

## W12F-D01 — CBP Border Wait Times
Primary:
https://bwt.cbp.gov/
https://bwt.cbp.gov/ViewAllPorts

Official CBP help documentation describes public RSS/XML-style access in addition to the web interface.

Useful fields:
commercial General/FAST wait state, lanes open, maximum lanes, port hours/status, source update time.

Production note:
verify and archive the exact current machine-readable endpoint/schema rather than depending on undocumented third-party wrappers.

## W12F-D02 — BTS Border Crossing/Entry Data
Primary:
https://data.bts.gov/Research-and-Statistics/Border-Crossing-Entry-Data/keg4-3bc2
https://www.bts.gov/explore-topics-and-geography/geography/border-crossingentry-data

Fields:
port, state, border, month, measure and value for inbound trucks, trains, loaded/empty containers, vehicles/passengers/pedestrians.

Important latency:
BTS documentation says validated public data can become available months after the reference month. Use as historical baseline, not live state.

## W12F-D03 — USDA Livestock Mandatory Reporting API
Primary:
https://mpr.datamart.ams.usda.gov/
Official API user guide:
https://mpr.datamart.ams.usda.gov/LMPRS-API-User-Guide.pdf

LMPR exposes public JSON report data and publication timestamps. Official documentation includes report examples such as 5-Area Daily Weighted Average Direct Slaughter Cattle — Negotiated.

## W12F-D04 — USDA MyMarketNews API
Primary:
https://mymarketnews.ams.usda.gov/mymarketnews-api

Use for broader agricultural cash/auction/physical market reports and source metadata.

## W12F-D05 — CME Grain/Oilseed Price-Limit Rules
Primary:
https://www.cmegroup.com/articles/faqs/grain-oilseed-and-lumber-price-limit-faq.html
https://www.cmegroup.com/trading/price-limits.html

CME documents periodic resets, expanded-limit triggers, cross-product triggers and near-delivery removal rules.

## W12F-D06 — CME Livestock Price-Limit Rules
Primary example:
https://www.cmegroup.com/rulebook/CME/II/100/101/101.pdf

Use current chapter/rule version for Live Cattle/Feeder Cattle research. Do not generalize one product's rule to another.

## W12F-D07 — CME Position Limits / Rule 562
Primary:
https://www.cmegroup.com/rulebook/files/cme-group-Rule-562.pdf

The 2026 advisory documents spot/accountability limits and certificate/warehouse-receipt limits for certain CBOT commodities, including the next-business-day correction requirement when delivery creates excess certificate holdings.

## W12F-D08 — CME Market Regulation Notices
Primary:
https://www.cmegroup.com/notices/market-regulation.html

Use notices for exact announcement/effective dates of position-limit/accountability changes.

## W12F-D09 — CFTC DCM Rule Filings
Primary:
https://www.cftc.gov/IndustryOversight/IndustryFilings/index.htm

Use as regulatory confirmation/provenance for exchange rule changes.

## W12F-D10 — Livestock Cash/Futures Research Evidence
Use peer-reviewed/USDA research only as mechanism evidence.

Recent research using daily Livestock Mandatory Reporting data finds negotiated-market thinness is associated with poorer lean-hog cash/futures convergence. This motivates W12F-E09 but does not prove a tradable effect or transfer to cattle.
