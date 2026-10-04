# Wave 16S — Source Notes

Namespace: **W16S**

## W16S-D01 — STB Rail Service Data
Primary:
https://www.stb.gov/reports-data/rail-service-data/
https://opendata.stb.gov/explore/assets/ep724-public-data/

STB requires Class I carriers to file weekly service-performance metrics including train speed, terminal dwell, cars online, unit-train origin dwell, trains held, cars not moved for 48+ hours and grain-service measures. Availability class: PUBLIC_SCHEDULED_WEEKLY; use actual STB publication vintage.

## W16S-D02 — STB Carrier Methodologies
Carrier methodology documents published under EP 724 define metric construction and changes.

Use point-in-time methodology by carrier.

## W16S-D03 — FAA NAS Status
Primary:
https://nasstatus.faa.gov/

FAA NAS Status provides current/forecast traffic-management information including closures, ground stops, ground delay programs, arrival/departure delays and deicing. Archive event updates/first-seen time; the page/feed being current does not eliminate ingestion/transport latency.

## W16S-D04 — FAA NAS Status Machine-Readable Feed
FAA NAS Status user documentation states active airport/en-route events are available in XML.

Use official machine-readable feed for production research rather than scraping visual pages.

## W16S-D05 — FAA OPSNET
Primary:
https://www.aspm.faa.gov/

Use historical delay details/summary to validate NAS Status event consequences.

## W16S-D06 — CBP Cargo Systems Messaging Service
Primary:
https://www.cbp.gov/trade/automated/cargo-systems-messaging-service

CSMS publishes timestamped operational messages, including ACE maintenance, unavailable applications, slow processing and resolution notices.

## W16S-D07 — CBP CSMS Archive
CBP publishes monthly archive documents containing CSMS messages.

Preserve original message IDs/timestamps and classify by modality/system.

## W16S-D08 — FDA Drug Shortages
Primary:
https://www.fda.gov/drugs/drug-safety-and-availability/drug-shortages

FDA states its national drug-shortage list is updated daily with new/resolved shortages and capacity updates.

## W16S-D09 — openFDA Drug Shortages API
Primary:
https://open.fda.gov/apis/drug/drugshortages/

Searchable fields include company, shortage reason, availability, status, update/change dates, dosage form, strength and therapeutic category.

## W16S-D10 — Existing Repo Cross-Sources
W16S should fuse, not duplicate:
CBP border wait times,
port/rail telemetry,
weather,
facility exposure graphs,
WARN/human-capacity data,
physical inventory/basis sources.
