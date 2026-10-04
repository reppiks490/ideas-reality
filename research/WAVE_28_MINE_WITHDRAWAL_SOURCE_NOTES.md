# Wave 28M — Source Notes

Namespace: **W28M**

## W28M-D01 — MSHA 107(a) Orders Issued
Primary:
https://arlweb.msha.gov/OpenGovernmentData/OGIMSHA.asp

MSHA publishes a dedicated list of section 107(a) imminent-danger orders. Current Open Government documentation states these files are generally updated every Friday afternoon unless otherwise noted.

## W28M-D02 — Section 107(a) Authority
Under the Mine Act, a 107(a) order requires the operator to withdraw persons from the affected area and prohibit entry until MSHA determines the imminent danger/causal conditions no longer exist.

## W28M-D03 — 107(a) Definition File
Primary:
https://arlweb.msha.gov/opengovernmentdata/DataSets/107(a)_Orders_Issued_Definition_File.txt

Fields include Mine ID, mine/operator identity, violation/order number, issue date and termination date.

## W28M-D04 — MSHA Mines Dataset
Primary:
https://arlweb.msha.gov/OpenGovernmentData/OGIMSHA.asp

Use the Mines dataset/definition file exposed from the Open Government portal; archive complete replacement vintages.

Contains Mine ID, current name/status/status date, operator/controller, mine type, commodity/SIC fields, employees, shifts and geography.

## W28M-D05 — MSHA Inspections
Primary:
https://arlweb.msha.gov/OpenGovernmentData/OGIMSHA.asp

Use the Inspections dataset/definition file from the same portal and the actual weekly replacement vintage; inspection event time is not public-file availability.

Use Event Number/Mine ID to normalize enforcement by inspection activity.

## W28M-D06 — General Violations Dataset
Primary:
https://www.msha.gov/data-and-reports/data-sources-and-calculators/data-resources/mdsrg/violations-data-set

Important limitation:
MSHA documentation says this dataset includes only final citations/orders. It is historical validation, not assumed live enforcement.

## W28M-D07 — Pattern of Violations
Primary:
https://www.msha.gov/compliance-and-enforcement/pattern-violations-pov
https://www.msha.gov/mines-issued-pov-notifications

Active POV status increases withdrawal-order consequences for subsequent S&S violations under the program rules.

## W28M-D08 — Quarterly Employment / Coal Production
Primary:
https://www.msha.gov/data-and-reports/data-sources-and-calculators/data-resources/mdsrg/employment-production-quarterly-data-set

MSHA states the quarterly dataset is posted the first Friday of the second month following the quarter, about 30–45 days after quarter-end.

## W28M-D09 — Preliminary Fatality Reports
Primary:
https://www.msha.gov/data-reports/fatality-reports

MSHA publishes preliminary reports for fatal mine accidents. Use public-posting time and treat cause/details as preliminary until final.

## W28M-D10 — MSHA Open Data Update Semantics
Open Government files are complete replacement files. Preserve each vintage rather than assuming the current file reconstructs what was public historically.
