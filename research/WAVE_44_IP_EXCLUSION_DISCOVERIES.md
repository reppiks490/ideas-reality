# Wave 44I — IP Exclusion & Import-Access State

Namespace: **W44I**

Thesis: intellectual-property enforcement can legally remove products from U.S. commerce even when manufacturing, shipping and customer demand remain intact. Section 337 investigations create explicit procedural states from institution through ALJ initial determination, Commission review, remedial order, presidential review, exclusion, settlement, redesign and rescission.

The research target is **product-access capacity under legal IP constraints**, not generic patent-news sentiment.

All candidates are research hypotheses only. Claude owns later implementation.

## W44I-E01 — Section 337 Investigation Institution

Primary source:
USITC Section 337 notices / EDIS.

State:
COMPLAINT
INSTITUTED
ALJ_ASSIGNED
HEARING_SCHEDULED
INITIAL_DETERMINATION
COMMISSION_REVIEW
FINAL.

Priority: S-

## W44I-E02 — Target-Date Clock

USITC must establish a target date within 45 days after institution.

Feature:
days to target date
and
target-date revisions.

Priority: S-

## W44I-E03 — ALJ Initial Determination Shock

Event:
public initial determination on violation/no violation.

Separate:
LIABILITY_FINDING
from
REMEDY_RECOMMENDATION.

Priority: S

## W44I-E04 — Commission Review State

The Commission can:
NOT_REVIEW
REVIEW_IN_PART
REVIEW_FULL
ADOPT
MODIFY
REVERSE.

Priority: S

## W44I-E05 — Remedy Probability Revision

After ALJ ID and Commission review notice:
estimate probability of:
NO_REMEDY
LIMITED_EXCLUSION_ORDER
GENERAL_EXCLUSION_ORDER
CEASE_AND_DESIST
COMBINATION.

Priority: S

## W44I-E06 — Limited Exclusion Capacity

For a limited exclusion order:
map named respondents/products/import pathways to estimated U.S. supply exposure.

Priority: S

## W44I-E07 — General Exclusion Capacity

General exclusion order can reach infringing articles beyond named respondents under statutory conditions.

Estimate:
addressable import share
× workaround/supplier substitution.

Priority: S

## W44I-E08 — Cease-and-Desist Domestic Inventory Constraint

A CDO can constrain post-import U.S. sale/distribution behavior of named parties.

Separate import exclusion from domestic inventory/channel restriction.

Priority: A+

## W44I-E09 — Presidential Review Clock

USITC remedial orders enter a 60-day policy review period delegated to USTR.

Feature:
days remaining in review.

Priority: S

## W44I-E10 — Bonded Entry State

During presidential review, subject goods may enter under bond as prescribed.

State:
ORDER_ISSUED
REVIEW_PERIOD_BONDED_ACCESS
FINAL_EXCLUSION
DISAPPROVED.

Priority: S

## W44I-E11 — Bond Severity

Commission sets bond amount for review period.

Feature:
bond % or unit amount
relative to
product gross margin / landed value.

Potentially changes economic feasibility before final exclusion.

Priority: A+

## W44I-E12 — Presidential Disapproval Shock

Event:
USTR disapproves remedial order for policy reasons.

Rare but high-impact state transition.

Priority: A

## W44I-E13 — Final Exclusion Effective Capacity Loss

After review expires without disapproval:
estimate legally unavailable import capacity.

Priority: S

## W44I-E14 — Settlement / License Exit

Investigation can terminate in whole/part through settlement/license agreement.

State:
ACTIVE
SETTLED_PARTY
LICENSED
TERMINATED_PARTIAL
TERMINATED_FULL.

Priority: S-

## W44I-E15 — Consent-Order Exit

USITC may terminate as to respondents through consent order without a violation finding.

Track obligations separately from settlement.

Priority: A+

## W44I-E16 — Respondent Breadth

Count named respondents and product families.

Do not equate respondent count with market share.

Priority: A

## W44I-E17 — Product Scope Expansion / Narrowing

Track amendments and Commission scope language:
products,
components,
modules,
downstream goods.

Priority: S-

## W44I-E18 — Domestic Industry Validation State

Section 337 patent cases require a domestic-industry showing.

Track public rulings on technical/economic prongs where material to remedy probability.

Priority: A

## W44I-E19 — Public-Interest Remedy Constraint

USITC considers public-health/welfare, competitive conditions, domestic production and consumers before remedy.

Create event state only from public Commission findings/submissions.

Priority: A

## W44I-E20 — Redesign Adjudication State

A respondent may redesign product to avoid infringement.

States:
REDESIGN_ANNOUNCED
REDESIGN_UNADJUDICATED
USITC_NONINFRINGEMENT_FINDING
CBP_PUBLIC_RULING_SUPPORT
DISPUTED.

Priority: S

## W44I-E21 — Redesign Escape Probability

Estimate:
P(commercially viable redesign avoids exclusion)
× redesign lead time
× certification/retooling cost.

Priority: S-

## W44I-E22 — Enforcement Proceeding State

After remedial order:
track public enforcement proceedings alleging violation of exclusion/CDO.

Priority: A+

## W44I-E23 — Civil-Penalty Exposure

USITC notes violations of Section 337 orders can carry substantial daily/value-based civil penalties.

Use exact current statutory/order terms.

Priority: A

## W44I-E24 — Order Rescission / Modification

Track:
rescission,
modification,
suspension,
termination
after patent invalidation, settlement, redesign or changed circumstances.

Priority: S-

## W44I-E25 — Federal Circuit Appeal State

USITC final determinations can be appealed to the Federal Circuit.

State:
NO_PUBLIC_APPEAL
APPEAL_PENDING
STAY/RELIEF
AFFIRMED
VACATED
REMANDED.

Priority: A+

## W44I-E26 — Exclusion vs Inventory Buffer

U.S. market impact depends on:
domestic inventory,
pipeline inventory,
alternative suppliers,
domestic production,
redesign.

Priority: S

## W44I-E27 — Product Revenue-at-Risk

For public respondent/brand:
estimate affected U.S. revenue
× exclusion probability
× substitution difficulty.

Require sourced product/geographic exposure.

Priority: S

## W44I-E28 — Competitor Transfer Capacity

Estimate how much excluded demand competitors can absorb.

Inputs:
product substitutability,
capacity,
channel access,
certifications,
switching cost.

Priority: S-

## W44I-E29 — Supplier Chain Propagation

Graph:
infringing component/product
-> importer/OEM
-> downstream device
-> retailer/customer.

Priority: A+

## W44I-E30 — Import-Access Reality Gap

Compare:
legal exclusion scope
vs
actual observed import/sales availability.

Possible explanations:
bonded review entry,
redesign,
licensed source,
inventory,
misclassification,
enforcement lag.

Priority: S

## W44I-E31 — Exclusion Capacity Quotient

ECQ =
legally constrained U.S. product capacity
/
available substitute + redesign + inventory capacity.

Priority: S

## W44I-E32 — IP Access Truth Ladder

COMPLAINT
-> INSTITUTION
-> ALJ ID
-> COMMISSION REVIEW
-> REMEDIAL ORDER
-> PRESIDENTIAL REVIEW
-> FINAL ACCESS STATE
-> REDESIGN/SETTLEMENT/RESCISSION
-> ACTUAL SALES/SHIPMENTS.

Priority: S architecture

## Highest-priority W44I tests

1. W44I-E03 ALJ Initial Determination Shock
2. W44I-E05 Remedy Probability Revision
3. W44I-E09 Presidential Review Clock
4. W44I-E10 Bonded Entry State
5. W44I-E13 Final Exclusion Effective Capacity Loss
6. W44I-E20 Redesign Adjudication State
7. W44I-E24 Order Rescission / Modification
8. W44I-E27 Product Revenue-at-Risk
9. W44I-E30 Import-Access Reality Gap
10. W44I-E31 Exclusion Capacity Quotient
