# Wave 24A — Source Notes

Namespace: **W24A**

## W24A-D01 — PJM Seven-Day Generation Outages
Primary:
https://dataminer2.pjm.com/feed/gen_outages_by_type

PJM reports today + six days of active/approved generation outage MW by region and outage type: planned, maintenance and forced.

## W24A-D02 — PJM Forecasted Generation Outages
Primary:
https://dataminer2.pjm.com/feed/frcstd_gen_outages

Provides longer-horizon expected outage MW by region for baseline construction.

## W24A-D03 — PJM Daily Generation Capacity
Primary:
https://dataminer2.pjm.com/feed/day_gen_capacity

Includes Economic Max, Emergency Max and Total Committed fields. Source definitions note these values should not be treated as outage-adjusted capacity without joining the relevant outage state.

## W24A-D04 — PJM Operations Summary
PJM projected-peak operations feeds provide scheduled capacity, tie flow, load forecast and operating reserve on morning update cycles.

## W24A-D05 — ERCOT Generation Outages Dashboard
Primary:
https://www.ercot.com/gridmktinfo/dashboards/generationoutages

ERCOT states current outage data include planned/forced full outages and qualifying partial derates and update every five minutes.

## W24A-D06 — ERCOT Hourly Resource Outage Capacity
Primary:
https://www.ercot.com/mp/data-products/data-product-details?id=NP3-233-CD

Public hourly 168-hour outlook by load zone/resource class using Outage Scheduler data.

## W24A-D07 — ERCOT Unplanned Resource Outages
Primary:
https://www.ercot.com/mp/data-products/data-product-details?id=NP1-346-ER

Daily retrospective public snapshot of forced/maintenance outages and derates; useful for validation at actual publication lag.

## W24A-D08 — CAISO Curtailed / Non-Operational Generators
Primary:
https://www.caiso.com/market-operations/outages/curtailed-and-non-operational-generators

Daily current-trade-date snapshot around 8:30 a.m. PT; fields can include resource, planned/forced type, curtailment MW/timing, PMax, NQC, zone and BA.

## W24A-D09 — NERC GADS
Primary:
https://www.nerc.com/programs/reliability-assessment--performance-analysis/generating-availability-data-system

Use aggregated historical forced-outage/derate statistics as structural priors only. GADS reporting/publication cadence is not suited to live operational triggers.

## W24A-D10 — Existing Repo Cross-Sources
W24A should fuse, not duplicate:
W23T transmission topology,
W22G gas transport,
W14I nuclear/hydro,
weather/load,
storage,
interchange,
emergency grid states.
