# Wave 30W — Source Notes

Namespace: **W30W**

## W30W-D01 — USGS Water Data APIs
Primary:
https://api.waterdata.usgs.gov/

Continuous observations can include discharge, gage height and water temperature, often at ~15-minute cadence with telemetered observations available within minutes at many sites.

## W30W-D02 — U.S. Drought Monitor
Primary:
https://droughtmonitor.unl.edu/DmData/DataDownload.aspx
https://droughtmonitor.unl.edu/DmData/DataDownload/WebServiceInfo.aspx

Weekly vector/statistical data and REST services provide D0-D4 drought state by geography.

## W30W-D03 — EPA ECHO / ICIS-NPDES
Primary:
https://echo.epa.gov/
https://echo.epa.gov/tools/web-services

ECHO/ICIS provides NPDES facility, permit, limit and monitoring/compliance data. Exact thermal-limit extraction and permit semantics require facility-specific validation.

## W30W-D04 — EIA Generator/Cooling Data
Primary:
https://www.eia.gov/electricity/data/eia860/
https://www.eia.gov/electricity/data/eia923/

EIA structural/historical datasets identify generator/plant characteristics, generation and environmental/cooling information.

## W30W-D05 — USGS Thermoelectric Water Reanalysis
Primary:
https://www.usgs.gov/data/thermoelectric-power-water-use-reanalysis-2008-2020-period-power-plant-month-and-year

Plant-level historical estimates provide structural withdrawal/consumption dependence and uncertainty ranges.

## W30W-D06 — California State Water Board Curtailments
Primary:
https://www.waterboards.ca.gov/drought/

Scott/Shasta pages demonstrate point-in-time public orders, addenda, priority groups, flow thresholds and suspension/reinstatement states.

## W30W-D07 — California Water Rights
Primary:
https://www.waterboards.ca.gov/upward/calwatrs/
https://www.waterboards.ca.gov/drought/respond_to_your_curtailment_order.html

CalWATRS is the current water-rights reporting/data system. Curtailment status is watershed/order-specific; preserve exact order/addendum/effective time and do not infer a facility right from geography alone.

Facility/right mapping must be verified individually.

## W30W-D08 — Bureau of Reclamation 24-Month Studies
Primary:
https://www.usbr.gov/uc/water/crsp/studies/24Month_01.html

Use point-in-time monthly reservoir/operation forecast vintages.

## W30W-D09 — Colorado River Annual Operating Plan
Primary:
https://www.usbr.gov/lc/region/g4000/aop/AOP26.pdf
https://www.usbr.gov/lc/riverops.html

Use the annual plan/document effective for each year plus subsequent operating-study/decision vintages; the annual plan is not a fixed forecast for the entire year.

Use as slower legal/allocation state.

## W30W-D10 — Existing Repo Cross-Sources
Reuse:
W14I reservoir/hydro,
W23T grid topology,
W15X industrial outage,
W7T/EIA grid,
weather and facility geospatial layers.
