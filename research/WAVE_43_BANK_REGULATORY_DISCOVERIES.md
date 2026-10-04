# Wave 43B — Bank Regulatory Constraint & Capital State

Namespace: **W43B**

Thesis: a bank's operating capacity can be legally constrained before ordinary earnings reveal the effect. Public enforcement actions, prompt-corrective-action directives, capital maintenance requirements, brokered-deposit restrictions, asset caps, growth/branch restrictions, dividend/share-repurchase conditions, and formal termination orders create explicit regulatory state transitions.

The research target is **legally constrained balance-sheet capacity and remediation progress**, not generic "regulatory risk."

All candidates are research hypotheses only. Claude owns later implementation.

## W43B-E01 — Formal Enforcement Entry
Primary sources:
FDIC ED&O,
OCC Enforcement Actions,
Federal Reserve enforcement releases.

State:
NONE
WRITTEN_AGREEMENT
CONSENT_ORDER
CEASE_AND_DESIST
PCA_DIRECTIVE
OTHER_FORMAL_ACTION.

Priority: S

## W43B-E02 — Enforcement Public-Lag
Store:
order effective/issued date,
first public regulator date,
first ingest.

FDIC ED&O is currently published monthly for the preceding month; other regulators have different timing.

Priority: S methodology/edge hybrid

## W43B-E03 — Asset-Cap Constraint
Extract explicit asset caps or required asset reduction schedules.

Feature:
permitted assets - current reported assets.

Priority: S

## W43B-E04 — Growth Restriction
Detect restrictions on:
asset growth,
new products,
new markets,
branching,
acquisitions,
subsidiaries.

Priority: S-

## W43B-E05 — Capital Distribution Constraint
Extract conditions/restrictions on:
dividends,
share repurchases,
other capital distributions.

Priority: S

## W43B-E06 — Capital Maintenance Requirement
Extract order-specific minimum capital/leverage requirements above ordinary regulatory minima.

Priority: S

## W43B-E07 — Numerical PCA Threshold Proximity
From point-in-time Call Reports, calculate distance to current PCA thresholds for:
Total RBC,
Tier 1 RBC,
CET1,
leverage,
and supplementary leverage where applicable.

Priority: S-

## W43B-E08 — Ratio-Only Classification Warning
Meeting numerical "well-capitalized" ratios is insufficient if the institution is subject to a qualifying capital order/directive.

Feature:
RATIO_WELL_CAPITALIZED
vs
LEGAL_WELL_CAPITALIZED_ELIGIBILITY.

Priority: S architecture

## W43B-E09 — Public PCA Directive State
Where a regulator publicly issues a prompt-corrective-action directive:
track effective date, required corrective actions, deadlines, and termination.

Priority: S

## W43B-E10 — Capital Restoration Plan Clock
For publicly known undercapitalized/PCA cases:
track statutory/order deadlines for capital restoration plans and subsequent milestones.

Priority: A+

## W43B-E11 — Brokered-Deposit Restriction State
FDIA Section 29 restricts less-than-well-capitalized institutions from brokered deposits; adequately capitalized institutions may seek an FDIC waiver under applicable rules.

State:
UNRESTRICTED
WAIVER_REQUIRED
RESTRICTED
PUBLIC_WAIVER_STATE_UNKNOWN.

Priority: S-

## W43B-E12 — High-Rate Deposit Restriction State
Track restrictions on offering rates significantly above prevailing rates where applicable under Section 29/FDIC rules.

Priority: A+

## W43B-E13 — Funding Replacement Pressure
Estimate:
restricted brokered/high-rate funding
/
liquid alternative funding capacity.

Potential substitutes:
core deposits,
FHLB,
Fed facilities,
wholesale secured funding,
capital.

Priority: S

## W43B-E14 — Consent-Order Deadline Vector
Extract every explicit deadline:
30d,
45d,
60d,
90d,
quarterly progress reports,
other milestones.

Priority: S

## W43B-E15 — Deadline Slippage / Extension
Track public written extensions, amended orders, missed disclosed milestones, and revised remediation dates.

Priority: S-

## W43B-E16 — Order Escalation
State transition:
informal/unknown
-> formal agreement
-> C&D/consent
-> PCA directive
-> stronger restriction.

Priority: A+

## W43B-E17 — Order De-escalation
Track:
amendment easing terms,
partial release,
termination,
replacement by narrower action.

Priority: S

## W43B-E18 — Termination Shock
Regulators publish formal termination of enforcement actions.

Feature:
termination of constraint
× estimated previously constrained capacity.

Priority: S-

## W43B-E19 — Regulatory Constraint Duration
Days from first public formal action to public termination/modification.

Priority: A+

## W43B-E20 — Restriction Severity Score
Weighted count of:
asset cap,
growth ban,
branch restriction,
capital requirement,
distribution restriction,
funding restriction,
management/governance remediation.

Do not assign weights without OOS validation.

Priority: A

## W43B-E21 — Capital Headroom under Order
effective capital headroom =
reported capital
-
max(regulatory threshold, order-specific requirement).

Priority: S

## W43B-E22 — Capital Depletion Velocity
Quarter-over-quarter change in effective headroom from:
losses,
RWA growth,
asset growth,
capital issuance/distribution.

Priority: S-

## W43B-E23 — Deposit Franchise Stress
Fuse:
Call Report deposit mix,
brokered-deposit dependence,
uninsured deposit share where publicly available,
funding costs,
regulatory funding constraints.

Priority: S

## W43B-E24 — Lending-Capacity Constraint
Estimate loan-growth capacity consistent with:
capital headroom,
asset cap/growth order,
funding availability,
liquidity.

Priority: S

## W43B-E25 — Branch / Market Expansion Optionality Loss
For banks with explicit branch/new-market restrictions:
estimate foregone planned expansion only from sourced public plans.

Priority: A

## W43B-E26 — Parent Source-of-Strength Requirement
Federal Reserve holding-company agreements can require parent financial/managerial support of subsidiary bank.

Track:
capital plan,
support obligations,
distribution restrictions at parent.

Priority: A+

## W43B-E27 — Cross-Regulator Constraint Graph
One bank/holding company may have FDIC/OCC/Fed/state actions simultaneously.

Create parent-child action graph and avoid double counting one remediation issue.

Priority: S

## W43B-E28 — Public Enforcement vs Financial Deterioration Gap
Compare regulator constraint state with:
capital,
liquidity,
asset quality,
earnings,
deposit flow.

Priority: S

## W43B-E29 — Capital Ratio Recovery without Order Termination
A bank can improve ratios while formal restrictions remain.

State:
FINANCIAL_RECOVERY
but
LEGAL_CONSTRAINT_ACTIVE.

Priority: S

## W43B-E30 — Order Termination without Full Earnings Recovery
Inverse:
formal order terminated
while profitability/asset quality remains weak.

Priority: A+

## W43B-E31 — Regulatory Capacity Quotient
RCQ =
legally usable growth/funding/distribution capacity
/
normal unconstrained capacity.

Priority: S

## W43B-E32 — Bank Regulatory Truth Ladder
FINANCIAL DETERIORATION
-> FORMAL ACTION
-> LEGAL RESTRICTION
-> REMEDIATION
-> TERMINATION
-> ACTUAL BALANCE-SHEET RECOVERY.

Priority: S architecture

## Highest-priority W43B tests

1. W43B-E03 Asset-Cap Constraint
2. W43B-E05 Capital Distribution Constraint
3. W43B-E08 Ratio-Only Classification Warning
4. W43B-E11 Brokered-Deposit Restriction State
5. W43B-E14 Consent-Order Deadline Vector
6. W43B-E18 Termination Shock
7. W43B-E21 Capital Headroom under Order
8. W43B-E24 Lending-Capacity Constraint
9. W43B-E29 Capital Ratio Recovery without Order Termination
10. W43B-E31 Regulatory Capacity Quotient
