# Wave 13H — Human Capacity & Communications Resilience

Namespace: **W13H**

Thesis: markets usually observe human-capacity loss after it reaches payrolls, sales, hospital utilization, production or earnings. Public administrative and infrastructure data can sometimes reveal the transition earlier: advance layoff notices, weekly unemployment claims, wastewater viral activity, and disaster communications-system degradation.

These are research hypotheses only. Claude owns any later implementation.

## W13H-E01 — WARN Forward Layoff Calendar

Primary framework:
U.S. Worker Adjustment and Retraining Notification Act plus official state workforce-agency WARN notice publications.

Federal WARN generally requires covered employers to provide 60 calendar days advance written notice for qualifying plant closings/mass layoffs, subject to coverage rules and exceptions.

Build point-in-time events:
- notice_received/publication
- announced layoff start
- affected workers
- closure vs reduction
- facility/city/county
- NAICS where provided
- subsequent revisions.

Key insight:
WARN can expose *planned future labor-capacity removal* before payroll data record it.

Priority: S-

## W13H-E02 — WARN Notice-to-Effective Compression

Feature:
effective_layoff_date - first_public_notice_date.

States:
NORMAL_ADVANCE
SHORT_NOTICE
RETROACTIVE/EXCEPTION
POSTPONED
CANCELLED/REDUCED
ACCELERATED.

Question:
Does unusually short notice correlate with higher operational distress or unplanned demand shocks?

Do not assume short notice means legal noncompliance; WARN contains exceptions.

Priority: A

## W13H-E03 — Workforce Shock Materiality

Candidate:
announced_workers_affected
/
estimated_local_or_company_workforce.

Enhance with:
facility role,
occupation mix where available,
revenue/production geography,
replacement labor availability,
remote-work feasibility.

Public-company mapping requires explicit entity resolution.

Priority: A+

## W13H-E04 — WARN Revision Velocity

State notices can be amended for:
worker count,
layoff schedule,
closure status,
location and timing.

Feature:
magnitude and direction of revision
× time remaining to effective date.

Hypothesis:
rapid upward revisions or repeated schedule changes may reveal deteriorating operating plans.

Priority: A

## W13H-E05 — Regional Layoff Cluster

Aggregate new WARN notices by:
county,
commuting zone,
state,
industry,
supplier cluster.

Normalize by:
employment base,
seasonality,
historical WARN coverage.

Goal:
detect localized labor-demand deterioration before monthly payroll estimates.

Priority: S-

## W13H-E06 — Supply-Chain Layoff Propagation

Graph:
anchor company/facility layoff
-> suppliers
-> logistics providers
-> local commercial demand
-> downstream employers.

Question:
Do layoffs cluster sequentially along known supply chains rather than merely by common macro exposure?

Priority: A+

## W13H-E07 — WARN-to-Claims Realization Gap

Fuse:
forward WARN scheduled layoffs
+ weekly state unemployment-insurance claims.

Expected claims from known layoffs
versus
actual new claims.

Interpretation:
actual claims above WARN-implied baseline may reveal hidden/smaller/unanticipated layoffs outside WARN coverage.

Priority: S

## W13H-E08 — State Claims Breadth / Depth Stress

Source:
U.S. Department of Labor weekly UI claims.

Recent Federal Reserve research constructs a labor-market stress indicator using the geographic breadth and depth of state-level claims acceleration.

Candidate state:
number/share of states with accelerating claims
× labor-force weight
× magnitude.

Use:
macro/labor regime and regional exposure.

Priority: S

## W13H-E09 — Advance-vs-Revised Claims Surprise

DOL weekly claims have an advance state reporting stage and subsequent revised reporting.

Research:
- advance state surprise
- revision direction
- revision breadth
- persistence.

Availability rule:
each vintage is a separate public information event.

Priority: A

## W13H-E10 — CDC Wastewater Respiratory Activity Field

Source:
CDC National Wastewater Surveillance System.

Status:
PUBLIC WEEKLY.

CDC reports national/state/site wastewater activity for respiratory viruses including SARS-CoV-2, Influenza A and RSV, with public dashboard data generally updated Friday using the previous week's data.

Features:
- viral activity level
- rate of change
- state breadth
- site agreement
- cross-pathogen burden
- population-weighted exposure.

Priority: A+

## W13H-E11 — Wastewater-to-Hospital Lead State

Empirical research using U.S. 2023–2024 data found SARS-CoV-2 wastewater levels often led hospitalization admissions by several days.

Research:
estimate pathogen-, state-, and season-specific lead distributions rather than hard-code one lag.

Output:
expected near-term hospitalization pressure.

Priority: A+

## W13H-E12 — Wastewater Workforce Absence Risk

Mechanism:
community disease burden can reduce effective labor supply through illness/absence.

Evidence:
research has linked COVID wastewater activity with health-related work absences; separate 2026 work finds community influenza wastewater can add information for predicting school attendance.

Candidate:
viral activity surprise
× local employment
× occupational physical-proximity / work-from-home exposure.

Critical:
do not assume influenza/RSV have the same labor effect as COVID; estimate each independently.

Priority: A

## W13H-E13 — Health-Capacity Exposure Graph

Graph:
sewershed/state viral activity
-> hospitals/health systems
-> employers/industries
-> high-contact workplaces
-> travel/retail/education.

First validate:
wastewater -> absenteeism / utilization.

Only later:
economic outcome -> market target.

Priority: A

## W13H-E14 — Disease-Wave Geographic Propagation

Track ordering of wastewater acceleration across states/regions.

Research:
origin/early regions
-> adjacency/travel-connected regions
-> national breadth.

Question:
Does propagation topology improve regional activity or healthcare-demand nowcasts?

Priority: B+

## W13H-E15 — FCC Disaster Communications Impairment

Source:
FCC Disaster Information Reporting System communications status reports during activations.

Status:
EVENT-DRIVEN public aggregate reports.

Public reports can contain:
- cell sites served/out
- percent out
- outage cause: damage / transport / power
- sites operating on backup power
- cable/wireline subscribers out
- PSAP/911 status
- broadcast station status.

Priority: S-

## W13H-E16 — Backup-Power Vulnerability Field

A site still operational on backup power is not equivalent to a healthy site.

Candidate:
backup_power_sites
/
served_sites

conditioned on:
storm duration,
restoration progress,
grid outage,
fuel/logistics access.

Hypothesis:
high backup-power dependence predicts risk of further communications degradation if utility restoration lags.

Priority: S-

## W13H-E17 — Communications Recovery Half-Life

FCC communications-status reports are event-driven. During some DIRS activations the FCC has issued daily updates, but daily cadence is not guaranteed; no report is UNKNOWN, not zero.

Measure:
peak cell-site outage
peak backup-power dependence
peak wireline/cable subscriber outage
50% recovery
90% recovery
PSAP normalization.

Use:
physical disaster-recovery state.

Priority: A+

## W13H-E18 — Outage-Cause Transition Matrix

Track cause mix:
POWER
TRANSPORT/BACKHAUL
PHYSICAL_DAMAGE
MULTIPLE/OTHER.

Mechanism:
different causes imply different recovery distributions.

Example:
power-dependent sites may recover rapidly after grid restoration; physical damage can persist longer.

Priority: A

## W13H-E19 — Communications Reality Gap

Fuse:
headline/disaster forecast severity
+ FCC observed telecom impairment
+ grid outage/load loss
+ Cloudflare/internet activity
+ nighttime-light loss.

Feature:
measured infrastructure disruption
-
narrative/forecast disruption.

Priority: A+

## W13H-E20 — Telecom × Cloud Continuity Graph

Fuse:
FCC communications impairment
+ public cloud-provider status
+ Cloudflare internet anomalies
+ power-grid stress.

Question:
Is a digital-service outage caused primarily by:
local access failure,
backhaul/transport,
power,
cloud provider,
or multi-layer contagion?

Priority: A+

## W13H-E21 — Human Capacity State Vector

Combine independent human-capacity measures:
FORWARD_LAYOFFS
WEEKLY_CLAIMS
DISEASE_ACTIVITY
ABSENCE_RISK
COMMUNICATIONS_ACCESS
TRANSPORT_ACCESS.

Purpose:
describe the economy's available workforce/operational capacity, not predict price directly.

Priority: S

## W13H-E22 — Announced vs Unannounced Labor Stress

Expected labor stress from public WARN notices
versus
claims/wastewater/operational data not explained by those notices.

Residual:
UNANNOUNCED_STRESS.

This may be a cleaner macro-nowcast feature than headline layoff counts.

Priority: S-

## W13H-E23 — Facility Shutdown Confirmation Stack

For a named facility with a WARN closure/reduction:
WARN notice
+ nighttime light
+ grid load
+ internet/telecom
+ rail/truck/port activity where relevant.

Goal:
distinguish announced capacity reduction from actual physical shutdown timing.

Priority: A

## W13H-E24 — Human-Capacity Shock Transmission

Research chain:
labor/health/communications shock
-> operational throughput
-> company/sector KPI
-> earnings expectation
-> price.

Promotion requires passing each intermediate link.

Priority: S research architecture

## Highest-priority W13H tests

1. W13H-E01 WARN Forward Layoff Calendar
2. W13H-E05 Regional Layoff Cluster
3. W13H-E07 WARN-to-Claims Realization Gap
4. W13H-E08 State Claims Breadth / Depth Stress
5. W13H-E10 CDC Wastewater Respiratory Activity
6. W13H-E12 Wastewater Workforce Absence Risk
7. W13H-E15 FCC Disaster Communications Impairment
8. W13H-E16 Backup-Power Vulnerability Field
9. W13H-E19 Communications Reality Gap
10. W13H-E21 Human Capacity State Vector
