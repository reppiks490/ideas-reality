# Wave 10B — Research Methods

Namespace: W10B

## W10B-M01 — Release-Lag Mask
Weekly dealer data is not available until Thursday publication. Every observation uses publication time, not week-end date.

## W10B-M02 — FR2004 Regime Mapper
NY Fed reporting categories changed historically. Build explicit schema regimes and avoid naive concatenation.

## W10B-M03 — Duration-Equivalent Inventory
Convert maturity buckets to approximate duration/risk equivalents before aggregating.

## W10B-M04 — Inventory / Turnover Joint State
Position size alone is insufficient; condition on transaction velocity.

## W10B-M05 — Financing Sign Convention
Define repo/reverse-repo and borrowed/lent securities consistently from the dealer perspective.

## W10B-M06 — Fail Normalization
Normalize fails by transaction volume and outstanding market size.

## W10B-M07 — Specific-vs-General Collateral Decomposition
Use venue/issue data to separate collateral scarcity from cash-funding stress.

## W10B-M08 — Preliminary-vs-Final Repo Vintage
OFR preliminary daily series can revise. Store immutable preliminary vintages and later final validated values.

## W10B-M09 — Repo Holiday/Lag Calendar
Model one-day/two-day venue-specific data lags and government/market holidays.

## W10B-M10 — Venue-Migration Share
Analyze proportions as well as absolute volume because total repo size changes over time.

## W10B-M11 — Auction Expectation Model
Expected investor-class allotment must condition on tenor, auction type, size, refunding status, rate volatility and history.

## W10B-M12 — Auction Lifecycle
Announcement -> when-issued trading -> auction -> result -> settlement -> dealer inventory.

## W10B-M13 — Dealer Capacity Denominator
Estimate inventory/financing relative to balance-sheet proxies, not raw dollars only.

## W10B-M14 — H.8 Revision/Vintage Handling
Weekly bank series are revised and benchmarked. Preserve first release and revised history separately.

## W10B-M15 — Slow-Prior / Fast-Signal Fusion
SCOOS and Form PF are priors, not current observations. Their weight decays with age.

## W10B-M16 — Aggregate-Data Privacy Boundary
Never infer named hedge-fund positions from masked/aggregated Form PF data.

## W10B-M17 — Central-Clearing Breakpoint
Predefine implementation windows and re-estimate model relationships around rule-driven clearing migration.

## W10B-M18 — Margin-Call Stress Test
Simulate spread widening, haircut increases, volatility and basis moves against leverage/financing state.

## W10B-M19 — Flow Conservation Check
Repo borrowing/lending, dealer securities-in/out and cash flows must obey coherent balance-sheet signs.

## W10B-M20 — Cross-Market Promotion Gate
A dealer-plumbing feature must first explain Treasury/repo liquidity before being promoted as an NQ/ES signal.
