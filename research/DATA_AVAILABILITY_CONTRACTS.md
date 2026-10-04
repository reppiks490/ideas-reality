# Data Availability Contracts

Status: CANONICAL GOVERNANCE
Effective: 2026-10-04

This file defines what "available" means for every research source in this repository.

## 1. Required clocks

Every observation/source event must preserve, when applicable:

- `event_time`: underlying physical/financial/legal event.
- `reporting_deadline`: deadline imposed on a reporter. This is not public availability.
- `source_received_time`: when the source owner received the report, if observable.
- `published_time`: first time the information became lawfully public in the relevant channel.
- `first_seen_time`: first time our collector observed that public information.
- `ingested_time`: time stored by our system.
- `revision_time`: time a correction/amendment/new vintage became public.
- `effective_time`: time a rule/order/restriction becomes operative.

Backtests may use a datum only when its applicable public availability time is <= decision time.

## 2. Source classes

- PUBLIC_REALTIME: public operational feed whose publication latency is documented/measurable at the target horizon.
- PUBLIC_NEAR_REALTIME: public feed with bounded minutes/hours latency.
- PUBLIC_SCHEDULED: public at scheduled release clocks.
- PUBLIC_EVENT_DRIVEN: published when qualifying events occur; no event/no publication is not zero.
- PUBLIC_BATCH: periodic batch publication.
- PUBLIC_DELAYED: useful only after material delay.
- RETROSPECTIVE_ONLY: historical/validation data unsuitable for target live horizon.
- PAID_REALTIME: public market-data product requiring paid subscription.
- LICENSED_REALTIME: accessible only under license/contract.
- PUBLIC_WEB_ONLY: human-readable public state without a guaranteed production API.
- UNKNOWN_MEASURED: public source whose public-posting latency is not formally documented; must be measured.
- CONFIDENTIAL_NONPUBLIC: prohibited as a live research source unless a separate lawful public disclosure exists.

## 3. Deadline != publication

A filing/reporting rule such as "within 24 hours", "within 96 hours", or "by 3 p.m." describes reporter obligation unless the primary source explicitly states that it is simultaneously publicly disseminated.

Research must never substitute reporting_deadline for published_time.

## 4. Homepage != provenance

A source is provenance-complete only when its record points to the best reproducible primary artifact available:
- API endpoint/documentation
- downloadable dataset
- official rule/specification
- exact notice/order
- official machine-readable feed
- official source page that directly exposes the data

Generic homepages are allowed only when no more specific primary artifact exists, and that limitation must be recorded.

## 5. Revisions and vintages

Mutable datasets are immutable in our archive: every fetched vintage is retained with content hash and retrieval timestamp.

Later revisions may not overwrite earlier historical information states.

## 6. Unknown latency

If latency is undocumented:
1. label source UNKNOWN_MEASURED;
2. prospectively record event/source/first-seen clocks;
3. estimate empirical latency distribution;
4. use conservative upper quantile in historical simulation;
5. prohibit claims of intraday/live usability until sufficient evidence exists.

## 7. Missingness

Distinguish:
- TRUE_ZERO
- NOT_SCHEDULED
- SOURCE_STALE
- SOURCE_DOWN
- SENSOR_OFFLINE
- REPORT_NOT_YET_PUBLIC
- ACCESS_DENIED
- SCHEMA_ERROR
- UNKNOWN

No missing source may be forward-filled indefinitely.

## 8. Rule/schema versions

Every rule-driven source stores:
- version/document identifier
- publication date
- effective date
- superseded date if known
- source URL/hash

Current rules must not be applied retroactively.

## 9. Rights and access

Each production source must state:
- access path
- authentication requirement
- paid/free
- redistribution restriction if known
- archival permission/constraints
- whether the UI/webpage and machine feed have different rights

Scientific validity and production rights are separate gates.

## 10. Promotion rule

No candidate reaches DATA_VERIFIED without a completed availability contract for every required source.

If a source is delayed beyond the proposed horizon, the candidate must either:
- move to a slower horizon,
- use the source only as retrospective validation/labels,
- replace it with a lawful faster source,
- or be retired.
