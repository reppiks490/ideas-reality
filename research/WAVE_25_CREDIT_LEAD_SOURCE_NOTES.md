# Wave 25C — Source Notes

Namespace: **W25C**

## W25C-D01 — FINRA TRACE Corporate Bonds
Primary:
https://www.finra.org/filing-reporting/trace
https://www.finra.org/filing-reporting/trace/documentation

FINRA requires member firms to report eligible corporate-bond transactions to TRACE.

## W25C-D02 — TRACE Reporting / Dissemination Timeframes
Primary:
https://www.finra.org/filing-reporting/trade-reporting-and-compliance-engine-trace/trace-reporting-timeframes

For ordinary corporate-bond secondary transactions, FINRA documentation states reporting within 15 minutes and dissemination upon receipt for disseminated transactions, subject to rules/exceptions.

## W25C-D03 — BTDS 2026 Specification
Primary:
https://www.finra.org/sites/default/files/2026-02/BTDS_MOLDUDP_v5.1.pdf
https://www.finra.org/filing-reporting/trace/technical-specifications

BTDS disseminated fields include price, yield, quantity, execution date/time, side, reporting-party type, contra-party type, ATS-related information, modifiers and correction/reversal messages.

## W25C-D04 — TRACE Size Caps
FINRA currently documents transaction-size display caps of:
$5MM for investment-grade corporate bonds,
$1MM for non-investment-grade corporate bonds,
with larger observations disseminated as capped values.

Version rules historically.

## W25C-D05 — TRACE Corporate/Agency API
Primary:
https://www.finra.org/filing-reporting/trace/documentation

Use the version listed as current on FINRA's documentation page. Historical tests must use the specification/version effective on that date; do not freeze the repository to an older direct PDF when FINRA supersedes it.

API products include security master/daily lists and end-of-day market aggregates/sentiment/most-active/closing files. Access requires FINRA credentials/token under current specifications.

## W25C-D06 — TRACE 144A / Specialized Products
FINRA operates separate dissemination/data products for relevant 144A and other categories.

Do not infer identical transparency/rights from ordinary BTDS; check product-specific rule/feed.

## W25C-D07 — SEC NRSRO Rating History
Primary:
https://www.sec.gov/data-research/structured-data/rating-history-files-publication-guide

NRSROs must publish structured rating histories, but Rule 17g-7 disclosure can lag rating actions by 12 months for issuer-paid ratings and 24 months for others. Treat as delayed historical validation.

## W25C-D08 — Treasury/Risk-Free Curve
Use official Treasury/Federal Reserve market series or licensed Treasury transactions to duration-neutralize corporate bond moves.

## W25C-D09 — Credit/Equity Price-Discovery Literature
Academic literature documents cross-market information transmission between corporate bonds and equities, with leadership depending on information type, liquidity and distress state.

Use as mechanism evidence only; independently reproduce under current TRACE structure.

## W25C-D10 — Convertible Integration Evidence
Recent 2025 research using TRACE and institutional data finds convertible issuance is associated with stronger integration between issuers' straight-bond and equity markets.

Use to motivate W25C-E21/E22, not as proof of tradable alpha.
