# Wave 65D — Research Methods

Namespace: **W65D**

## W65D-M01 — Filing Acceptance Clock
Use SEC EDGAR acceptance/public time, not transaction date, unless the information was already public elsewhere.

## W65D-M02 — Debt Instrument Identity
Map each note/loan by issuer, principal, maturity, coupon/spread, currency and CUSIP/credit-agreement identifier where available.

## W65D-M03 — Maturity-Schedule Vintage
Never reconstruct historical maturity walls from the latest filing.

## W65D-M04 — Cash Availability Haircut
Restricted cash and liquidity unavailable under covenants do not count one-for-one.

## W65D-M05 — Revolver Commitment Semantics
Committed amount != drawable amount when borrowing-base/covenant limits bind.

## W65D-M06 — Item 2.03 Materiality Boundary
Item 2.03 captures material direct obligations under Form 8-K rules; absence is not proof no financing occurred.

## W65D-M07 — Item 2.04 Trigger Semantics
Trigger, cure, waiver and actual acceleration are distinct.

## W65D-M08 — Preliminary-vs-Final Offering
Preliminary marketing terms can change before final pricing.

## W65D-M09 — Benchmark-Time Alignment
New-issue spread/concession requires benchmark and TRACE comparables from the same pricing window.

## W65D-M10 — Curve Comparable Set
Match secondary bonds by:
seniority,
currency,
maturity/duration,
security/guarantee,
callability.

## W65D-M11 — TRACE Liquidity Control
Illiquid secondary issues can produce noisy concession estimates.

## W65D-M12 — Deal Settlement Confirmation
Pricing is not settlement. Preserve issue/settlement date.

## W65D-M13 — Proceeds Reality
Use final documents/filings to determine actual use of proceeds; announcement intent can change.

## W65D-M14 — Debt Retirement Confirmation
Do not assume refinancing proceeds retire old debt until redemption/tender/maturity/filing confirms.

## W65D-M15 — Tender Censoring
Tender results may be partial; track residual principal.

## W65D-M16 — Covenant Definition Fidelity
Financial covenant calculations use agreement-defined EBITDA/debt, not generic accounting metrics.

## W65D-M17 — Amendments as New Events
Every waiver, amendment and maturity extension is a distinct availability-time event.

## W65D-M18 — Market-Regime Control
Treasury yields, IG/HY spreads and issuance calendar affect concessions.

## W65D-M19 — Survivor Control
Include deals that were delayed, downsized or withdrawn when publicly observable.

## W65D-M20 — Intermediate Promotion Gate
Before equity alpha require OOS improvement in:
financing completion,
concession,
secondary spread,
covenant state,
liquidity runway,
or default/restructuring hazard.
