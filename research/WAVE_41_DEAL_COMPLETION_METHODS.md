# Wave 41M — Research Methods

Namespace: **W41M**

## W41M-M01 — Public-Time Event Ledger
Store filing/event effective time, EDGAR/agency publication time and ingest time separately.

## W41M-M02 — HSR Confidentiality Gate
HSR filings are confidential under 15 U.S.C. 18a(h).

Never infer undisclosed filing content or status.

## W41M-M03 — Agency Silence Is Unknown
No FTC/DOJ press release does not mean:
no Second Request,
clearance,
or no investigation.

## W41M-M04 — HSR Rule-Version Ledger
Version:
waiting-period rules,
filing form regime,
early termination,
thresholds,
Second Request procedure.

## W41M-M05 — 2026 Form Vacatur State
Encode Feb. 12, 2026 vacatur and Mar. 19, 2026 denied stay exactly.

Do not apply 2025 updated-form requirements after reversion unless party voluntarily used them.

## W41M-M06 — Business-Day Calendar
Tender clocks use SEC-defined business days, not naive calendar-day subtraction.

## W41M-M07 — Tender Relief Eligibility
Before applying April 16, 2026 10-day relief, verify all conditions of the exemptive order.

Otherwise default to ordinary rule.

## W41M-M08 — Preliminary vs Definitive Proxy
PREM14A and DEFM14A are distinct states.

Do not treat preliminary meeting dates as final unless supported.

## W41M-M09 — S-4 Effectiveness
Stock consideration may require effective registration statement.

Filed/amended is not effective.

## W41M-M10 — Vote Threshold Reconstruction
Use state law/charter/agreement/proxy threshold actually applicable.

## W41M-M11 — Tendered vs Guaranteed Delivery
Keep validly tendered/not withdrawn shares distinct from guaranteed-delivery notices.

## W41M-M12 — Condition Waiver Semantics
Some conditions can be waived; others cannot.

Map waiver rights by party.

## W41M-M13 — Outside-Date Versioning
Every merger-agreement amendment that changes outside date becomes a new state.

## W41M-M14 — Financing Commitment Versioning
Archive debt/equity commitment amendments, expirations and conditionality.

## W41M-M15 — Multi-Jurisdiction Regulator Graph
Every approval source has its own public-time semantics.

Do not collapse all into "regulatory approval."

## W41M-M16 — Spread Decomposition
Separate:
deal risk,
time value/rates,
dividend differences,
borrow,
optionality,
FX where applicable.

## W41M-M17 — Break-Price Uncertainty
Market-implied completion probabilities are sensitive to assumed break price.

Use distributions/sensitivity bands.

## W41M-M18 — Competing-Bid Path
A wider spread is not necessarily higher break risk when interloper optionality exists.

## W41M-M19 — Historical Deal Selection
Include closed, broken, withdrawn, amended and competing-bid deals.

Avoid survivor datasets built only from completed transactions.

## W41M-M20 — Intermediate Promotion Gate
Before return alpha require OOS improvement in:
clearance,
vote,
tender success,
condition satisfaction,
closing date,
or break probability.
