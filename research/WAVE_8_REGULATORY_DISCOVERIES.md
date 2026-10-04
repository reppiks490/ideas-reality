# Wave 8R — Pre-Regulatory Warning & Safety Lifecycle Research

Namespace: **W8R**

Purpose: identify lawful, public, point-in-time warning signals that may precede or refine later regulatory, product-safety, clinical, or supply events.

These are hypotheses for Claude to test later. They are not claims of profitability and they do not modify ICARUS.

## W8R-E01 — NHTSA Complaint Hazard Field

Source:
NHTSA Office of Defects Investigation consumer complaint data/API.

Status:
LIVE public administrative data; official metadata describes daily updates.

Mechanism:
NHTSA explicitly uses consumer complaints with other information to identify safety issues that may warrant investigation and to determine whether a defect trend exists. Complaint acceleration may therefore be a lawful public precursor to a formal investigation or recall.

Candidate features:
- complaints / estimated installed fleet
- complaint acceleration vs age-cohort baseline
- component-specific complaint breadth
- unique ODI-case breadth
- crash/fire/injury/death severity weighting
- failure mileage distribution shift
- repeat occurrence intensity
- geographic dispersion/concentration
- narrative topic emergence
- complaint-source mix
- days since model launch / vehicle age

Hard rule:
Use NHTSA receive/add/public-availability timing, not the consumer's earlier incident date, for trading-information availability.

Priority: S-

## W8R-E02 — Complaint-to-Investigation Hazard Model

Sources:
NHTSA complaints + NHTSA defect investigations.

State transition:
NOISE
-> COMPLAINT_CLUSTER
-> PRELIMINARY/DEFECT INVESTIGATION
-> ENGINEERING ANALYSIS / PETITION / QUERY
-> RECALL or CLOSE_WITHOUT_RECALL.

Output:
probability and expected time to regulatory escalation.

Research target:
first predict formal NHTSA investigation opening. Only after that succeeds should Claude test issuer return or option-volatility effects.

Priority: S

## W8R-E03 — Investigation-to-Recall Conversion Surprise

Source:
NHTSA investigation files link investigations to resulting recall campaign numbers when applicable.

Candidate:
recall_probability_before_opening
vs
recall_probability_after_new_public_investigation_information.

Use:
- complaint count/severity
- affected models/years
- component
- prior manufacturer defect history
- investigation stage
- supplier/common-component graph
- investigation age.

The tradable information is the change in estimated recall probability, not the existence of an investigation alone.

Priority: A+

## W8R-E04 — Recall Scope Revision / Remedy Failure State

Sources:
NHTSA investigations, recall campaigns, recall complaints, manufacturer communications.

Mechanism:
A recall can fail to resolve the underlying defect or be too narrow, creating a later recall query, scope expansion, or remedy revision.

Candidate features:
- post-remedy complaint persistence
- complaints per repaired vehicle proxy
- same-component failures after remedy date
- new model-year spillover
- investigation/reopen/query transition
- recall completion vs complaint trajectory.

Priority: A+

## W8R-E05 — Common-Component Supplier Propagation Graph

Build:
component/part
-> supplier where publicly resolvable
-> OEM/model
-> affected population
-> public issuer.

Hypothesis:
A defect may surface first in one OEM but have economic implications for other manufacturers sharing the same component/platform/supplier.

Require explicit entity-resolution confidence; never infer supplier relationships from text similarity alone.

Priority: A

## W8R-E06 — ADAS/ADS Public Safety Incident State

Source:
NHTSA Standing General Order crash-report public datasets.

Status:
DELAYED/PERIODIC public data, not real-time.

Important source caveats:
- ADS and Level 2 ADAS reporting requirements differ
- records may be incomplete or unverified
- the same crash can have multiple reports
- some fields are redacted
- historical releases can be revised.

Research:
build manufacturer/system-normalized crash/severity trends and study whether public monthly releases alter regulatory-risk expectations.

Priority: B+

## W8R-E07 — FAA Service Difficulty Defect Cluster

Source:
FAA Service Difficulty Reporting System (SDRS).

Status:
PUBLIC processed reports; approval/QC delay applies.

Official data include:
- difficulty date
- aircraft make/model
- engine make/model
- part/JASC code
- problem description
- operational context
- component/part metadata.

Mechanism:
Clusters of repeated malfunctions/defects may precede broader service actions or Airworthiness Directives.

Hard rule:
Recently submitted reports are not public until FAA processing/approval. Availability time must be reconstructed independently of difficulty date.

Priority: A+

## W8R-E08 — SDR-to-Airworthiness-Directive Escalation Graph

Sources:
FAA SDRS + FAA Dynamic Regulatory System (DRS).

State transition:
isolated SDR
-> repeated component cluster
-> service/safety bulletin context
-> AD NPRM / immediate-adoption action where applicable
-> final Airworthiness Directive.

FAA DRS exposes searchable AD/NPRM metadata including issue date, citation publication date, manufacturer, model and product type; AD results can be exported.

Research target:
predict AD/NPRM opening or affected-product expansion before testing equity effects.

Priority: S-

## W8R-E09 — Aviation Component Cross-Fleet Risk

Graph:
part/engine/JASC component
-> aircraft models
-> fleet/operator exposure
-> manufacturer/supplier.

Candidate:
defect frequency normalized by exposed fleet/cycles where denominators can be obtained.

This can reveal whether an apparent OEM-specific issue is actually a shared engine/component problem.

Priority: A

## W8R-E10 — Clinical Trial State-Transition Surprise

Source:
ClinicalTrials.gov current API + official History of Changes/archived versions.

ClinicalTrials.gov records preserve successive posted versions with submitted dates and changed modules.

Candidate transitions:
- NOT_YET_RECRUITING -> RECRUITING
- RECRUITING -> ACTIVE_NOT_RECRUITING
- delayed primary-completion date
- enrollment revision
- site expansion/contraction
- sponsor/collaborator change
- outcome-measure revision
- arm/intervention revision
- termination/suspension/withdrawal
- results posting.

Priority: S for biotech/pharma research

## W8R-E11 — Trial Completion Delay Hazard

Build expected milestone dates from the public version available at each point in time.

Features:
- repeated primary-completion extensions
- enrollment pace proxy from registered enrollment/site/status revisions
- location additions/removals
- recruiting duration vs matched trials
- protocol revisions
- sponsor history
- indication/phase complexity.

Output:
probability distribution of milestone delay rather than a binary guess.

Priority: A+

## W8R-E12 — Protocol Revision Risk State

Not all registry changes are equal.

Research potentially informative revisions to:
- primary/secondary outcome measures
- enrollment target
- eligibility
- study design
- arms/interventions
- primary completion
- masking/allocation.

Negative control:
administrative/contact-only changes should not have the same weight.

Priority: A

## W8R-E13 — Trial Registry Reality Gap

Compare:
company-stated milestone expectations
vs
ClinicalTrials.gov point-in-time registered schedule/status.

Hypothesis:
persistent divergence may contain information about execution risk, but only if exact public timestamps and issuer-study mapping are defensible.

Priority: A+

## W8R-E14 — FDA Drug Shortage Supply Shock

Source:
openFDA Human Drug Shortages API.

Status:
LIVE public; FDA states its shortage list is updated daily.

Official searchable fields include:
generic/proprietary name,
company,
presentation,
availability,
shortage reason,
therapeutic category,
dosage form,
strength,
status,
initial posting,
update/change/resolved/discontinued dates.

Candidate:
shortage onset severity × manufacturer exposure × market share × substitutability.

Priority: A+

## W8R-E15 — Therapeutic Substitute Demand Graph

Graph:
short drug/API
-> therapeutic alternatives
-> substitute manufacturers
-> capacity constraints
-> affected hospitals/providers.

Research:
Does shortage onset transfer demand/pricing power to identifiable alternatives, and does the effect persist until resolution?

Must distinguish:
same molecule/generic substitution,
therapeutic substitution,
non-substitutable critical medicine.

Priority: S-

## W8R-E16 — Drug Shortage Resolution Half-Life

Model:
onset -> partial availability -> recovery -> resolved/discontinued.

Features:
- stated shortage reason
- manufacturer count
- dosage/strength breadth
- prior shortage history
- manufacturing/quality reason
- substitute availability
- update cadence.

Potential edge:
markets may price shortage onset faster than restoration duration.

Priority: A

## W8R-E17 — Medical Device Adverse-Event Hazard

Source:
openFDA device adverse-event / MAUDE-derived data.

Research:
severity- and exposure-normalized adverse-event acceleration by manufacturer/device/product code.

Important caveat:
published research documents substantial late manufacturer reporting in MAUDE, including reports more than six months after manufacturer awareness. Absence of reports is therefore not evidence of absence.

Use:
risk-state estimation, not naive event counting.

Priority: A

## W8R-E18 — Device Adverse-Event-to-Recall Lifecycle

Sources:
openFDA device event + device recall + enforcement APIs.

OpenFDA device recall data expose initiated/created/posted/terminated dates, firm, product code, reason, root cause and other identifiers; enforcement data add hazard classification and are updated on a scheduled basis.

State:
adverse-event cluster
-> firm action
-> recall initiation
-> FDA posting/classification
-> enforcement/termination.

Research:
estimate recall probability conditioned on publicly available event accumulation.

Priority: A+

## W8R-E19 — Regulatory Warning Truth Ladder

Cross-industry abstraction:

L1 raw public complaints / defect reports
L2 severity-normalized cluster
L3 regulator investigation / formal review
L4 proposed action
L5 recall / AD / shortage / clinical outcome
L6 realized financial impact.

Rule:
an earlier layer is valuable only if it predicts the next higher truth layer out of sample.

Priority: S research architecture

## W8R-E20 — Cross-Regulator Escalation Hazard Engine

Unify lifecycle methodology across:
NHTSA,
FAA,
FDA device,
FDA drug shortages,
ClinicalTrials.gov.

Do not pool effects blindly. Share statistical machinery while preserving regulator-specific timing, reporting rules and denominators.

Output:
calibrated probability of next public escalation state with uncertainty/abstention.

Priority: S architecture

## Highest-priority Wave 8R tests

1. W8R-E02 Complaint-to-Investigation Hazard
2. W8R-E08 SDR-to-AD Escalation
3. W8R-E10 Clinical Trial State-Transition Surprise
4. W8R-E11 Trial Completion Delay Hazard
5. W8R-E14 Drug Shortage Supply Shock
6. W8R-E15 Therapeutic Substitute Demand Graph
7. W8R-E18 Device Event-to-Recall Lifecycle
8. W8R-E19 Regulatory Warning Truth Ladder
9. W8R-E04 Recall Remedy Failure State
10. W8R-E20 Cross-Regulator Escalation Hazard Engine
