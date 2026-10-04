# Wave 39F — Research Methods

Namespace: **W39F**

## W39F-M01 — 2026 Rule-State Contract
In 2026, the 2024 N-PORT monthly-public expansion is delayed to 2027/2028 and a 2026 proposal may change it again.

Backtests use the disclosure regime actually effective on each date.

## W39F-M02 — Public Filing Availability
Use EDGAR/public-dataset availability time, not portfolio month-end, as information time.

## W39F-M03 — Third-Month Public-Regime Handling
Under the current pre-amendment regime, public N-PORT dissemination is quarterly; do not assume every monthly report was public.

## W39F-M04 — Permanently Nonpublic Fields
Some N-PORT information remains nonpublic.

Never use regulatory-only fields in public-strategy backtests.

## W39F-M05 — As-Filed Data
SEC datasets are derived from registrant submissions as filed.

Preserve amendments and filing corrections point-in-time.

## W39F-M06 — Holding Identifier Resolution
Resolve CUSIP/LEI/ISIN/ticker/name changes with point-in-time identifiers.

## W39F-M07 — Fund/Series/Class Identity
Do not collapse registrant, series and share class.

Flows and holdings may live at different reporting levels.

## W39F-M08 — Flow Definition
Use N-PORT sales/redemptions definitions exactly, including omnibus/netting and exchange treatment.

## W39F-M09 — TNA Normalization
Normalize flows/exposures using contemporaneous reported net assets.

## W39F-M10 — Portfolio Staleness Model
Estimate turnover-driven uncertainty after disclosure.

A 60+ day old high-turnover fund should receive low current-position confidence.

## W39F-M11 — Non-Proportional Sale Model
Redemption does not imply proportional liquidation of every holding.

Estimate sale propensity by liquidity/strategy historically.

## W39F-M12 — Derivative Economic Exposure
Convert derivative terms into delta/duration/notional-equivalent risk where defensible.

Raw notional is not exposure.

## W39F-M13 — Margin Scenario Method
Use transparent standardized shocks and contract-specific sensitivities.

Report ranges rather than false precision.

## W39F-M14 — Repo Sign Convention
Distinguish repo borrowing from reverse-repo lending and collateral role.

## W39F-M15 — Securities-Lending Mapping
Borrower exposure, collateral received and reinvested cash collateral are distinct.

## W39F-M16 — Counterparty Name Normalization
Normalize legal-entity names/LEIs while preserving original filing text.

## W39F-M17 — Holdings Overlap Hierarchy
Use security-level overlap where identifiers permit; issuer-level only as separate coarser metric.

## W39F-M18 — Liquidity Cross-Source Join
Use TRACE/equity market data at the historical point in time, not current liquidity statistics.

## W39F-M19 — Survivorship Control
Include merged/liquidated funds and historical filings.

## W39F-M20 — Intermediate Promotion Gate
Before financial alpha require OOS improvement in:
fund outflow,
portfolio sale,
market depth consumption,
spread/price impact,
borrow recall,
or margin stress.
