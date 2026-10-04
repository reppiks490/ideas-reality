# Wave 51B — Bankruptcy & Court-Controlled Restructuring

Namespace: **W51B**

Thesis: once a firm enters Chapter 11, ordinary corporate finance is replaced by a court-supervised state machine. Cash collateral, DIP financing, first-day relief, asset sales, claim priority, plan voting, confirmation, conversion and emergence can mechanically change survival probability and recovery values before quarterly financial statements catch up.

The research target is not "bankruptcy = zero." It is the point-in-time evolution of enterprise value, liquidity runway and creditor/equity recovery under court authority.

All candidates are research hypotheses only. Claude owns any later implementation.

## W51B-E01 — Chapter 11 Petition State

Primary source:
PACER / bankruptcy court docket.

Event:
voluntary or involuntary petition / order for relief.

State:
PREPETITION
FILED
DIP_OPERATING
CONVERTED
DISMISSED
CONFIRMED
EMERGED.

Priority: S

## W51B-E02 — Petition-to-SEC Disclosure Lag

For SEC registrants:
compare court petition timestamp with Form 8-K Item 1.03 public filing time.

Priority: S-

## W51B-E03 — First-Day Relief Completeness

Track first-day motions/orders:
cash management,
wages,
critical vendors,
utilities,
insurance,
taxes,
customer programs,
cash collateral,
DIP financing.

Output:
OPERATIONS_SUPPORTED
PARTIALLY_SUPPORTED
LIQUIDITY_AT_RISK.

Priority: S

## W51B-E04 — Cash-Collateral Authorization State

A debtor in possession cannot freely use cash collateral absent lender consent or court authorization.

Track:
interim authorization
final authorization
budget
adequate-protection obligations
termination/default events.

Priority: S

## W51B-E05 — DIP Financing Size and Availability

Feature:
committed DIP
drawn DIP
roll-up component
new-money component
undrawn availability.

Priority: S

## W51B-E06 — DIP Runway

Estimate:
available liquidity
/
court-budget cash burn.

Priority: S

## W51B-E07 — DIP Milestone Compression

DIP orders can include milestones for:
sale process,
plan filing,
confirmation,
emergence.

Feature:
time to milestone
× execution risk.

Priority: A+

## W51B-E08 — Budget Variance

Where public:
actual receipts/disbursements
vs
approved DIP/cash-collateral budget.

Priority: A+

## W51B-E09 — Priming / Lien Dilution State

Track new liens/superpriority claims that may subordinate or dilute prepetition creditor recovery.

Priority: S-

## W51B-E10 — Adequate Protection Burden

Estimate:
cash payments
replacement liens
fees
other protection
relative to debtor liquidity.

Priority: A

## W51B-E11 — Restructuring Support Agreement State

Track:
RSA signed
support percentage by class
milestones
termination rights
amendments
support withdrawals.

Priority: S

## W51B-E12 — Prepack / Prenegotiated Certainty

State:
FREEFALL
PRENEGOTIATED
PREPACKAGED.

Research whether prepetition support shortens case duration and recovery uncertainty.

Priority: A+

## W51B-E13 — Claim Priority Waterfall

Construct:
administrative
DIP/superpriority
secured
priority unsecured
general unsecured
subordinated
preferred
common equity.

Priority: S architecture

## W51B-E14 — Recovery Waterfall Range

For enterprise-value scenarios:
estimate recoveries by class.

Do not assume face-value claims equal allowed claims.

Priority: S

## W51B-E15 — Secured-Coverage Ratio

Collateral value
/
secured claim + priming obligations.

Priority: S-

## W51B-E16 — Unsecured Recovery Implied State

Infer from:
plan consideration
credit bids
asset-sale proceeds
enterprise-value range
claims estimate.

Priority: S

## W51B-E17 — Equity Survival Probability

Estimate whether old equity:
cancelled
reinstated
receives warrants/new equity
retains residual value.

No blanket zero assumption.

Priority: S

## W51B-E18 — 363 Sale Process State

Track:
sale motion
bidding procedures
stalking horse
bid deadline
auction
sale hearing
sale order
closing.

Priority: S

## W51B-E19 — Stalking-Horse Bid Gap

Feature:
stalking-horse purchase price
vs
estimated going-concern/liquidation value.

Priority: A

## W51B-E20 — Auction Increment Surprise

If auction occurs:
winning bid
-
stalking-horse bid.

Priority: S-

## W51B-E21 — Credit-Bid Capacity

Secured lenders may use credit bids subject to case terms.

Estimate maximum practical credit-bid influence.

Priority: A

## W51B-E22 — Asset Sale Completion Risk

Sale order is not closing.

Track:
regulatory conditions,
financing,
assignment issues,
outside date,
closing confirmation.

Priority: A+

## W51B-E23 — Executory Contract Rejection Shock

Court-approved rejection/assumption of leases/contracts can alter:
store footprint,
supplier/customer relationship,
cash burn,
liability.

Priority: A+

## W51B-E24 — Store / Facility Closure Capacity Loss

Map rejected leases and closure motions to operating capacity.

Priority: S-

## W51B-E25 — Claims Bar-Date State

Track:
bar date,
scheduled claims,
filed proofs of claim,
late claims,
objections.

Priority: A

## W51B-E26 — Claims Inflation Surprise

Feature:
filed/asserted claims
-
initially scheduled/estimated claims.

Priority: S-

## W51B-E27 — Preference / Avoidance Recovery Optionality

Where public:
estimate potential estate recoveries from avoidance actions.

Treat as uncertain contingent asset.

Priority: B+

## W51B-E28 — Plan Filing State

Track:
plan filed
amended
disclosure statement filed
approved
solicitation begun.

Priority: S

## W51B-E29 — Class Voting Support

Where public:
accepted/rejected by class
voting participation
consenting claim amount.

Priority: S-

## W51B-E30 — Confirmation Probability

Estimate:
P(confirm by target date)
from:
class support,
objections,
feasibility,
valuation disputes,
milestone timing.

Priority: S

## W51B-E31 — Confirmation Order Shock

Court confirmation is a major legal-state transition.

Map recoveries and implementation conditions exactly.

Priority: S

## W51B-E32 — Effective-Date / Emergence Gap

Plan confirmation can precede actual effective date/emergence.

Track conditions precedent and closing requirements.

Priority: A+

## W51B-E33 — Conversion-to-Chapter-7 Hazard

Estimate:
P(conversion/dismissal)
from:
liquidity runway,
failed sale,
DIP default,
administrative insolvency,
plan failure.

Priority: S

## W51B-E34 — Administrative Insolvency Risk

If estate cannot pay administrative claims:
reorganization may fail despite positive gross asset value.

Priority: S-

## W51B-E35 — Bankruptcy Recovery Revision

Feature:
today's class recovery estimate
-
prior estimate
after each court event.

Priority: S

## W51B-E36 — Distressed Credit / Court Reality Gap

Fuse W25C:
bond/credit pricing
vs
court-implied recovery.

Priority: S

## W51B-E37 — Equity / Court Reality Gap

Compare equity market capitalization to court-implied residual/equity recovery.

Priority: S

## W51B-E38 — Bankruptcy Supplier Contagion

Map debtor obligations/customer role to:
critical suppliers,
customers,
landlords,
lessors,
lenders.

Priority: A+

## W51B-E39 — DIP Lender Opportunity State

Map participating lenders / backstop parties and economics:
fees,
OID,
roll-up,
exit financing
where public.

Priority: A

## W51B-E40 — Chapter 11 Truth Ladder

PETITION
-> FIRST-DAY LIQUIDITY
-> DIP/CASH COLLATERAL
-> OPERATING TRAJECTORY
-> SALE/PLAN
-> CLAIM WATERFALL
-> CONFIRMATION
-> EFFECTIVE DATE
-> REALIZED RECOVERY.

Priority: S architecture

## Highest-priority W51B tests

1. W51B-E03 First-Day Relief Completeness
2. W51B-E04 Cash-Collateral Authorization State
3. W51B-E06 DIP Runway
4. W51B-E07 DIP Milestone Compression
5. W51B-E14 Recovery Waterfall Range
6. W51B-E18 363 Sale Process State
7. W51B-E26 Claims Inflation Surprise
8. W51B-E30 Confirmation Probability
9. W51B-E35 Bankruptcy Recovery Revision
10. W51B-E36 Distressed Credit / Court Reality Gap
