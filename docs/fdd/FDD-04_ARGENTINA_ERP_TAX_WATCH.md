# FDD-04 — Argentina ERP / tax regulatory watch

> **Status:** FUNCTIONAL DESIGN — NOT IMPLEMENTED / NOT ACCEPTED  
> **Target:** Existing OpenClaw on OVH, Docker/headless, accessible from Windows and Android  
> **Timezone:** `America/Argentina/Buenos_Aires`  
> **Privacy:** Public-safe specification. Do not commit personal/corporate content or credentials.

**Cross-cutting contract.** Reuse the existing running OpenClaw, its supported agents/tools, native cron/heartbeat and persistent storage. Do not redesign VPS/network/authentication, change the main model, or incur API costs without explicit approval. Separate Work (corporate) from Career (personal recruiting). Scheduled tasks must not silently duplicate existing automations. No function is DONE based solely on a created cron job; prove live permitted data, persistence after restart, delivery, failure visibility and recovery. Android notifications must be checked, not assumed.

## 1. Objective
Proactively identify **official** Argentine regulatory and operational changes that may affect ERP implementations, fiscal interfaces and client incidents. Output an actionable brief, not a generic news digest or definitive legal opinion.

## 2. Sources
ARCA, ARBA and relevant provincial/municipal official publications, implementation manuals, layouts, calendars and published resolutions. Only include sources actually verified and dated. Use web/news retrieval where authorized; keep exact source URL, issuing body, publication date and effective date. Avoid relying solely on social posts.

## 3. Requirements
- **FR01 Scan:** weekly proposed Monday 09:00 local, with a lookback window and publication-time handling; urgent changes may be separately enabled.
- **FR02 Validate:** distinguish published draft, enacted rule, effective change, deadline extension, interpretation, technical specification and historical recap.
- **FR03 Map ERP impact:** identify affected process (invoice, withholding, perception, IVA, IIBB, e-report, file layout, jurisdiction), likely operational action and uncertainty.
- **FR04 Deduplicate:** track official document identifier and version; suppress reposts, highlight amendments.
- **FR05 Prioritize:** imminent effective dates, layout-breaking changes and mandatory filings first; label 'no verified relevant changes' only after successful scan.
- **FR06 Deliver:** 3–8 concise items, original source links, what changed, who is impacted, possible follow-up for consultant; no automatic ERP production edits.

## 4. Persistent state
Store source URL, regulation ID, official timestamps, effective date, prior-seen checksum/version and status `NEW`, `UPDATED`, `NO_CHANGE`, `UNVERIFIED`; avoid full copies of copyrighted documents.

## 5. Exceptions and boundaries
If source unavailable, say `SOURCE_UNCHECKED`; never invent changes or infer future legislation. Escalate ambiguous tax interpretation as needing qualified verification. Do not duplicate an existing ChatGPT scheduled tax briefing until user explicitly chooses cutover.

## 6. Acceptance
Two real weekly runs with at least one manually audited official-source sample; correct dates, functional ERP relevance and dedupe. If a source is unavailable, failure must be visible. No external filing or production system changes.

## 7. Dependencies and decisions
List of relevant provinces, topical coverage, delivery schedule, source catalog and relationship with existing recurring briefing. Related: FDD-09 and FDD-10.
