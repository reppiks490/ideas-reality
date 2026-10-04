# Wave 9C Source Notes

Namespace: **W9C**

## W9C-D01 — FCC ULS / LMS Public Licensing Data

Primary:
https://www.fcc.gov/fcc-frequency-assignment-databases
https://www.fcc.gov/wireless/data/public-access-files-database-downloads
https://www.fcc.gov/uls/transactions/daily-weekly

FCC states ULS public data include wireless services plus assignments/transfers and are updated in daily/weekly files. LMS broadcast public files are also updated regularly.

Key rule:
application status, authorization status and consummation are different events.

## W9C-D02 — USPTO Open Data Portal Assignments

Primary:
https://data.uspto.gov/apis/patent-file-wrapper/assignments
https://data.uspto.gov/apis

Assignment endpoint:
GET /api/v1/patent/applications/{applicationNumberText}/assignment

Fields include received, recorded, mailed and execution dates, assignor/assignee and conveyance. USPTO states assignment data are refreshed daily. API requires key/account; bulk daily/annual files are also available.

## W9C-D03 — EPA ECHO

Primary:
https://echo.epa.gov/

ECHO public web services integrate multiple EPA program systems and can return facility/compliance/enforcement data in structured formats.

Treat program-specific fields carefully; ECHO is not a generic construction-permit feed.

## W9C-D04 — USACE Regulatory / Section 408 Public Data

Primary:
https://permits.ops.usace.army.mil/orm-public
https://rrs.usace.army.mil/rrs/public-notices

Public data include pending complete applications, permit decisions, public notice dates, NEPA milestones, Section 408 and emergency permit information.

## W9C-D05 — Texas Railroad Commission Drilling Permits

Primary:
https://www.rrc.state.tx.us/resource-center/research/data-sets-available-for-download/

Official cadence:
- pending W-1 permit snapshot: twice daily
- current-month approved/master data: nightly
- completions query: nightly
- production: monthly.

Files include identifiers, operator/lease/field, well profile, depth, status and coordinates.

## W9C-D06 — North Dakota DMR Daily Activity

Primary:
North Dakota Department of Mineral Resources daily oil/gas activity reports.

Useful as a second jurisdictional validation source for permit/production lifecycle methodology.

## W9C-D07 — BOEM Lease Data

Primary:
https://www.boem.gov/oil-gas-energy/lease-sales
https://www.data.boem.gov/Main/Leasing.aspx

BOEM publishes lease sale bids/results, later adjudication/acceptance, active lease ownership/operator information and status changes.

## W9C-D08 — PJM Service Request / Interconnection Data

Primary:
https://www.pjm.com/planning/m/cycle-service-request-status

Public project pages and study reports include project status, dates, MW/resource type and study milestones. Public and secure datasets differ; never rely on CEII/restricted fields in a public-data claim.

## W9C-D09 — EIA-860M

Primary:
https://www.eia.gov/electricity/data/eia860m/

Monthly preliminary generator inventory tracks existing, proposed, retired and planned generator units. EIA explicitly notes values can be corrected in later monthly releases.

## W9C-D10 — Rights Entity Mapping

Needed identifiers:
FCC FRN/call sign,
USPTO assignee,
USACE applicant/project,
RRC operator/API well ID,
BOEM company/lease,
PJM project/developer,
EIA plant/operator.

Create a versioned mapping from each legal entity to public issuer and economic exposure.
