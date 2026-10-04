# Wave 51B — Research Methods

Namespace: **W51B**

## W51B-M01 — Court-Docket Primary Clock
Use the bankruptcy court docket entry/public document as primary legal-state timestamp where available.

## W51B-M02 — PACER Specific-Court vs Case-Locator
Specific-court PACER access can update in real time; nationwide Case Locator updates daily.

Preserve which source produced the event.

## W51B-M03 — PACER Cost/Access Gate
PACER is public but fee-bearing for many searches/documents.

Production architecture must respect account, billing and access rules.

## W51B-M04 — Mirror Completeness Gate
RECAP/claims-agent mirrors are secondary and can be incomplete or delayed.

Never infer no filing from mirror absence.

## W51B-M05 — SEC 8-K Secondary Clock
For SEC registrants, Item 1.03 filings are valuable public confirmation but may follow the court event.

## W51B-M06 — EDGAR Point-in-Time
Use EDGAR dissemination timestamp; data.sec.gov submissions history updates continuously after dissemination.

## W51B-M07 — Joint Administration != Substantive Consolidation
Do not merge debtor entities/claims merely because cases are jointly administered.

## W51B-M08 — Interim vs Final Order
Interim DIP/cash-collateral relief can differ materially from final order.

Version each separately.

## W51B-M09 — Budget Versioning
Archive each approved/revised budget and covenant/milestone schedule.

## W51B-M10 — DIP New Money vs Roll-Up
Separate incremental liquidity from refinancing/roll-up of prepetition debt.

## W51B-M11 — Claim Amount Uncertainty
Schedules, proofs of claim, objections and allowed claims are distinct states.

## W51B-M12 — Enterprise Value Vintage
Use valuation evidence available at each court stage; do not import later confirmed valuation backward.

## W51B-M13 — Priority/Collateral Legal Mapping
Recovery hierarchy depends on specific liens, guarantees, collateral and intercompany claims.

## W51B-M14 — Sale Order vs Closing
Court approval does not equal completed transaction.

## W51B-M15 — Plan Confirmation vs Effective Date
Keep confirmation order, conditions precedent and substantial consummation/emergence distinct.

## W51B-M16 — Equity Instrument Identity
Old equity, new equity, warrants and litigation/trust interests are different securities.

## W51B-M17 — Market Suspension / Delisting State
Track exchange delisting, OTC migration and trading halts separately from bankruptcy legal state.

## W51B-M18 — Distressed Security Survivorship
Preserve securities that stop trading; do not drop dead/delisted names from backtests.

## W51B-M19 — Event Family Deduplication
Court filing, company press release and SEC 8-K may report the same event.

Parent under one legal event with multiple public timestamps.

## W51B-M20 — Intermediate Promotion Gate
Before financial alpha, require OOS improvement in:
liquidity runway,
sale probability,
confirmation probability,
class recovery,
case duration,
or emergence outcome.
