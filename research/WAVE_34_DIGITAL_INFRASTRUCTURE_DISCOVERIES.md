# Wave 34D — Digital Infrastructure Outage & Dependency Propagation

Namespace: **W34D**

Thesis: cloud, CDN, DNS, routing and authentication failures can remove digital operating capacity even when physical facilities remain intact. The useful signal is not "provider status is red"; it is the propagation path from provider incident to independently observed network impairment to customer-visible service loss and finally to economically material business interruption.

All candidates are research hypotheses only. Claude owns later implementation.

## W34D-E01 — Provider Public Incident Pulse
Normalize official public incidents from AWS, Azure, Google Cloud, Cloudflare and other verified infrastructure providers.
Fields:
provider,
service,
region,
severity,
first-public time,
provider-stated start time,
status,
last update.
Priority: S

## W34D-E02 — Provider Acknowledgement Lag
Feature:
first-public provider incident time - independently detected anomaly time.
Question:
does external telemetry reliably lead provider acknowledgement?
Priority: S

## W34D-E03 — Incident Update Velocity
Count state/text updates per unit time and classify:
INVESTIGATING
IDENTIFIED
MITIGATING
RECOVERING
RESOLVED
PIR.
Priority: A+

## W34D-E04 — Region-Service Blast Radius
Estimate affected combinations of:
region,
availability zone,
service,
feature,
control plane,
data plane.
Priority: S

## W34D-E05 — Control-Plane vs Data-Plane Failure
Deployment/API/console failures can differ materially from serving/data-path failures.
Preserve this distinction.
Priority: S

## W34D-E06 — Identity / Authentication Dependency Shock
IAM, identity, token, directory or login impairment can block many otherwise healthy services.
Priority: S-

## W34D-E07 — DNS / Naming Dependency Shock
DNS and service-discovery failures can propagate broadly despite healthy underlying compute.
Priority: S

## W34D-E08 — Storage / Database Dependency Shock
Classify stateful service failures separately because downstream recovery may lag network restoration.
Priority: A+

## W34D-E09 — Network Fabric Impairment
Provider-reported connectivity, packet-loss, routing or load-balancer impairment.
Priority: S

## W34D-E10 — Multi-Service Cascade
Count distinct services affected by one parent incident after deduplication.
Priority: S

## W34D-E11 — Cross-Region Propagation
Detect whether incident expands:
single AZ -> region -> multi-region -> global.
Priority: S-

## W34D-E12 — Incident Recovery Half-Life
Measure time from first mitigation to:
provider resolved,
network normalization,
customer-service normalization.
These may differ.
Priority: S

## W34D-E13 — Post-Mitigation Relapse
Detect a second degradation after provider reports partial or underlying mitigation.
Priority: A+

## W34D-E14 — AWS Public Health State
Primary:
AWS Health Dashboard public Service Health.
Capture public events, service, region, severity and timeline.
Do not assume account-specific impact.
Priority: A+

## W34D-E15 — Azure Broad-Incident State
Primary:
Azure public status and status history/PIR.
Public Azure status focuses on wide-ranging incidents; absence is not proof an account/service is unaffected.
Priority: A

## W34D-E16 — Google Cloud Public Service-Health State
Primary:
Google Cloud Service Health / public incident history and RSS.
Capture incident timeline, affected services/features, regions/zones and customer-impact description.
Priority: A+

## W34D-E17 — Cloudflare Radar Traffic Anomaly
Use Radar traffic anomalies as an independent operational signal.
State:
ALGORITHMIC_ANOMALY
VERIFIED_OUTAGE.
Priority: S

## W34D-E18 — IODA Connectivity Confirmation
Fuse Georgia Tech IODA:
BGP,
active probing,
telescope
signals by country/region/ASN.
Priority: S

## W34D-E19 — RIPE RIS Withdrawal Burst
Use RIPE RIS Live real-time BGP updates to detect abnormal route withdrawals/peer-state events.
Priority: S-

## W34D-E20 — Routing-vs-Traffic Divergence
States:
BGP_ONLY
TRAFFIC_ONLY
BOTH
NEITHER.
Routing anomalies are not automatically customer outages.
Priority: S

## W34D-E21 — Provider Reality Gap
Compare provider self-report to:
Cloudflare traffic anomaly,
IODA,
RIPE RIS,
customer-service telemetry where lawful/public.
Priority: S

## W34D-E22 — Digital Dependency Graph
Graph:
cloud region/service
-> platform/API
-> public-company service
-> business process
-> revenue/transaction dependency.

Only sourced dependencies qualify.
Priority: S

## W34D-E23 — Single-Provider Concentration
Estimate fraction of a customer workload/business function depending on one cloud/CDN/DNS provider where publicly documented.
Priority: A+

## W34D-E24 — Multi-Cloud Substitution Capacity
Estimate whether affected workload can fail over to another region/provider without material degradation.
Priority: A+

## W34D-E25 — Business-Hours Exposure
Impact weight =
affected duration
× local business-hour overlap
× transaction intensity.
Priority: S-

## W34D-E26 — Payments / Commerce Disruption
For verified dependencies, detect whether cloud/network incident impairs:
checkout,
payments,
order entry,
authentication,
marketplace transactions.
Priority: S

## W34D-E27 — Travel / Transportation Digital Disruption
Map verified digital dependency to:
airline booking/check-in,
hotel reservation,
logistics dispatch,
mobility apps.
Priority: A+

## W34D-E28 — Market / Trading Infrastructure Digital Disruption
Map public exchange/broker/data-vendor incidents separately from generic cloud outages.
Do not infer exchange impact merely because a shared provider is degraded.
Priority: S-

## W34D-E29 — Customer Blast-Radius Breadth
Count independently verified customer services impaired by one parent infrastructure incident.
Priority: S

## W34D-E30 — Digital Capacity Loss Quotient
DCLQ =
probability-weighted customer business capacity unavailable
/
available failover/substitute capacity.
Priority: S

## W34D-E31 — Provider-vs-Customer Recovery Gap
Customer systems may recover after provider marks service resolved.
Feature:
customer normalization time - provider resolved time.
Priority: S-

## W34D-E32 — NDX Mega-Cap Digital Exposure
Aggregate verified operational impact for major Nasdaq constituents and their digital dependencies.
This is customer/provider operational exposure, not a generic "tech outage" factor.
Priority: S

## W34D-E33 — Cause Taxonomy
Separate:
ACCIDENTAL_CHANGE
CAPACITY
NETWORK
DNS
POWER
HARDWARE
SOFTWARE
SECURITY/CYBER
THIRD_PARTY
UNKNOWN.
Do not classify as cyberattack without evidence.
Priority: S methodology/edge hybrid

## W34D-E34 — Digital Infrastructure Truth Ladder
PROVIDER NOTICE / EXTERNAL ANOMALY
-> NETWORK/SERVICE IMPAIRMENT
-> CUSTOMER IMPACT
-> BUSINESS CAPACITY LOSS
-> TRANSACTION/REVENUE LOSS
-> FINANCIAL EFFECT.
Priority: S architecture

## Highest-priority W34D tests
1. W34D-E02 Provider Acknowledgement Lag
2. W34D-E04 Region-Service Blast Radius
3. W34D-E10 Multi-Service Cascade
4. W34D-E17 Cloudflare Radar Traffic Anomaly
5. W34D-E18 IODA Connectivity Confirmation
6. W34D-E20 Routing-vs-Traffic Divergence
7. W34D-E21 Provider Reality Gap
8. W34D-E22 Digital Dependency Graph
9. W34D-E30 Digital Capacity Loss Quotient
10. W34D-E34 Digital Infrastructure Truth Ladder
