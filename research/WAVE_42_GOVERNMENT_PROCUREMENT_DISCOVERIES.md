# Wave 42G — Government Procurement Award & Protest State

Namespace: **W42G**

Thesis: a federal contract award is not equivalent to economically usable backlog. A procurement can move through award, debriefing, protest, automatic performance stay, override, corrective action, reevaluation, resolicitation, court injunction, modification, termination and actual obligation/performance. These legal states can materially change the timing and probability of contractor revenue.

The research target is **award-to-performance conversion** and **legally blocked backlog**, not generic "government contract won" sentiment.

All candidates are research hypotheses only. Claude owns later implementation.

## W42G-E01 — Federal Award Announcement Pulse

Primary public sources:
SAM.gov award/opportunity notices where published,
issuer filings/releases,
agency award notices.

Normalize:
agency,
solicitation,
awardee,
amount ceiling/value,
contract type,
base/options,
period of performance,
public announcement time.

Priority: S-

## W42G-E02 — Award-to-Performance Conversion

State:
ANNOUNCED
AWARDED
PERFORMANCE_ALLOWED
PERFORMANCE_STAYED
PERFORMANCE_STARTED
MODIFIED
TERMINATED.

Target:
probability/timing that announced award becomes executable revenue/backlog.

Priority: S

## W42G-E03 — Debriefing Window State

Where a required debriefing applies:
track offered/concluded debriefing date when publicly disclosed.

This can alter the deadline for obtaining an automatic GAO stay.

Priority: A+

## W42G-E04 — GAO Protest Filing Pulse

Primary source:
GAO public Bid Protest Docket.

Fields can include:
protester,
agency,
solicitation number,
B-number,
filed date,
posted date,
due date,
decision date/status.

Priority: S

## W42G-E05 — Automatic CICA Stay Eligibility

FAR 33.104(c) generally requires suspension/termination of awarded-contract performance when GAO notice reaches the agency within:
10 days after award,
or 5 days after an applicable required debriefing date offered to the protester,
whichever is later.

Model exact procurement-specific rule version.

Priority: S

## W42G-E06 — Legally Blocked Backlog

Candidate:
probability award is under effective performance stay
× remaining contract value expected during stay horizon.

Do not equate total contract ceiling with near-term revenue.

Priority: S

## W42G-E07 — Stay Override State

FAR permits agency leadership to authorize continued performance despite protest under documented findings such as best interests or urgent/compelling circumstances.

State:
STAY_EXPECTED
STAY_ACTIVE
OVERRIDE_DISCLOSED
PERFORMANCE_CONTINUES.

Priority: S-

## W42G-E08 — Protest Decision Countdown

GAO generally resolves protests within 100 calendar days from filing; FAR also provides a 65-day express option.

Feature:
days to public due/decision deadline.

Priority: S

## W42G-E09 — Corrective-Action Transition

Many protests end without a merits decision because the agency voluntarily takes corrective action.

State:
PROTEST_OPEN
CORRECTIVE_ACTION
REEVALUATION
AMENDED_SOLICITATION
NEW_AWARD_PENDING.

Priority: S

## W42G-E10 — Sustain / Deny / Dismiss / Withdraw State

GAO outcomes:
SUSTAINED
DENIED
DISMISSED
WITHDRAWN
CORRECTIVE_ACTION / OTHER PROCEDURAL END.

Do not reduce all non-denials to "award lost."

Priority: S methodology/edge hybrid

## W42G-E11 — Protest Effectiveness Prior

Use historical GAO effectiveness/sustain statistics only as broad priors.

FY2025:
14% sustain rate among merits decisions,
52% effectiveness rate including relief via corrective action or sustain.

Condition by agency/procurement class rather than assume a universal 52%.

Priority: A

## W42G-E12 — Protester Relief Probability

Estimate:
P(material award change or relief | current protest state).

Inputs:
grounds where public,
agency,
procurement type,
incumbency,
timeliness/stay,
parallel protests,
corrective-action history.

Priority: S-

## W42G-E13 — Awardee Revenue-at-Risk Envelope

Estimate:
near-term expected revenue delayed/lost
under scenarios:
DENIED
CORRECTIVE_ACTION
SUSTAINED
OVERRIDE
RESOLICIT
TERMINATION.

Priority: S

## W42G-E14 — Multiple-Protester Crowding

One procurement can have multiple B-numbers/protesters.

Feature:
number of independent protests
× ground diversity
× filing sequence.

Avoid counting amended/supplemental filings as fully independent protests.

Priority: A+

## W42G-E15 — Protest Amendment Escalation

Track supplemental/amended protest grounds.

Question:
does case complexity or new record information increase resolution time or relief probability?

Priority: A

## W42G-E16 — Agency Report Clock

GAO FAQ states the agency generally provides its report within 30 days of protest filing unless case posture changes.

Use only as procedural state where public milestones are observable.

Priority: B+

## W42G-E17 — Protest Resolution Surprise

Feature:
actual outcome
-
model-implied outcome probability before public decision.

Use to study repricing at resolution.

Priority: S-

## W42G-E18 — Corrective Action without Award Loss

Corrective action can preserve the same awardee after reevaluation.

Separate:
TEMPORARY_UNCERTAINTY
from
ACTUAL_AWARD_TRANSFER.

Priority: A+

## W42G-E19 — Re-Award / Recompetition State

After corrective action:
track whether agency:
reevaluates existing proposals,
amends and requests revisions,
resolicits,
cancels,
or reaffirms original award.

Priority: S-

## W42G-E20 — USAspending Obligation Confirmation

Primary source:
USAspending API.

Use award/action records as downstream confirmation of actual federal obligations and modifications.

Important:
obligation timing/reporting is not identical to public award-announcement time.

Priority: S-

## W42G-E21 — Obligation Ramp

After performance becomes legally available:
measure cumulative obligations relative to:
contract value,
period of performance,
historical execution profile.

Priority: A+

## W42G-E22 — Award Modification Shock

Track:
funding increment,
option exercise,
scope change,
period extension,
ceiling increase/decrease,
deobligation where public.

Priority: S-

## W42G-E23 — Stop-Work / Suspension State

FAR clauses permit stop-work/suspension mechanisms in specified contracts.

Mark only when a public agency/issuer/court source confirms an actual order.

Priority: A+

## W42G-E24 — Termination for Convenience / Default

Separate:
TERMINATION_FOR_CONVENIENCE
TERMINATION_FOR_DEFAULT
PARTIAL_TERMINATION.

Estimate remaining backlog removed and settlement exposure.

Priority: S

## W42G-E25 — Court of Federal Claims Protest Escalation

Primary public source:
U.S. Court of Federal Claims public opinions/orders.

A procurement protest can move from GAO to COFC or arise directly there.

Court injunctive relief is distinct from GAO automatic-stay mechanics.

Priority: A+

## W42G-E26 — Injunction State

For COFC:
track public TRO/preliminary/permanent injunction orders when available.

State:
NO_PUBLIC_INJUNCTION
TRO
PRELIMINARY_INJUNCTION
PERMANENT_RELIEF
DENIED
DISSOLVED.

Priority: S-

## W42G-E27 — Protest-to-Performance Delay

Feature:
first award date
-> legally permitted/observed performance start.

This is the clean operational target.

Priority: S

## W42G-E28 — Incumbent Bridge-Contract Optionality

When protested recompete delays transition:
incumbent may receive bridge/extension work.

Research:
protest delay
-> incumbent extension probability/value.

Priority: S-

## W42G-E29 — Challenger Opportunity Transfer

If original award is stayed/corrected:
estimate which alternative bidders could receive award, using only public competitive-set evidence.

Priority: A

## W42G-E30 — Procurement Concentration Shock

Aggregate protested/stayed awards by:
agency,
program,
prime contractor,
mission segment,
fiscal quarter.

Question:
does one contractor have excessive near-term backlog exposed to unresolved procurement states?

Priority: A+

## W42G-E31 — Federal Backlog Quality

For public contractors:

quality_adjusted_backlog =
announced backlog
× probability_performance_allowed
× probability_funded
× schedule_realization_factor.

Priority: S

## W42G-E32 — Procurement Truth Ladder

SOLICITATION
-> AWARD
-> DEBRIEFING
-> PROTEST/STAY
-> RESOLUTION
-> OBLIGATION
-> PERFORMANCE
-> REVENUE.

Do not promote a contract headline directly to revenue without passing through the legal/operational layers.

Priority: S architecture

## Highest-priority W42G tests

1. W42G-E02 Award-to-Performance Conversion
2. W42G-E05 Automatic CICA Stay Eligibility
3. W42G-E06 Legally Blocked Backlog
4. W42G-E08 Protest Decision Countdown
5. W42G-E09 Corrective-Action Transition
6. W42G-E13 Awardee Revenue-at-Risk Envelope
7. W42G-E20 USAspending Obligation Confirmation
8. W42G-E27 Protest-to-Performance Delay
9. W42G-E28 Incumbent Bridge-Contract Optionality
10. W42G-E31 Federal Backlog Quality
