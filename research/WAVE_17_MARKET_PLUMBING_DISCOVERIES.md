# Wave 17P — Market Plumbing & Operational Integrity

Namespace: **W17P**

Thesis: financial markets can remain price-discovering while the infrastructure beneath them degrades. Payment, securities settlement, market-data, and venue disruptions can create nonlinear liquidity and execution risk. These states are more useful as operational regime/risk controls than as naive directional signals.

All candidates are research hypotheses only. Claude owns any later implementation.

## W17P-E01 — Federal Reserve Service Status Vector

Primary source:
Federal Reserve Financial Services Service Status.

Public service states include normal operations, service issue, and service disruption for systems including:
FedACH
FedNow
Fedwire Funds
Fedwire Securities
National Settlement
and other FRFS services.

Feature:
service
× severity
× onset
× duration
× simultaneous-service breadth.

Priority: S-

## W17P-E02 — Fedwire Funds Disruption State

Fedwire Funds is a mission-critical same-day final funds-transfer service.

Research:
service issue/disruption
× time of day
× Treasury settlement/payment calendar
× bank funding conditions.

Use first as an operational/liquidity-risk regime indicator.

Priority: S

## W17P-E03 — Fedwire Securities Disruption State

Research:
Fedwire Securities impairment
× Treasury/agency settlement window
× repo settlement/funding stress
× Treasury auction/settlement calendar.

Question:
Does degradation near critical settlement windows alter repo fails, dealer liquidity or Treasury microstructure?

Priority: S

## W17P-E04 — FedACH Delay State

FedACH disruptions can delay file distribution/settlement windows.

Research:
onset
window affected
acknowledgement delay
restoration
backlog completion.

Targets:
payment-operational exposure rather than intraday market direction.

Priority: A

## W17P-E05 — FRFS Cross-Service Contagion

State:
single-service issue
-> access-layer issue
-> multi-service disruption
-> restoration.

Candidate:
number/criticality of simultaneously degraded services.

Priority: A+

## W17P-E06 — Critical-Clock Proximity

Operational disruption severity should be conditioned on how close it is to:
Fedwire cutoff
NSS close
Treasury settlement
margin/payment deadlines
corporate payment windows.

Feature:
time_to_critical_cutoff.

Priority: S

## W17P-E07 — Operating-Hours Extension Signal

Federal Reserve continuity guidance allows operational extensions under qualifying conditions.

Research:
extension request/announcement
× affected service
× disruption duration
× settlement obligations.

An extension itself is a stress-management response, not necessarily failure.

Priority: A+

## W17P-E08 — FRFS Recovery Reconciliation State

Federal Reserve continuity guidance emphasizes reconciliation after a disruption before resubmitting certain messages.

Hypothesis:
"service restored" and "participants operationally caught up" are separate states.

Priority: A

## W17P-E09 — DTCC Settlement Rollover Event

Public DTCC Important Notices documented a June 29, 2026 DTC/NSCC settlement rollover after an operational incident involving erroneous participant trades and inability to complete settlement before NSS close.

Build state:
NORMAL
EXTENSION
FAILED_SAME_DAY_SETTLEMENT
ROLLOVER
NEXT_DAY_CATCHUP.

Priority: S

## W17P-E10 — Settlement Rollover Funding Burden

The June 2026 DTCC event led to:
unpaid net credit/debit balances overnight
and additional next-day NSCC Clearing Fund requirements related to extra unsettled guaranteed activity.

Research:
settlement rollover
-> overnight funding need
-> clearing-fund increase
-> dealer/broker liquidity response.

Priority: S

## W17P-E11 — DTCC Market-Disruption Rule Activation

Public Important Notices can identify formal activation of NSCC/DTC market-disruption/force-majeure rules.

Treat formal rule activation as a discrete operational regime change.

Priority: A+

## W17P-E12 — DTCC Client Incident vs Public Confirmation Gap

DTCC states client incident communications may be distributed through subscribed Availability and Incident notifications, with updates during disruptions.

Public Important Notices can confirm major events later.

Research:
client-only detection clock
vs
public-confirmation clock.

Hard rule:
public backtests cannot use client-only timestamps unless licensed/access was actually available.

Priority: S methodology/edge hybrid

## W17P-E13 — Nasdaq Market System Status State

Primary source:
Nasdaq Trader Market System Status.

Nasdaq publishes system-status messages and searchable historical status data.

Build:
affected market
affected service
onset/update/resolution
operational halt state.

Priority: A+

## W17P-E14 — Cboe System Status State

Primary source:
Cboe public system-status notices.

Normalize:
venue
asset class
service
degraded/unavailable/restored
event duration.

Priority: A

## W17P-E15 — Venue-Specific Operational Halt

Cboe/Nasdaq rules/notices support operational halts for technology/market infrastructure problems.

Research:
one-venue halt
× alternative venue liquidity
× NBBO fragmentation
× routing changes.

Priority: S-

## W17P-E16 — SIP Outage / Material Latency State

Exchange rules explicitly contemplate SIP outages/material latency.

Build:
SIP impairment
-> exchange routing/self-help changes
-> quote/trade visibility degradation
-> venue-specific halt/continuation.

Priority: S

## W17P-E17 — Market Data vs Execution Divergence

Separate failures affecting:
market data only
order entry
drop copy
post-trade
clearing
settlement.

Question:
Which combinations create the most dangerous false sense of normal market operation?

Priority: S

## W17P-E18 — Cross-Venue Operational Breadth

Feature:
number of major venues/services simultaneously impaired
weighted by market share/systemic role.

States:
LOCAL
MULTI_VENUE
SIP_WIDE
POST_TRADE_WIDE
SYSTEMIC.

Priority: A+

## W17P-E19 — Payment × Settlement Collision

Fuse:
FRFS disruption
+ DTC/NSCC/FICC operational stress
+ Treasury settlement calendar
+ margin/funding state.

Mechanism:
clearing obligations can become harder to settle precisely when payment rails are impaired.

Priority: S

## W17P-E20 — Trading Venue × Clearing Collision

Fuse:
exchange/SIP disruption
+ clearing/settlement stress.

Question:
Does a market-access event create more durable dislocation when post-trade infrastructure is also impaired?

Priority: A+

## W17P-E21 — Plumbing Recovery Half-Life

Measure:
first degraded status
first restoration
participant catch-up
normal settlement confirmation.

Do not define recovery as the first "green" status alone.

Priority: A+

## W17P-E22 — Operational-Risk Regime Gate

Use market-plumbing status primarily as:
position-size reducer
execution-quality gate
venue-selection constraint
model-confidence modifier.

Not every plumbing event should generate a directional trade.

Priority: S architecture

## W17P-E23 — Critical Infrastructure Dependency Graph

Graph:
exchange/SIP
-> clearing
-> settlement
-> payment rail
-> member/participant
-> asset class.

Purpose:
identify which operational event can actually propagate to the user's traded instruments.

Priority: A+

## W17P-E24 — Plumbing Stress Composite

Candidate:
FRFS severity
+ settlement exception
+ venue/SIP breadth
+ time-to-cutoff
+ funding stress
+ recovery lag.

Output:
NORMAL
DEGRADED
CRITICAL_WINDOW
SETTLEMENT_RISK
SYSTEMIC_OPERATIONAL_STRESS.

Priority: S

## Highest-priority W17P tests

1. W17P-E02 Fedwire Funds Disruption
2. W17P-E03 Fedwire Securities Disruption
3. W17P-E06 Critical-Clock Proximity
4. W17P-E09 DTCC Settlement Rollover
5. W17P-E10 Settlement Rollover Funding Burden
6. W17P-E15 Venue-Specific Operational Halt
7. W17P-E16 SIP Outage / Material Latency
8. W17P-E17 Market Data vs Execution Divergence
9. W17P-E19 Payment × Settlement Collision
10. W17P-E24 Plumbing Stress Composite
