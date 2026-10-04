# Wave 27V — Source Notes

Namespace: **W27V**

## W27V-D01 — Limit Up Limit Down Plan
Primary:
https://www.luldplan.com/

The Plan defines Tier classifications, rolling five-minute reference-price logic, price bands, Limit State and Trading Pause mechanics.

## W27V-D02 — LULD Reports / Amendments
Primary:
https://www.luldplan.com/plans
https://www.luldplan.com/plan-amendments
https://www.luldplan.com/studies

Version plan rules historically; 2026 includes ongoing amendments/monitoring material.

## W27V-D03 — Nasdaq Trading Halts
Primary:
https://www.nasdaqtrader.com/Trader.aspx?id=TradeHalts
https://www.nasdaqtrader.com/Trader.aspx?id=TradeHaltCodes

Public halt codes include LUDP/LUDS and market-wide circuit-breaker states.

## W27V-D04 — Cboe LULD / Halt Auction Rules
Primary:
https://www.cboe.com/document/tech-spec/document/technical-specifications/cboe-limit-updown-faq
https://www.cboe.com/document/tech-spec/document/technical-specifications/cboe-titanium-u.s.-equities-auction-process

Cboe documents five-minute LULD halt auctions, collar widening, extensions, and late-day Volatility Close handling for Cboe-listed securities.

## W27V-D05 — SEC Regulation SHO Rule 201
Primary:
https://www.sec.gov/rules-regulations/staff-guidance/trading-markets-frequently-asked-questions-7

Trigger is a >=10% decline from prior regular-session close; restriction applies remainder of day and following trading day, subject to exceptions.

## W27V-D06 — Nasdaq Short Sale Circuit Breaker List
Primary:
https://www.nasdaqtrader.com/Trader.aspx?id=RegSHO

Nasdaq publishes daily Rule 201 circuit-breaker files with symbols and trigger timestamps.

## W27V-D07 — Exchange Short-Sale Data
NYSE and FINRA publish short-sale/short-volume products of differing scope and latency.

Use source-specific coverage; exchange short volume is not total market short interest.

## W27V-D08 — Rule 201 Causal Evidence
Office of Financial Research Working Paper 23-08 uses the -10% threshold in a quasi-experimental design and reports reduced short-sale activity and changes in returns/liquidity around Rule 201.

Treat as mechanism evidence, not guaranteed current alpha.

## W27V-D09 — Options Substitution Evidence
Published research documents option-market responses and synthetic-short substitution around Rule 201 restrictions.

Use only to motivate tests; independently reproduce with current options data and point-in-time rules.

## W27V-D10 — Index / Futures Cross-Market Data
Use existing repo sources for NDX/SPX weights, QQQ/SPY, CME NQ/ES and options.

Do not duplicate connectors already specified in W26R/W1/W8M.
