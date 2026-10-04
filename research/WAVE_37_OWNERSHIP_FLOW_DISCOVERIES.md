# Wave 37O — Insider & Beneficial-Owner Flow

Namespace: **W37O**

Thesis: equity ownership changes by officers, directors, affiliates and large beneficial owners can contain information and create supply/demand pressure, but only when transaction type, plan state, ownership form and filing clock are modeled correctly. The target is not "insider sentiment"; it is point-in-time ownership-flow state with motive left unknown unless disclosed.

All candidates are research hypotheses only. Claude owns later implementation.

## W37O-E01 — Discretionary Open-Market Insider Purchase
Form 4 code-P acquisition, filtered for genuine cash open-market/privately negotiated purchase rather than award/exercise.
Priority: S

## W37O-E02 — Discretionary Open-Market Insider Sale
Form 4 code-S disposition not identified as Rule 10b5-1 and not mechanically linked to exercise/tax/estate transaction.
Priority: A+

## W37O-E03 — Rule 10b5-1 Planned Execution
Use Form 4/5 plan checkbox plus row-specific footnotes/adoption date.
Priority: S

## W37O-E04 — Planned-vs-Discretionary Flow Gap
Compare insider buy/sell notional after separating 10b5-1 and non-plan activity.
Priority: S

## W37O-E05 — Plan Adoption State
Primary source:
issuer Item 408(a) quarterly disclosures.
Track director/officer adoption/modification of Rule 10b5-1 or covered non-10b5-1 trading arrangement.
Priority: S-

## W37O-E06 — Plan Termination State
Track disclosed termination/modification and remaining expected plan horizon where terms are public.
Priority: A+

## W37O-E07 — Cooling-Off Completion Clock
For directors/officers under current Rule 10b5-1:
eligible execution no earlier than the later of 90 days after adoption/modification or two business days after disclosure of the issuer's financial results for the relevant quarter, capped at 120 days.
Priority: S-

## W37O-E08 — Plan Execution Deviation
Compare realized Form 4 transactions with disclosed aggregate plan amount/duration where available.
Priority: A

## W37O-E09 — Recurrent Routine-Sale Baseline
Model person-specific cadence/size to distinguish routine periodic selling from unusual flow.
Priority: S-

## W37O-E10 — Insider Purchase Cluster
Multiple independent officers/directors buying within a defined window.
Weight by role, size relative to compensation/holdings and transaction independence.
Priority: S

## W37O-E11 — Insider Sale Cluster
Multiple discretionary sellers normalized by each person's historical behavior.
Priority: A+

## W37O-E12 — Holding-Change Fraction
Net acquired/disposed shares / pre-transaction beneficial ownership.
Priority: S

## W37O-E13 — Direct-vs-Indirect Ownership
Separate direct holdings from trusts, LLCs, foundations, family entities and other indirect forms.
Priority: A

## W37O-E14 — Exercise-and-Sell Neutralization
Option exercise followed by same-day sale can reflect compensation/liquidity mechanics.
Decompose exercise acquisition from market disposition.
Priority: S methodology/edge hybrid

## W37O-E15 — Tax-Withholding / Award Neutralization
Separate award vesting and shares withheld/sold for tax obligations from discretionary market flow.
Priority: S methodology/edge hybrid

## W37O-E16 — Gift / Estate Transfer State
Treat gifts, trusts and estate-planning transfers separately from market purchase/sale.
Priority: A

## W37O-E17 — Form 4 Filing Lag
Feature:
EDGAR acceptance time - transaction execution time.
Most Form 4 changes are due within two business days.
Priority: A+

## W37O-E18 — Foreign-Private-Issuer Section 16 Expansion
From March 18, 2026, directors/officers of covered foreign private issuers with Section 12-registered equity became subject to Section 16 filing under the Holding Foreign Insiders Accountable Act.
Track coverage regime change.
Priority: S methodology

## W37O-E19 — Form 144 Proposed-Sale Intent
Electronic Form 144 identifies affiliate intent to sell restricted/control securities when Rule 144 filing thresholds are exceeded.
Priority: S-

## W37O-E20 — Form 144 Intent-to-Execution Conversion
Match proposed Form 144 sale with later Form 4/market execution where possible.
States:
PROPOSED
PARTIAL_EXECUTION
FULL_EXECUTION
NO_CONFIRMED_EXECUTION.
Priority: S

## W37O-E21 — Affiliate Sale Capacity
Rule 144 volume limitations and Form 144 proposed units create a potential supply envelope, not guaranteed flow.
Priority: A+

## W37O-E22 — 13D Initial Activist/Control-Intent Entry
Primary source:
Schedule 13D.
Detect new >5% beneficial owner subject to 13D, filed within current five-business-day deadline.
Priority: S

## W37O-E23 — 13D Amendment Velocity
Current rule generally requires material amendments within two business days.
Track ownership, purpose and plan changes.
Priority: S

## W37O-E24 — 13D Purpose-State Change
Normalize Item 4 intentions:
board/governance,
capital allocation,
M&A,
strategic alternatives,
ordinary investment,
other.
Use disclosed text, not inferred activism.
Priority: S-

## W37O-E25 — 13G Passive/QII Ownership State
Track large non-control beneficial ownership under category-specific 13G clocks.
Priority: A+

## W37O-E26 — 13G-to-13D Conversion
Transition from passive/qualified reporting into 13D/control-intent reporting.
Priority: S

## W37O-E27 — Beneficial Ownership Acceleration
Change in reported percentage/shares across 13D/G amendments normalized by free float.
Priority: S

## W37O-E28 — Large-Holder Exit Pressure
Detect material beneficial-ownership reduction and distinguish actual reported ownership drop from proposed sale.
Priority: A+

## W37O-E29 — Insider Flow × Issuer Flow
Fuse W37O with W32I:
company buying shares while insiders sell,
company issuing while insiders buy,
or aligned demand/supply.
Priority: S

## W37O-E30 — Insider/Owner Flow × Short Constraint
Fuse W33S borrow/short fragility with concentrated insider/owner buying or selling.
Priority: S-

## W37O-E31 — Ownership Flow / Free-Float Quotient
OFQ =
confirmed net insider/large-holder ownership change
/
tradable free float.
Priority: S

## W37O-E32 — Filing Surprise
Compare reported ownership-flow event with person's/entity's prior public pattern and known plan state.
Priority: S-

## W37O-E33 — Ownership Concentration State
Combine insider/director/officer, 13D/G and public float estimates to measure concentration and marginal float.
Priority: A+

## W37O-E34 — Ownership-Flow Truth Ladder
PLAN / PROPOSED SALE / BENEFICIAL-OWNER INTENT
-> EXECUTED TRANSACTION
-> CONFIRMED HOLDING CHANGE
-> FREE-FLOAT CHANGE
-> LIQUIDITY/SUPPLY EFFECT
-> PRICE EFFECT.
Priority: S architecture

## Highest-priority W37O tests
1. W37O-E01 Discretionary Open-Market Insider Purchase
2. W37O-E03 Rule 10b5-1 Planned Execution
3. W37O-E04 Planned-vs-Discretionary Flow Gap
4. W37O-E10 Insider Purchase Cluster
5. W37O-E20 Form 144 Intent-to-Execution Conversion
6. W37O-E22 13D Initial Entry
7. W37O-E23 13D Amendment Velocity
8. W37O-E26 13G-to-13D Conversion
9. W37O-E29 Insider Flow × Issuer Flow
10. W37O-E34 Ownership-Flow Truth Ladder
