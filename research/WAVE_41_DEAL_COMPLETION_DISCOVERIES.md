# Wave 41M — Deal Completion & Regulatory Clocks

Namespace: **W41M**

Thesis: announced mergers and tender offers evolve through explicit legal, regulatory, financing, voting and contractual states. Those states create observable clocks that change completion probability and timing. The research target is the transition from signed agreement to satisfied closing conditions—not generic merger-arbitrage spread chasing.

All candidates are research hypotheses only. Claude owns implementation.

## W41M-E01 — Definitive Agreement State

Primary sources:
SEC Form 8-K, merger agreement exhibits, Schedule TO/14D-9, proxy/prospectus filings.

Normalize:
ANNOUNCED
SIGNED
AMENDED
TERMINATED
COMPLETED.

Priority: S

## W41M-E02 — Outside-Date Clock

Extract contractual outside/drop-dead date from the merger agreement.

Feature:
calendar/business days to outside date
conditioned on remaining closing conditions.

Priority: S

## W41M-E03 — Outside-Date Extension Optionality

Many agreements permit one or more extensions for regulatory or other specified reasons.

Model:
base outside date,
automatic extensions,
elective extensions,
maximum extended date.

Priority: S-

## W41M-E04 — Termination-Fee State

Extract:
target termination fee,
reverse termination fee,
expense reimbursement,
trigger conditions.

Use as contractual payoff/cost state, not completion guarantee.

Priority: A+

## W41M-E05 — Ticking Fee / Consideration Adjustment

Some transactions increase consideration or otherwise adjust economics as closing is delayed.

Track exact contractual formula and trigger dates.

Priority: A

## W41M-E06 — Public HSR Filing State

HSR filings themselves are confidential.

Only mark:
HSR_FILED
if a party publicly discloses filing/submission.

Never infer filing from transaction size alone.

Priority: S methodology/edge hybrid

## W41M-E07 — Initial HSR Waiting Clock

Current general structure:
ordinary HSR review normally carries a 30-calendar-day waiting period;
cash tender offers and certain bankruptcy transactions normally use 15 days.

Start clock only from a publicly supported filing/start date.

Priority: S

## W41M-E08 — HSR Early Termination Event

Primary source:
FTC Early Termination Notices database/API plus company disclosure.

Event:
waiting period terminated early.

FTC publishes granted early terminations.

Priority: S-

## W41M-E09 — Publicly Disclosed Second Request

A Second Request extends review and prevents closing until statutory conditions are met.

Mark only when:
party,
FTC/DOJ,
court filing,
or other reliable public source discloses it.

Priority: S

## W41M-E10 — Second-Request Compliance State

States:
SECOND_REQUEST_ISSUED
COMPLIANCE_IN_PROGRESS
SUBSTANTIAL_COMPLIANCE_DISCLOSED
SECOND_WAIT_RUNNING
SECOND_WAIT_EXPIRED/TERMINATED.

Do not infer substantial compliance from elapsed time.

Priority: S

## W41M-E11 — Second Waiting Clock

After substantial compliance:
ordinary transactions typically have an additional 30-day agency review period;
cash tender/bankruptcy transactions generally have 10 days after acquiring-person substantial compliance.

Agreements with the agencies can extend timing.

Priority: S-

## W41M-E12 — 2026 HSR Form Rule State

The HSR filing form changed materially:
updated form effective Feb. 10, 2025;
vacated by federal district court Feb. 12, 2026;
FTC appealed;
Fifth Circuit denied stay Mar. 19, 2026;
agencies reverted to accepting the prior form while also accepting voluntary updated-form submissions.

Encode form regime by date.

Priority: Infrastructure

## W41M-E13 — FTC/DOJ Challenge State

Primary:
public complaint,
motion for preliminary injunction,
administrative complaint,
DOJ civil complaint.

State:
NO_PUBLIC_CHALLENGE
CHALLENGE_FILED
INJUNCTION_PENDING
INJUNCTION_GRANTED/DENIED
APPEAL
RESOLVED.

Priority: S

## W41M-E14 — Remedy Negotiation / Consent State

Public remedy artifacts:
consent agreement,
proposed final judgment,
competitive impact statement,
divestiture package,
hold-separate order.

Priority: S-

## W41M-E15 — Divestiture Completion Clock

Where a public consent/judgment imposes divestiture deadlines:
track base deadline,
permitted extensions,
acquirer approval,
trustee appointment risk.

Priority: A+

## W41M-E16 — Shareholder Vote Clock

Primary:
PREM14A/DEFM14A,
S-4/proxy-prospectus,
special-meeting notices.

Extract:
record date,
meeting date,
approval threshold,
adjournment authority.

Priority: S

## W41M-E17 — Vote Outcome

Primary:
Form 8-K Item 5.07 and company release.

State:
APPROVED
REJECTED
ADJOURNED
WITHDRAWN.

Priority: S

## W41M-E18 — Proxy Review State

Separate:
PRELIMINARY_PROXY
SEC_COMMENT/AMENDMENT
DEFINITIVE_PROXY
VOTE_SCHEDULED.

SEC comment/review can add information and delay but does not itself imply deal failure.

Priority: A+

## W41M-E19 — Stock-Consideration S-4 State

For stock deals:
S-4 FILED
AMENDED
EFFECTIVE
STOP_ORDER/OTHER
PROXY_PROSPECTUS_MAILED.

Closing can require registration statement effectiveness.

Priority: S-

## W41M-E20 — Tender Offer Clock

Default Rule 14e-1 framework:
tender offers generally remain open at least 20 business days.

Track:
commencement,
scheduled expiration,
extensions,
withdrawal-right state.

Priority: S

## W41M-E21 — 2026 Ten-Day Equity Tender Relief

SEC April 16, 2026 exemptive order permits qualifying equity tender offers to use a 10-business-day minimum if specified conditions are satisfied.

State:
DEFAULT_20_DAY
QUALIFYING_10_DAY_RELIEF
OTHER_EXEMPTIVE_RELIEF.

Priority: S methodology/edge hybrid

## W41M-E22 — Tender Consideration / Size Amendment

Under Rule 14e-1 framework, changes in consideration or percentage sought generally require sufficient extension; the default rule specifies 10 business days for such changes, subject to current exemptive conditions where applicable.

Priority: S-

## W41M-E23 — Other Material Tender Amendment

SEC guidance generally evaluates required extension based on materiality; historical staff guidance often references about five business days for material changes other than price/percentage, but facts matter.

Do not hard-code five days as universal law.

Priority: A

## W41M-E24 — Target Tender Recommendation

Schedule 14D-9 / Rule 14e-2 target response:
ACCEPT
REJECT
NEUTRAL
UNABLE_TO_TAKE_POSITION
AMENDED.

Target response is generally required within 10 business days after commencement/awareness under applicable rules.

Priority: A+

## W41M-E25 — Tender Participation State

When public amendments disclose deposited/tendered shares:
estimate:
tendered eligible shares
/
minimum condition.

Keep guaranteed-delivery shares separate.

Priority: S

## W41M-E26 — Tender Condition Satisfaction

Track:
minimum tender,
regulatory,
financing,
MAE,
other offer conditions.

At expiration classify each as:
SATISFIED
WAIVED
FAILED
UNKNOWN.

Priority: S

## W41M-E27 — Financing Commitment Clock

Extract public:
debt/equity commitment,
bridge/term financing expiration,
conditions precedent,
funding risk.

Do not infer lender willingness beyond documents.

Priority: A+

## W41M-E28 — Acquirer Credit / Funding Stress

Fuse W25C/W38O:
acquirer bond/CDS/rates funding state
with financing needs.

Priority: A

## W41M-E29 — Multi-Regulator Approval Matrix

Depending on transaction:
state insurance/banking,
FCC,
FERC,
transport,
foreign competition,
sector regulators,
CFIUS if publicly disclosed.

Represent every approval separately with source/effective date.

Priority: S

## W41M-E30 — CFIUS Public-Disclosure Gate

CFIUS process is often nonpublic.

Only create transaction state when the parties or government publicly disclose:
filing,
clearance,
mitigation,
Presidential action,
withdrawal/re-filing.

Priority: Methodology

## W41M-E31 — Deal Litigation State

Track:
stockholder suits,
antitrust suits,
appraisal/material closing-condition litigation,
injunction requests.

Separate routine merger litigation from a genuine closing blocker.

Priority: A

## W41M-E32 — Competing Bid / Interloper State

State:
NO_PUBLIC_INTERLOPER
INDICATION
SUPERIOR_PROPOSAL
MATCH_RIGHT_RUNNING
AMENDED_DEAL
TERMINATION_FOR_INTERLOPER.

Extract match-right clocks from agreement.

Priority: S-

## W41M-E33 — Deal Spread State

For cash deal:
annualized/raw spread adjusted for:
time,
dividends,
borrow,
rates,
deal consideration changes.

For stock deal:
use exact exchange ratio and hedge basket.

Priority: S

## W41M-E34 — Market-Implied Completion Probability

Estimate probability from deal spread only after modeling:
break price distribution,
time value,
dividends,
borrow,
financing,
competing bid optionality.

Output interval, not a naive single-point probability.

Priority: S

## W41M-E35 — Options-Implied Deal Distribution

Where liquid options exist:
use skew/term structure to estimate close/break/timing distribution.

Control for broad volatility and earnings.

Priority: A+

## W41M-E36 — Target Credit Confirmation

Fuse target TRACE/CDS/bonds:
credit deterioration can reveal skepticism about completion or standalone stress.

Priority: A

## W41M-E37 — Regulatory Clock Revision

Feature:
today's expected regulatory-clearance date
-
prior expected date.

Updates driven by:
Second Request,
compliance,
remedy,
court schedule,
foreign approvals.

Priority: S

## W41M-E38 — Closing-Condition Completion Matrix

For each public condition:
NOT_STARTED
IN_PROGRESS
SATISFIED
WAIVED
FAILED
UNKNOWN.

Compute percent complete only as a descriptive metric; conditions are not equally important.

Priority: S

## W41M-E39 — Outside-Date Proximity Hazard

Estimate break/extension/closing hazard as deal approaches outside date with unresolved conditions.

Priority: S

## W41M-E40 — Completion Confirmation

Primary:
Form 8-K Item 2.01,
merger certificate/company release,
tender final results.

Do not mark COMPLETED from expected closing date alone.

Priority: S

## W41M-E41 — Break / Termination State

Primary:
8-K,
termination agreement,
court/regulatory action.

Classify:
regulatory break,
vote failure,
financing failure,
MAE/condition,
interloper,
mutual termination,
outside-date termination.

Priority: S

## W41M-E42 — Post-Break Standalone Repricing

Estimate break-price distribution from:
standalone fundamentals,
pre-deal price adjusted for market/sector,
deal synergies already priced,
new information since announcement.

Priority: A+

## W41M-E43 — Deal Completion Hazard Model

Time-varying hazard using only public states:
contract terms,
regulatory,
vote,
tender,
financing,
litigation,
market/credit confirmation.

Priority: S

## W41M-E44 — Deal Truth Ladder

SIGNED AGREEMENT
-> REQUIRED FILINGS
-> REGULATORY/VOTE/TENDER CONDITIONS
-> FINANCING/OTHER CONDITIONS
-> LEGAL CLEARANCE
-> CLOSING
or
-> TERMINATION.

No hidden HSR/CFIUS state may be invented.

Priority: S architecture

## Highest-priority W41M tests

1. W41M-E02 Outside-Date Clock
2. W41M-E09 Publicly Disclosed Second Request
3. W41M-E10 Second-Request Compliance State
4. W41M-E13 FTC/DOJ Challenge State
5. W41M-E16 Shareholder Vote Clock
6. W41M-E20 Tender Offer Clock
7. W41M-E25 Tender Participation State
8. W41M-E29 Multi-Regulator Approval Matrix
9. W41M-E38 Closing-Condition Completion Matrix
10. W41M-E43 Deal Completion Hazard Model
