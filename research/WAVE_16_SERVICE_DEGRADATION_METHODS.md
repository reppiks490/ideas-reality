# Wave 16S — Research Methods

Namespace: **W16S**

## W16S-M01 — Weekly Rail Vintage Archive
Preserve each carrier report and consolidated STB file by publication date.

Corrections/restatements are new vintages, not replacements.

## W16S-M02 — Carrier Methodology Versioning
STB carrier methodology can differ/change.

Store the carrier's published metric definition and effective period.

## W16S-M03 — Seasonal Rail Baseline
Normalize speed/dwell/cars-held by:
carrier,
terminal,
train type,
week-of-year,
weather regime.

## W16S-M04 — Network Breadth vs Local Shock
Separate one-terminal deterioration from carrier-wide or multi-carrier deterioration.

## W16S-M05 — Commodity Lane Mapping Confidence
Map rail service metrics to commodity/customer exposure only when route/terminal/service relationships are evidenced.

## W16S-M06 — Rail Correction Ledger
STB can publish carrier corrections/restatements.

Backtests retain the originally available value until correction publication.

## W16S-M07 — FAA Event-Time Ledger
Store:
forecast posted
event activated
event updated
extension probability changes
event ended.

## W16S-M08 — Airport Cargo Importance Weight
Weight airport constraints by freight tonnage/network role using independent public statistics.

Passenger volume is not a substitute for cargo importance.

## W16S-M09 — Cargo Sort-Window Alignment
Airport delay has different economic effect depending on whether it overlaps critical overnight/daytime cargo sort banks.

## W16S-M10 — Reason-Specific FAA Model
Weather, runway, equipment and volume constraints receive separate treatment.

## W16S-M11 — Advisory vs Realized Delay
Forecast/ground program existence and realized operational delay are separate outcomes.

## W16S-M12 — CSMS Message Versioning
Store every CBP CSMS message with message ID, timestamp, affected system/mode and resolved-message link.

## W16S-M13 — Planned Maintenance Mask
Scheduled ACE maintenance must not be labeled an unexpected outage.

## W16S-M14 — UI-vs-EDI Separation
If ACE portal UI is slow but EDI processing is normal, treat them as different operational states.

## W16S-M15 — Queue-Clearing State
Resolution message != backlog eliminated.

Where CBP explicitly references queues/backlog, store clearance completion separately.

## W16S-M16 — Physical Confirmation Gate
ACE digital degradation promotes only if it predicts measurable border/port/cargo-delay consequences.

## W16S-M17 — FDA Daily Availability Ledger
Store each drug-shortage record by observed daily vintage.

Do not use later reason/status/resolution fields before their update date.

## W16S-M18 — Product/Manufacturer Identity
Resolve NDC/product presentation, applicant/manufacturer and parent company separately.

## W16S-M19 — Shortage Selection Boundary
FDA national shortage status reflects nationwide supply/demand and manufacturer reporting; local pharmacy/hospital scarcity is not equivalent.

## W16S-M20 — Intermediate Throughput Gate
Before market-return testing, require prediction of:
rail delivery,
airport cargo throughput,
customs clearance,
drug availability,
or another real flow variable.
