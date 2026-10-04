# Wave 36P — Source Notes

Namespace: **W36P**

## W36P-D01 — FDA Drug Shortages
Primary:
https://www.fda.gov/drugs/drug-safety-and-availability/drug-shortages
https://www.accessdata.fda.gov/scripts/drugshortages/

FDA tracks national shortages, current/resolved status, discontinuations, applicants, reasons and estimated duration/availability. FDA states the list is updated daily.

## W36P-D02 — openFDA Drug Shortages
Primary:
https://open.fda.gov/apis/drug/drugshortages/

Machine-readable JSON endpoint:
https://api.fda.gov/drug/shortages.json

Searchable fields include company, presentation, status, availability, shortage reason, update date, change date and initial posting date.

## W36P-D03 — FDA Shortage Semantics
FDA defines a shortage as national demand/projected demand exceeding supply and publishes statutory shortage-reason categories. Manufacturer product-availability statements can change daily.

## W36P-D04 — FDA Drug Enforcement / Recalls
Primary:
https://open.fda.gov/apis/drug/enforcement/
https://www.fda.gov/safety/recalls-market-withdrawals-safety-alerts/industry-guidance-recalls

openFDA enforcement data are publicly releasable recall/enforcement records and update on their documented cadence; they are not an unclassified real-time recall-initiation feed.

Use recall initiation/report/classification/public dates according to source semantics.

## W36P-D05 — FDA Inspection Classification
Primary:
https://www.fda.gov/inspections-compliance-enforcement-and-criminal-investigations/inspection-classification-database
https://datadashboard.fda.gov/

FDA updates final NAI/VAI/OAI classifications weekly. Database is not comprehensive.

## W36P-D06 — FDA Inspection Data API
Primary:
https://api-datadashboard.fda.gov/v1/inspections_classifications

Field documentation includes inspection end date, product type and classification code.

## W36P-D07 — OII Electronic Reading Room / Form 483
Primary:
https://www.fda.gov/about-fda/office-inspections-and-investigations/oii-foia-electronic-reading-room

Selected/proactively posted inspection records include record date, company, FEI, record type and publish date.

## W36P-D08 — FDA Warning Letters
Primary:
https://www.fda.gov/inspections-compliance-enforcement-and-criminal-investigations/compliance-actions-and-activities/warning-letters

Use the FDA public-posting date/time available to the researcher; letter date and public-posting availability are distinct if they differ.

Use public issue/posting date and later resolution/closeout independently.

## W36P-D09 — FDA Import Alerts
Primary:
https://www.fda.gov/industry/import-alerts/search-import-alerts
https://www.accessdata.fda.gov/cms_ia/

FDA states the Import Alert databases are updated in real time; archive the observed list vintage and exact firm/product/list state.

Use firm/product/country and current alert-list state; detention without physical examination is a supply-access constraint, not proof of national shortage.

## W36P-D10 — Drug Shortage Mechanism Evidence
FDA and economic literature identify manufacturing quality, limited capacity, ingredient shortages, discontinuations, logistics and demand increases as shortage mechanisms, with sterile injectables especially vulnerable.
Use as mechanism evidence; validate every live chain point-in-time.
