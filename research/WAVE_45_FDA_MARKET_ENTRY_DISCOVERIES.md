# Wave 45F — FDA Review & Market-Entry Clocks

Namespace: **W45F**

Thesis: a drug or biologic can move through a sequence of public regulatory states long before revenue is realized. Application review clocks, advisory-committee events, major-amendment extensions, approval/Complete Response outcomes, label scope, REMS, tentative approval, patent/exclusivity barriers, biosimilar/interchangeability state, and actual commercial launch all alter the probability and timing of market entry.

The research target is **regulatory-to-commercial conversion**, not a simplistic binary "FDA approval catalyst."

All candidates are research hypotheses only. Claude owns later implementation.

## W45F-E01 — Public PDUFA Goal-Date State
Application-specific goal dates are often first disclosed by the sponsor rather than through a universal FDA live calendar.

Use only:
SEC filings,
issuer releases,
or other primary public sponsor disclosure.

State:
GOAL_DATE_PUBLIC
GOAL_DATE_REVISED
GOAL_DATE_UNKNOWN.

Priority: S

## W45F-E02 — Standard vs Priority Review Clock
For NDA/BLA review:
encode the applicable PDUFA review class and rule vintage.

Current PDUFA VII goals generally include:
standard original NME NDA/BLA: 10 months from filing date,
priority original NME NDA/BLA: 6 months from filing date.

Priority: S-

## W45F-E03 — Filing-Date vs Receipt-Date Clock
For NME NDAs/original BLAs under the Program, the clock generally starts after the 60-day filing period; other submission types can use receipt date.

Do not infer a goal date from raw submission date without application class.

Priority: S methodology/edge hybrid

## W45F-E04 — Major-Amendment Extension
Late substantial submissions can extend the review clock under applicable PDUFA procedures.

State:
NO_PUBLIC_EXTENSION
EXTENSION_DISCLOSED
NEW_GOAL_DATE_PUBLIC.

Priority: S

## W45F-E05 — Advisory Committee Scheduled State
Primary source:
FDA advisory committee calendar + sponsor disclosure.

Track:
meeting date,
committee,
indication,
briefing-material release,
vote/recommendation,
meeting cancellation/postponement.

Priority: S-

## W45F-E06 — FDA Briefing-Document Shock
Compare sponsor narrative with FDA staff briefing documents once public.

Extract issue classes:
efficacy,
safety,
trial design,
manufacturing,
label,
REMS,
postmarketing requirements.

Priority: S

## W45F-E07 — Advisory Vote Surprise
Feature:
actual committee vote/recommendation
-
pre-meeting probability.

Use exact question wording; committee votes can address benefit-risk or narrower questions.

Priority: S

## W45F-E08 — Advisory Vote-to-Approval Conversion
Estimate:
P(approval / CRL | committee state, application class, issue type).

FDA is not bound by advisory committee votes.

Priority: S-

## W45F-E09 — Drugs@FDA Approval Action
Primary source:
Drugs@FDA / openFDA Drugs@FDA.

State:
APPROVED
TENTATIVE_APPROVAL
OTHER_ACTION.

Use public action date and application/submission number.

Priority: S

## W45F-E10 — Complete Response Letter State
Primary source:
FDA public Complete Response Letter database where available,
plus sponsor disclosures.

CRL means FDA will not approve the application in its current form.

Priority: S

## W45F-E11 — CRL Deficiency Taxonomy
Classify public deficiency categories:
clinical efficacy,
safety,
CMC/manufacturing,
facility inspection,
statistics,
labeling,
REMS,
other.

Priority: S

## W45F-E12 — CRL Remediation Complexity
Estimate remediation class:
DOCUMENT_ONLY
ANALYSIS
MANUFACTURING_REMEDIATION
ADDITIONAL_STUDY
NEW_PIVOTAL_TRIAL
UNKNOWN.

Priority: S

## W45F-E13 — Resubmission Class Clock
Class 1 vs Class 2 NDA/BLA resubmissions have different PDUFA goals under current commitments.

Track only when sponsor/FDA public information supports class.

Priority: S-

## W45F-E14 — Approval Label Scope
Compare approved label with expected/requested commercial scope:
population,
line of therapy,
biomarker,
age,
combination,
dose,
boxed warning/limitations.

Priority: S

## W45F-E15 — Label Compression Quotient
LCQ =
addressable patients under approved label
/
addressable patients under sponsor/base-case expectation.

Priority: S

## W45F-E16 — REMS Friction State
If approval includes REMS:
classify required controls and expected distribution/prescriber/patient friction.

Do not equate all REMS programs.

Priority: A+

## W45F-E17 — Postmarketing Requirement Burden
Track required/committed studies where public.

Potential value:
future regulatory cost/risk,
confirmatory-trial dependence,
label maintenance risk.

Priority: A

## W45F-E18 — Accelerated Approval Dependency
For accelerated approvals:
map surrogate basis,
confirmatory-study obligation,
later conversion/withdrawal status.

Priority: A+

## W45F-E19 — Manufacturing-Inspection Collision
Fuse W36P:
application is clinically approvable
but facility/CMC deficiencies block approval or launch.

Priority: S

## W45F-E20 — Approval-to-Launch Delay
Feature:
first approval date
-> first commercial availability.

Approval is not revenue realization.

Priority: S

## W45F-E21 — Launch Readiness
Estimate:
inventory,
distribution,
pricing/access,
manufacturing release,
controlled-substance scheduling where applicable,
payer coverage.

Only public, sourced components.

Priority: A+

## W45F-E22 — First Generic Approval
Primary source:
FDA First Generic Drug Approvals.

Track first approved generic entrant for a reference product/strength/form.

Priority: S-

## W45F-E23 — Tentative-to-Final ANDA Conversion
Tentative approval can precede final market eligibility because patents/exclusivities or other legal barriers remain.

State:
TENTATIVE
FINAL_APPROVED
LAUNCHED.

Priority: S

## W45F-E24 — Orange Book Entry Barrier
Use point-in-time Orange Book:
patents,
exclusivity codes,
expiration dates,
reference listed drug.

Model regulatory/legal barrier separately from approval status.

Priority: S

## W45F-E25 — 180-Day Generic Exclusivity State
Where public records support first-applicant/exclusivity eligibility:
track:
ELIGIBLE
TRIGGERED
FORFEITED
EXPIRED
UNKNOWN.

Do not infer from approval order alone.

Priority: S-

## W45F-E26 — Generic Competition Capacity
Estimate:
number of final-approved substitutable entrants
× launch status
× manufacturing capacity proxy.

Priority: S

## W45F-E27 — Purple Book Biosimilar State
Primary source:
FDA Purple Book.

Track:
reference biologic,
licensed biosimilar,
interchangeable designation where applicable,
licensure date.

Priority: S-

## W45F-E28 — Biosimilar Launch Barrier
Approval can precede launch due to patent settlement/litigation, manufacturing, contracting or market strategy.

Track approval and commercial availability separately.

Priority: A+

## W45F-E29 — Market-Entry Capacity Quotient
MECQ =
legally + regulatorily + operationally launchable capacity
/
addressable demand.

Priority: S

## W45F-E30 — Regulatory-to-Commercial Truth Ladder
APPLICATION
-> REVIEW CLOCK
-> ADVISORY/REVIEW SIGNALS
-> APPROVAL OR CRL
-> LABEL/REMS
-> LEGAL EXCLUSIVITY
-> MANUFACTURING
-> LAUNCH
-> UPTAKE.

Priority: S architecture

## Highest-priority W45F tests

1. W45F-E01 Public PDUFA Goal-Date State
2. W45F-E04 Major-Amendment Extension
3. W45F-E06 FDA Briefing-Document Shock
4. W45F-E10 Complete Response Letter State
5. W45F-E12 CRL Remediation Complexity
6. W45F-E14 Approval Label Scope
7. W45F-E19 Manufacturing-Inspection Collision
8. W45F-E20 Approval-to-Launch Delay
9. W45F-E23 Tentative-to-Final ANDA Conversion
10. W45F-E29 Market-Entry Capacity Quotient
