# Wave 54C — Medicare Coverage, Coding & Reimbursement Reality

Namespace: **W54C**

Thesis: FDA authorization does not equal commercial access. A therapy, device or diagnostic can be legally marketable yet commercially impaired because Medicare coverage is absent, geographically fragmented, coding is unresolved, payment is inadequate, a temporary add-on expires, or utilization fails to appear in claims. Conversely, favorable coverage/coding/payment transitions can expand addressable demand before quarterly company results show it.

The research object is the full reimbursement truth chain:
FDA ELIGIBILITY
-> COVERAGE
-> CODE
-> BENEFIT CATEGORY
-> PAYMENT
-> PROVIDER ECONOMICS
-> CLAIM UTILIZATION
-> REALIZED REVENUE.

All candidates are research hypotheses only. Claude owns any later implementation.

## W54C-E01 — National Coverage Analysis State

Primary source:
CMS Medicare Coverage Database tracking sheets.

State:
NO_NCA
NCA_OPEN
PUBLIC_COMMENT
PROPOSED_DECISION
FINAL_DECISION
RECONSIDERATION.

Priority: S

## W54C-E02 — NCA Decision Clock

Track:
formal request accepted,
review initiated,
public-comment window,
proposed memo due,
expected completion date,
final decision.

Priority: S

## W54C-E03 — Proposed-to-Final Coverage Revision

Feature:
scope_final
-
scope_proposed.

Changes may occur in:
indication,
patient eligibility,
provider type,
setting,
evidence requirements,
noncoverage carve-outs.

Priority: S

## W54C-E04 — National Coverage Breadth Score

Encode final NCD as:
NATIONAL_COVERAGE
COVERAGE_WITH_EVIDENCE
NATIONAL_NONCOVERAGE
MAC_DISCRETION
MIXED/CONDITIONAL.

Priority: S

## W54C-E05 — Coverage With Evidence Development State

Primary source:
CMS CED NCDs and approved-study listings.

Track:
CED_ACTIVE
STUDY_ENROLLMENT
EVIDENCE_COMPLETE
RECONSIDERATION_OPEN
CED_REMOVED
CED_CONTINUES.

Priority: S-

## W54C-E06 — CED Evidence-Maturity Clock

Estimate time to evidence milestone from CMS-approved study plan / review date.

Priority: A+

## W54C-E07 — TCET Candidate State

Primary source:
CMS Transitional Coverage for Emerging Technologies pathway.

State:
NOT_NOMINATED
NOMINATED
ACCEPTED
EVIDENCE_PREVIEW
FDA_AUTHORIZED
NCD_OPEN
TRANSITIONAL_COVERAGE
LONG_TERM_DECISION.

Priority: S-

## W54C-E08 — TCET Coverage Timing

For accepted breakthrough devices:
measure FDA authorization -> NCD initiation -> finalized coverage.

CMS states a goal of finalizing a TCET NCD within six months after FDA market authorization for qualifying candidates.

Priority: A+

## W54C-E09 — Local Coverage Fragmentation

Primary source:
Medicare Coverage Database LCD data.

For product/service:
covered MAC jurisdictions
/
relevant Medicare FFS population or provider base.

Priority: S

## W54C-E10 — LCD Adoption Wave

Track one MAC's favorable LCD language propagating to other jurisdictions over time.

Priority: A+

## W54C-E11 — Draft-to-Final LCD Revision

Compare:
draft LCD
public comments
final LCD
effective coverage.

Priority: S-

## W54C-E12 — Final LCD Notice Clock

CMS guidance requires a minimum 45-day notice period between final LCD publication and effective date.

Feature:
days until coverage change becomes effective.

Priority: S

## W54C-E13 — LCD Reconsideration Optionality

State:
FINAL_ACTIVE
RECONSIDERATION_REQUESTED
RECONSIDERATION_ACCEPTED
DRAFT_CHANGE
FINAL_CHANGE
DENIED/NO_CHANGE.

Priority: A

## W54C-E14 — Coverage Geography Expansion Quotient

CGEQ =
newly covered Medicare FFS population
/
previously covered Medicare FFS population.

Priority: S

## W54C-E15 — HCPCS Application State

Primary source:
CMS HCPCS Level II process.

State:
NOT_FILED
FILED
PRELIMINARY
PUBLIC_MEETING
FINAL
EFFECTIVE.

Priority: S

## W54C-E16 — HCPCS Code Assignment Shock

Track:
new code,
code revision,
code deletion,
temporary code,
crosswalk.

Priority: S

## W54C-E17 — Coding Denial / Deferral Risk

Target:
P(no satisfactory code this cycle)
based on:
preliminary determination,
public comments,
prior cycle,
product similarity,
benefit-category uncertainty.

Priority: A+

## W54C-E18 — Preliminary-to-Final HCPCS Revision

CMS public meetings expose preliminary coding, benefit-category and payment determinations.

Feature:
final decision delta from preliminary.

Priority: S

## W54C-E19 — HCPCS Effective-Date Clock

CMS publishes complete quarterly code files with explicit effective dates.

Track:
final decision publication
-> file publication
-> effective date.

Priority: S

## W54C-E20 — Code Without Coverage Gap

State:
HCPCS_AVAILABLE
but
NO_NATIONAL/LOCAL_COVERAGE.

Priority: S

## W54C-E21 — Coverage Without Specific Code Gap

State:
COVERAGE_EXISTS
but billing depends on miscellaneous/NOC or imperfect coding.

Priority: S-

## W54C-E22 — Benefit Category Assignment

CMS may separately determine whether product/service fits a Medicare benefit category.

State:
ASSIGNED
NOT_ASSIGNED
UNCERTAIN
SETTING_LIMITED.

Priority: S

## W54C-E23 — Benefit-Category Reality Gap

FDA authorization + code can exist while Medicare statutory benefit category blocks payment.

Priority: S

## W54C-E24 — OPPS Status Indicator Transition

Primary source:
CMS quarterly OPPS Addendum A/B.

Track HCPCS status indicator, APC assignment and payment-rate changes by quarter.

Priority: S

## W54C-E25 — OPPS Payment Rate Shock

Feature:
new OPPS payment
-
prior payment

normalized by provider acquisition/procedure cost where observable.

Priority: S

## W54C-E26 — Device Pass-Through State

State:
APPLIED
PRELIM_APPROVED
EFFECTIVE_NEXT_QUARTER
ACTIVE
EXPIRING
EXPIRED.

Priority: S

## W54C-E27 — Pass-Through Approval Timing

CMS evaluates OPPS pass-through applications quarterly; fast-track approvals can become effective at the start of the next quarter.

Priority: A+

## W54C-E28 — Pass-Through Expiry Cliff

Estimate provider economics before/after separate pass-through payment ends and payment becomes packaged/otherwise repriced.

Priority: S

## W54C-E29 — New Technology APC State

Track:
application,
approval,
assigned APC,
payment rate,
migration to conventional APC.

Priority: A+

## W54C-E30 — NTAP State

Primary source:
CMS IPPS New Technology Add-On Payment.

State:
APPLIED
PENDING
APPROVED
CONTINUED
DISCONTINUED.

Priority: S-

## W54C-E31 — NTAP Approval / Discontinuation Shock

Use annual IPPS final-rule implementation files to identify technologies newly approved, continued or discontinued.

Priority: S

## W54C-E32 — Inpatient Reimbursement Cliff

Estimate:
DRG base payment
+ NTAP
vs
post-NTAP payment after expiration/discontinuation.

Priority: A+

## W54C-E33 — Part B ASP Payment State

Primary source:
CMS quarterly Medicare Part B Drug Payment Limit Files.

Track HCPCS-level:
payment limit,
NOC price,
effective quarter,
revisions.

Priority: S

## W54C-E34 — ASP Quarter-over-Quarter Shock

Feature:
current Medicare payment limit
-
prior quarter payment limit.

Priority: S

## W54C-E35 — ASP Revision Surprise

CMS may revise prior quarter files.

Archive file vintages and treat revised historical prices as later information.

Priority: A+

## W54C-E36 — NDC-to-HCPCS Mapping Change

Primary source:
CMS NDC-HCPCS crosswalks.

Track:
new mapping,
removed NDC,
code reassignment,
seasonal update.

Priority: A+

## W54C-E37 — Reimbursement Margin Proxy

Estimate:
Medicare payment
-
provider acquisition/admin cost proxy.

Goal:
provider economic incentive state, not manufacturer gross margin.

Priority: S-

## W54C-E38 — Payment Adequacy Threshold

Research whether procedure/drug adoption accelerates only once reimbursement exceeds a product-specific provider-cost threshold.

Priority: S

## W54C-E39 — Quarterly Claims Adoption Curve

Primary source:
CMS preliminary quarterly Part B/Part D spending-by-drug datasets where applicable.

Track:
beneficiaries,
claims,
utilization,
spending
after code/coverage/payment activation.

Priority: S

## W54C-E40 — Claims Maturity Adjustment

Starting in 2026, preliminary Part B quarterly files can be available about three months after the reporting quarter with >94% of records captured, but payment details are not fully final.

Model claim completion/maturity before interpreting acceleration.

Priority: S methodology/edge hybrid

## W54C-E41 — Coverage-to-Utilization Lag

Feature:
days/quarters from favorable coverage effective date
to
observable claims adoption.

Priority: S

## W54C-E42 — Code-to-Utilization Lag

Feature:
HCPCS effective date
to
claims inflection.

Priority: S

## W54C-E43 — Payment-to-Utilization Elasticity

Estimate:
change in utilization
/
change in provider reimbursement
after controlling indication, supply, launch and seasonality.

Priority: A+

## W54C-E44 — Reimbursement Without Adoption Gap

State:
coverage/code/payment all favorable
but claims utilization remains weak.

Potential explanations:
clinical friction,
site-of-care limitations,
supply,
training,
physician reluctance,
competing therapy,
patient access.

Priority: S

## W54C-E45 — Adoption Ahead of Coverage Gap

Observed utilization before broad formal coverage may identify:
commercial/private payer use,
local MAC coverage,
clinical trial use,
cash-pay/off-label pathways.

Do not infer Medicare adoption without payer evidence.

Priority: A

## W54C-E46 — Medicare FFS vs MA Blind Spot

CMS FFS coverage/claims data do not automatically represent Medicare Advantage coverage/utilization.

Maintain payer-population scope explicitly.

Priority: S methodology

## W54C-E47 — Product Revenue Addressability

Estimate:
covered eligible population
× coding/payment availability
× site-of-care capacity
× observed adoption probability.

Priority: S

## W54C-E48 — Provider Site-of-Care Economics

Compare reimbursement incentives across:
hospital outpatient,
physician office,
ASC,
inpatient
where product can be used.

Priority: S-

## W54C-E49 — Site-of-Care Migration

Coverage/payment changes can shift administration venue.

Track claims share by care setting where public data support.

Priority: A+

## W54C-E50 — Competitive Reimbursement Asymmetry

Compare products with similar indications:
coverage breadth,
code specificity,
payment amount,
pass-through/NTAP status,
site-of-care economics.

Priority: S

## W54C-E51 — Reimbursement Moat

A product with entrenched favorable coding/coverage/payment may have commercial protection even before clinical differentiation is reconsidered.

Measure persistence rather than assume permanence.

Priority: A+

## W54C-E52 — Reimbursement Cliff Calendar

Combine known future dates:
LCD effective dates,
HCPCS effective dates,
pass-through expiration,
NTAP discontinuation,
ASP new quarter,
NCA due dates,
CED review milestones.

Priority: S

## W54C-E53 — CMS Decision Surprise Score

Compare actual:
coverage,
coding,
benefit category,
payment
to prior publicly observable expectation.

Priority: S

## W54C-E54 — FDA-to-CMS Commercialization Gap

Fuse W45 FDA.

Feature:
FDA authorization achieved
but Medicare commercial stack incomplete.

Priority: S

## W54C-E55 — CMS-to-Revenue Reality Gap

Compare:
favorable reimbursement stack
vs
later reported product revenue / utilization.

Priority: S

## W54C-E56 — Reimbursement Truth Ladder

FDA AUTHORIZATION
-> COVERAGE
-> CODE
-> BENEFIT CATEGORY
-> PAYMENT
-> PROVIDER ECONOMICS
-> CLAIM UTILIZATION
-> COMPANY REVENUE.

Priority: S architecture

## Highest-priority W54C tests

1. W54C-E03 Proposed-to-Final Coverage Revision
2. W54C-E09 Local Coverage Fragmentation
3. W54C-E12 Final LCD Notice Clock
4. W54C-E18 Preliminary-to-Final HCPCS Revision
5. W54C-E20 Code Without Coverage Gap
6. W54C-E28 Pass-Through Expiry Cliff
7. W54C-E34 ASP Quarter-over-Quarter Shock
8. W54C-E39 Quarterly Claims Adoption Curve
9. W54C-E44 Reimbursement Without Adoption Gap
10. W54C-E54 FDA-to-CMS Commercialization Gap
