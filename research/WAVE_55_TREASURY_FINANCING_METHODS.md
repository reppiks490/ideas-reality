# Wave 55T — Research Methods

Namespace: **W55T**

## W55T-M01 — Announcement/Auction/Settlement Clocks
Store announcement, bidding close, result-publication, issue/settlement and maturity separately.

## W55T-M02 — Real-Time Result Clock
TreasuryDirect states auction results pages update on a real-time basis as results become available.

Capture actual first-seen timestamp.

## W55T-M03 — Security Identity
Use CUSIP + issue date + maturity + reopening status.

## W55T-M04 — New Issue vs Reopening
Model separately; reopenings add to existing CUSIP and can have different repo specialness.

## W55T-M05 — Gross vs Private New Cash
Never use offering amount alone as private financing drain.

## W55T-M06 — SOMA Add-On Treatment
SOMA rollovers are noncompetitive add-ons to announced auction sizes and should not be counted as private-sector absorption.

## W55T-M07 — Privately Held Maturity
Use Treasury-reported privately held maturing amount or reconstruct carefully.

## W55T-M08 — Settlement-Date Aggregation
Liquidity impulse belongs on cash settlement date, not only auction date.

## W55T-M09 — CMB Flag
Treasury Auction Query exposes a Cash Management Bill field; preserve separate from regular bill issuance.

## W55T-M10 — Bidder Category Semantics
Primary, direct and indirect categories follow Treasury definitions.

Indirect != foreign.

## W55T-M11 — Bid-to-Cover Limit
Bid-to-cover can look strong due to bidding behavior/auction mechanics; evaluate with allocation shares and tail.

## W55T-M12 — When-Issued Source Discipline
Tail/stop-through requires point-in-time WI market data immediately before results.

Do not reconstruct from end-of-day yields.

## W55T-M13 — Macro Announcement Exclusion
Control auctions near CPI, payrolls, FOMC and major fiscal headlines.

## W55T-M14 — Primary Dealer Weekly Lag
NY Fed dealer statistics update Thursdays for the previous week.

Do not treat as same-day dealer inventory.

## W55T-M15 — Dealer Bucket Mapping
Map dealer position series to auction maturity with documented maturity-bucket definitions.

## W55T-M16 — Securities-Lending Specialness
Fed lending demand is a proxy for scarcity/specialness, not the private repo rate itself.

## W55T-M17 — Buyback Scheduled vs Accepted
Tentative maximum amount != actual accepted amount.

## W55T-M18 — Buyback Type Split
Separate liquidity-support from cash-management operations.

## W55T-M19 — Buyback Cash Accounting
Treasury buyback settlement consumes Treasury cash but can be funded by other issuance; model net system effect, not one-sided injection.

## W55T-M20 — TGA Flow Causality
TGA changes reflect taxes, spending, issuance, redemptions and other flows.

Do not attribute entire change to auctions.

## W55T-M21 — Quarterly Refunding Vintage
Archive financing estimate Monday release, Wednesday policy statement, auction schedule and later updates.

## W55T-M22 — Regime-Break Ledger
Preserve changes in auction sizes, settlement conventions, buyback limits, Fed reinvestment policy and market structure.

## W55T-M23 — Duration Normalization
Convert face-value issuance to DV01/duration exposure using contemporaneous security characteristics.

## W55T-M24 — NQ Mechanism Gate
Before claiming NQ alpha, validate intermediate:
auction pricing,
yield response,
repo/funding,
dealer inventory,
curve movement.

## W55T-M25 — Orthogonal Promotion Gate
A Treasury edge must add OOS information beyond:
macro releases,
yield level,
term premium proxies,
VIX/rates vol,
known auction calendar.
