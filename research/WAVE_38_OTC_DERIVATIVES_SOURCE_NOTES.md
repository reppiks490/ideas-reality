# Wave 38O — Source Notes

Namespace: **W38O**

## W38O-D01 — CFTC Part 43
Primary:
https://www.cftc.gov/LawRegulation/DoddFrankAct/Rulemakings/DF_18_RealTimeReporting/index.htm

Part 43 governs real-time public reporting of publicly reportable swap transaction/pricing data and includes rules for delays, anonymization, rounding and caps.

## W38O-D02 — CFTC Parts 43/45 Technical Specification
Primary:
CFTC Parts 43 and 45 Technical Specification.

The specification defines reportable data elements, public-dissemination flags, validation rules, UPI use, action/event types and dissemination metadata.

## W38O-D03 — CFTC Block / Cap Tables
Primary:
CFTC published Part 43 appropriate-minimum-block-size and cap-size files/tables.

Version by effective date.

## W38O-D04 — CME Repository Services
Primary:
https://www.cmegroup.com/market-data/repository/data.html

CME states public swap transaction/pricing data are posted on receipt unless subject to regulatory delay, with downloadable dated files. Direct-public-use and redistribution terms differ.

## W38O-D05 — DTCC Data Repository
Primary:
DTCC DDR public-price-dissemination services and current DDR rulebook.

DDR publicly disseminates CFTC swap and SEC security-based-swap PPD records subject to applicable caps/delays and prohibits party identification.

## W38O-D06 — SEC Regulation SBSR
Primary:
https://www.sec.gov/about/divisions-offices/division-trading-markets/security-based-swap-markets/security-based-swap-data-repositories

Regulation SBSR governs reporting and public dissemination of security-based swaps. Current registered SDRs include DDR, ICE Trade Vault and KOR under SEC orders.

## W38O-D07 — SEC SBS Public Cap Semantics
Current DDR rules state single-credit/narrow-based-credit SBS notionals of $5MM or greater are publicly capped at $5MM; other SBS capping/rounding follows applicable rules.

Version independently across repositories/rule changes.

## W38O-D08 — ANNA DSB UPI
Primary:
https://www.anna-dsb.com/

The Derivatives Service Bureau issues ISO 4914 Unique Product Identifiers and associated OTC-derivative reference data used in current regulatory reporting.

## W38O-D09 — ISDA SwapsInfo
ISDA publishes aggregate analyses using DTCC/CFTC/SEC public repository data for interest-rate and credit derivatives.

Use as coverage/reference validation, not as a substitute for raw public vintages.

## W38O-D10 — Existing Repo Cross-Sources
Fuse W38O with:
W25C TRACE credit,
W27V market constraints,
W32R RealityGap,
W33S short/settlement stress,
W22G gas transport,
W23T/W25R power scarcity,
W17P market plumbing.

Do not duplicate those connectors.
