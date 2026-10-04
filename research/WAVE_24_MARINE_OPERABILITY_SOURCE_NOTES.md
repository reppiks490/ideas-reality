# Wave 24M — Source Notes

Namespace: **W24M**

## W24M-D01 — NOAA CO-OPS Data API
Primary:
https://api.tidesandcurrents.noaa.gov/api/prod/

Products include preliminary/verified 6-minute water levels, currents, current predictions, wind, visibility and air gap where available.

## W24M-D02 — NOAA PORTS
Primary:
https://tidesandcurrents.noaa.gov/ports.html
https://tidesandcurrents.noaa.gov/ports_help.html

PORTS provides frequently updated real-time oceanographic/meteorological observations and predictions for participating ports.

## W24M-D03 — NOAA Operational Forecast Systems
Primary:
https://tidesandcurrents.noaa.gov/models/
https://tidesandcurrents.noaa.gov/ofs/ofs_faq.html

OFS systems run on defined cycles and provide short-term forecasts, typically 48–120 hours depending on system, with model output distributed through NOAA infrastructure.

## W24M-D04 — NOAA NDBC
Primary:
https://www.ndbc.noaa.gov/
https://www.ndbc.noaa.gov/data/realtime2/

NDBC real-time data include standard meteorology, continuous wind, spectral-wave summaries and other station-dependent data. Most stations report hourly; NDBC says much data are available by roughly 25 minutes after the hour.

## W24M-D05 — U.S. Coast Guard Homeport / MSIB
Primary:
https://homeport.uscg.mil/
https://www.news.uscg.mil/

Captain-of-the-Port restrictions and Marine Safety Information Bulletins are event-driven and geographically decentralized. There is not assumed to be one complete national machine API; preserve exact local public source/timestamp.

## W24M-D06 — Hurricane Port Conditions
Official Coast Guard examples document:
YANKEE: restrictions on inbound commercial vessel traffic in relevant events;
ZULU: port closure/suspension of vessel/cargo operations except authorized movements.

Exact local COTP order controls.

## W24M-D07 — Great Lakes St. Lawrence Seaway
Primary:
https://greatlakes-seaway.com/
https://www.seaway-greatlakes.com/

Public notices expose maximum permissible draft, effective dates, navigation-season rules and operational changes. Public pages also expose vessel-transit/bridge/environment information.

## W24M-D08 — Seaway Draft Information System Rules
Primary:
2026 Seaway Handbook / Notices.

DIS-qualified vessels may receive a defined incremental draft allowance when all rule requirements are satisfied.

## W24M-D09 — Marine Operability Literature
Use port-hydrodynamic/AIS research as mechanism evidence for how under-keel/current restrictions can create cascading waiting time.

Literature is not evidence of market alpha.

## W24M-D10 — Existing Repo Cross-Sources
Fuse W24M with existing:
AIS/port data,
USACE locks,
weather/tsunami,
Panama/Great Lakes chokepoints,
rail/truck alternatives,
pipeline/LNG flows,
energy inventories.

Do not duplicate their connectors.
