# Wave 55T — Source Notes

Namespace: **W55T**

## W55T-D01 — Treasury Auction Query
Primary:
https://www.treasurydirect.gov/auctions/auction-query/

Structured/downloadable auction history includes:
auction/issue/maturity dates,
offering amount,
bid-to-cover,
direct/indirect/primary dealer accepted/tendered,
SOMA fields,
CMB flag,
NLP thresholds and more.

## W55T-D02 — Treasury Auction Results
Primary:
https://www.treasurydirect.gov/auctions/announcements-data-results/announcement-results-press-releases/auction-results/

Treasury states auction results are updated in real time as results become available.

## W55T-D03 — Treasury Quarterly Refunding
Primary:
https://home.treasury.gov/policy-issues/financing-the-government/quarterly-refunding/most-recent-quarterly-refunding-documents/

Provides financing estimates, policy statements, auction schedules, buyback schedules, TBAC materials and primary dealer survey data.

## W55T-D04 — Quarterly Refunding Statements
Treasury refunding statements explicitly report:
gross securities offered,
privately held maturities refunded,
approximate new cash raised,
future auction sizes,
bill/CMB expectations,
TGA cash-balance assumptions,
buyback plans.

## W55T-D05 — Primary Dealer Auction Size Survey
Primary:
https://home.treasury.gov/policy-issues/financing-the-government/quarterly-refunding/quarterly-refunding-archives/primary-dealer-auction-size-survey

Use point-in-time survey expectations for auction-size surprise/disagreement.

## W55T-D06 — TBAC Financing Tables
Primary:
Treasury Borrowing Advisory Committee recommended financing tables and minutes.

Use as expectation/advice, not Treasury policy.

## W55T-D07 — NY Fed Treasury Rollover Policy
Primary:
https://www.newyorkfed.org/markets/treasury-rollover-faq

SOMA rollover bids are noncompetitive Treasury-auction add-ons equal to reinvested maturing SOMA holdings under applicable FOMC policy.

## W55T-D08 — NY Fed Primary Dealer Statistics
Primary:
https://www.newyorkfed.org/markets/counterparties/primary-dealers-statistics

Weekly series cover dealer positions, transactions, financing and fails; updated Thursday with previous week's data.

## W55T-D09 — NY Fed Securities Lending
Primary:
https://www.newyorkfed.org/markets/desk-operations/securities-lending

Daily operation results include CUSIP-level submitted/accepted lending demand and available/outstanding amounts.

## W55T-D10 — Treasury Buybacks
Primary:
Treasury quarterly buyback schedules, buyback FAQs and operation results.

Preserve operation type, maximum, accepted amount, maturity bucket, operation and settlement dates.

## W55T-D11 — 2026 Structural Changes
Treasury announced:
- 20-year reopening settlement moved to Friday of auction week beginning June 2026 to reduce repo specialness;
- long-end liquidity-support buyback maximums increased beginning September 9, 2026.

These create explicit backtest regime breaks.

## W55T-D12 — Existing ICARUS Cross-Layers
Fuse W55T with:
W17 market plumbing,
W27 volatility constraints,
W32 Reality Gap,
rates/curve data,
TGA/reserve/repo layers,
and NQ execution.

Do not duplicate connectors.
