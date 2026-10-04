# Wave 34D — Source Notes

Namespace: **W34D**

## W34D-D01 — AWS Health Dashboard
Primary:
https://health.aws.amazon.com/health/status
https://docs.aws.amazon.com/health/latest/ug/aws-health-dashboard-status.html

Public Service Health requires no sign-in and exposes public service/region incidents, severity and update timelines. Service history is available for the recent historical window.

## W34D-D02 — AWS Programmatic Caveat
AWS Health API is authenticated/account-oriented and AWS documentation cautions that public RSS format may change. Treat public dashboard/RSS as public source; do not assume unrestricted API access.

## W34D-D03 — Azure Status / Status History
Primary:
https://azure.status.microsoft/
https://azure.status.microsoft/en-us/status/history/

Azure public status is for broad incidents. Status history retains public Post Incident Reviews for multiple years and provides incident tracking IDs, affected regions/services and timelines.

## W34D-D04 — Google Cloud Service Health
Primary:
https://status.cloud.google.com/

Public status and per-product history expose incident details, affected products/locations, customer-impact text and update timelines. Google documentation also provides an RSS consumption path for public Service Health.

## W34D-D05 — Cloudflare Radar
Primary:
https://developers.cloudflare.com/radar/

Radar API exposes traffic anomalies and outage annotations. API use requires a Cloudflare API token. Verified outages are distinct from algorithmically observed anomalies.

## W34D-D06 — Georgia Tech IODA
Primary:
https://ioda.inetintel.cc.gatech.edu/

Public outage monitoring combines BGP, active probing and telescope signals at country/region/ASN scope. Dashboard supports CSV export; API use has documented time-range limits.

## W34D-D07 — RIPE RIS Live
Primary:
https://ris-live.ripe.net/
https://ris-live.ripe.net/manual/

Real-time BGP messages are available through a filterable WebSocket JSON API and stream, including announcements, withdrawals and peer-state events.

## W34D-D08 — RouteViews
Primary:
https://api.routeviews.org/docs/
https://archive.routeviews.org/

Use collector/event timestamps and archive publication separately. Current RouteViews API/archive cadence does not prove identical historical latency.
Use as secondary routing confirmation where needed.

## W34D-D09 — Customer Dependency Evidence
Use SEC filings, official engineering architecture documents, incident reports and authoritative customer/provider disclosures to establish dependencies.

## W34D-D10 — Operational-Risk Literature
Studies of large IT outages such as the 2024 CrowdStrike event provide mechanism evidence that digital outages can create operational and market effects.
Use only as mechanism evidence; reproduce with point-in-time incident/dependency data.
