# Wave 8M — Research Methods

Namespace: W8M

## W8M-M01 — Intent / Execution State Matching
Match Form 144 proposals to actual transactions using issuer, seller, class, quantity, timing and filing lineage. Preserve unmatched and partial cases.

## W8M-M02 — Proposed Supply Normalization
Normalize proposed shares by float, ADV, current seller stake and market capitalization.

## W8M-M03 — Same-Day EDGAR Clock
Use EDGAR acceptance/dissemination timestamps, not form signature date alone.

## W8M-M04 — 10b5-1 Plan-Age Control
Separate newly adopted, old-plan and non-plan proposals. Routine plans require different priors from discretionary sales.

## W8M-M05 — Sale-Opportunity Window
Form 144 creates an execution window rather than guaranteeing an execution tick. Evaluate hazards over the valid window.

## W8M-M06 — Cash-Flow Calendar Residual
For DTS line items model weekday, month-end, tax, benefit, holiday and fiscal-year seasonality before defining surprise.

## W8M-M07 — TGA / Reserve Sign Accounting
Write explicit balance-sheet signs for every Treasury cash/debt flow. Never use “TGA up/down” heuristics without flow decomposition.

## W8M-M08 — Weekend / Holiday Batch Adjustment
DTS can roll non-business-day activity into the next statement. Model batching explicitly.

## W8M-M09 — Debt Settlement Separation
Separate public-debt cash issuance/redemption from operating deposits/withdrawals.

## W8M-M10 — Cash-Futures Contract Mapping
Map physical grade, location, timing and delivery terms to the correct futures contract before computing basis.

## W8M-M11 — Thin-Cash-Market Robustness
Cash observations with tiny/no volume receive lower confidence. Missing quotes are not zero.

## W8M-M12 — Five-Minute Grid Time Alignment
Normalize ISO/RTO timestamps, dispatch intervals, settlement intervals, DST and publication delay.

## W8M-M13 — Congestion Graph Representation
Represent transmission constraints as network edges/nodes rather than one regional price average.

## W8M-M14 — Expected-Outage Absorption
Estimate spare generation/import/reserve capacity before assigning severity to an outage.

## W8M-M15 — Censored Notional Estimation
Public swap notionals may be capped/rounded. Treat capped observations as censored, not exact.

## W8M-M16 — SDR Cross-Repository Deduplication
Use UTI/UPI, timestamps, product fields and action/event types to avoid duplicate public swap records where possible.

## W8M-M17 — Swap Lifecycle Reconstruction
Handle NEW / MODIFY / CORRECT / CANCEL / TERMINATE records as one transaction lifecycle instead of independent trades.

## W8M-M18 — Public Dissemination Delay
Decision time begins when the SDR makes the record public, not swap execution time if a regulatory delay applies.

## W8M-M19 — Direction-Inference Abstention
If public fields do not reliably identify payer/receiver or customer/dealer direction, do not invent it. Research unsigned intensity/price impact instead.

## W8M-M20 — Structural Break Registry
Record reporting-rule changes, cap thresholds, UPI taxonomy changes, exchange/ISO market redesigns and Form 144 electronic-mandate changes as explicit regimes.
