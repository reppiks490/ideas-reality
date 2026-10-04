# Wave 25C — Research Methods

Namespace: **W25C**

## W25C-M01 — TRACE Public-Time Ledger
Store execution time, report/dissemination time, first ingest, correction/reversal time.

Execution time is not public availability time.

## W25C-M02 — Side Semantics
Interpret side from the reporting dealer's perspective exactly as FINRA defines it.

Customer sale means dealer buys from customer.

## W25C-M03 — Interdealer Double-Count Guard
Only one side of disseminated interdealer activity is represented under BTDS semantics.

Do not create synthetic two-sided flow.

## W25C-M04 — Contra-Party Taxonomy Versioning
Preserve dealer/customer/affiliate/ATS definitions by feed version.

## W25C-M05 — Censored Quantity Model
Trades above dissemination caps are interval-censored/lower-bounded.

Never replace "5MM+" with 5,000,000 as exact size.

## W25C-M06 — Correction/Reversal State
TRACE corrections/cancels/reversals must update the point-in-time ledger only when publicly disseminated.

## W25C-M07 — Bond Master Point-in-Time Join
Use security master effective at the timestamp for:
maturity,
coupon,
seniority/product,
144A/public status,
issue identifiers.

## W25C-M08 — Treasury-Curve Neutralization
Remove matched risk-free duration moves before calling a bond move issuer credit.

## W25C-M09 — Sector Credit Neutralization
Remove common sector/quality spread move to isolate issuer residual.

## W25C-M10 — Liquidity Adjustment
Control for bond age, issue size, trading frequency, maturity and market liquidity.

## W25C-M11 — Multi-Bond Hierarchical Model
Pool information across issuer bonds without pretending each issue is an independent observation.

## W25C-M12 — Same-Event Clock Alignment
For bond/equity/options lead-lag use synchronized public timestamps and realistic feed latency.

## W25C-M13 — Lead-Lag Anti-Snooping
Pre-register lag windows and apply multiple-testing control.

Do not mine hundreds of lags and report the winner.

## W25C-M14 — Ratings-Lag Gate
SEC Rule 17g-7 history files can be published long after rating action.

Use only at their public disclosure date for live-style backtests; use action date solely as retrospective label when explicitly allowed.

## W25C-M15 — Refinancing Exposure Vintage
Outstanding debt/maturity schedules must be point-in-time, not reconstructed from latest debt tables.

## W25C-M16 — Structural-Terms Parser
Calls, puts, conversion terms, guarantees, security and covenants need sourced versioned terms.

## W25C-M17 — Primary-vs-Secondary Trade Split
Primary fixed/list/takedown transactions have different reporting timing and economics from ordinary secondary trades.

## W25C-M18 — Market-Data Rights Gate
Tag real-time BTDS/144A and API products by subscription/redistribution rights.

Scientific validity does not imply production rights.

## W25C-M19 — Common-News Control
Scheduled macro/rates shocks can move both credit and equity.

Neutralize before claiming credit leadership.

## W25C-M20 — Intermediate Credit Promotion Gate
Before equity alpha, require OOS improvement in at least one:
future issuer spread,
liquidity deterioration,
rating transition,
refinancing outcome,
default/distress label,
or financing concession.
