# FDD-03 — Aurora Work: private corporate task organizer

> **Status:** FUNCTIONAL DESIGN — NOT IMPLEMENTED / NOT ACCEPTED  
> **Target:** Existing OpenClaw on OVH, Docker/headless, accessible from Windows and Android  
> **Timezone:** `America/Argentina/Buenos_Aires`  
> **Privacy:** Public-safe specification. Do not commit personal/corporate content or credentials.

**Cross-cutting contract.** Reuse the existing running OpenClaw, its supported agents/tools, native cron/heartbeat and persistent storage. Do not redesign VPS/network/authentication, change the main model, or incur API costs without explicit approval. Separate Work (corporate) from Career (personal recruiting). Scheduled tasks must not silently duplicate existing automations. No function is DONE based solely on a created cron job; prove live permitted data, persistence after restart, delivery, failure visibility and recovery. Android notifications must be checked, not assumed.

## 1. Approved business requirement
The user works with corporate **Outlook email, Microsoft Teams and calendar**. Manually copying pending items is unacceptable. Build a private assistant that reads authorized work communications, identifies client issues and the user's commitments, and maintains a concise personal dashboard. Each morning it proposes which tasks to tackle given calendar availability, effort and urgency. It never writes to corporate systems, contacts clients, sends mail, attends meetings or impersonates the user.

This is **personal internal organization**, not an employer-facing CRM or a bot participating in company workflows.

## 2. Architecture and permission gate
Preferred location for **task logic, tracking, storage and UI is the existing OpenClaw on OVH**. Input from Microsoft 365 via a permitted read-only Microsoft Graph integration, delegated to the user's account. Candidate permissions `Mail.Read`, `Calendars.Read`, `Chat.Read` (exact least privilege subject to tenant and use-case verification). The official Teams bot integration is not equivalent to read access to user's personal chat history.

**Mandatory gate:** employer must authorize third-party Graph access, external processing on personal OVH and any external model processing. Even an ephemeral raw email fetched over Graph leaves the corporate Microsoft environment; summaries (client and issue) can still be confidential. If corporate policy disallows this, do not bypass it with browser scraping or shadow sync. Do not call GPT/DeepSeek/OpenRouter with corporate bodies unless the provider and use are approved. An approved local extraction path is a separate design option, not part of this FDD by default.

## 3. Ingestion and interpretation
- **FR01 Read-only:** synchronize user's Inbox, Sent Items, authorized Teams messages and work calendar as feasible; begin with Outlook + calendar, add Teams after verified consent and API coverage.
- **FR02 Incremental reconciliation:** use provider IDs/delta markers and timestamps; recognize message edits/replies, avoid full mailbox downloads and duplicate tasks.
- **FR03 Discover obligations:** extract direct client requests, user's promises ('I'll investigate tomorrow'), escalation, due dates, dependency on others, and confirmed fixes. Distinguish tasks assigned to another employee from the user's responsibilities.
- **FR04 Group by case:** normalize customer/alias and issue; connect related Outlook and Teams threads without merging distinct incidents merely because the customer matches.
- **FR05 Lifecycle:** `NEW`, `TRIAGE`, `IN_ANALYSIS`, `WAITING_CLIENT`, `WAITING_INTERNAL`, `BLOCKED`, `POSSIBLY_RESOLVED`, `CLOSED_CONFIRMED`. Silence never means resolved; ambiguities must be visible.
- **FR06 Prioritize:** explicit deadline, client impact, blocker, age, promised response and current urgency. Rank reasons must be explainable. A newly received low-priority message must not displace critical older work.
- **FR07 Estimate:** use initial classes 30/60/90 min and calibrate from feedback. **Estimated remaining effort is not verified billable hours**; never invent recorded hours.
- **FR08 Schedule:** read work calendar busy/free slots and user-defined work hours, reserve a buffer for incidents, select an achievable top 2–3. Do not create calendar events.
- **FR09 Daily briefing:** morning plan, overdue commitments, items waiting on others, and proposals for available focus blocks; mark stale/unavailable data explicitly.
- **FR10 Explainability:** each record carries source identifiers or deep links (if permitted), evidence type, last change and confidence. Do not store full email bodies or chat transcripts in dashboard.

## 4. Data contract and sample dashboard
Each item: `task_id`, `client_alias`, `issue_title`, `status`, `priority`, `priority_reason`, `estimated_remaining_minutes`, `assignee`, `waiting_on`, `due_at`, `next_followup_at`, `last_activity_at`, `provenance_ref`, `confidence`, `last_reconciled_at`.

| Client | Task | Status | Priority | Effort |
|---|---|---|---|---|
| Client A | Validate sales interface | IN_ANALYSIS | High | 90 min |
| Client B | Investigate report issue | TRIAGE | Medium | 60 min |
| Client C | Await confirmation | WAITING_CLIENT | Medium | 30 min |

Examples are fictional and should not be mistaken for real connected case data. Store sanitized minimum metadata, set a retention rule, encrypt sensitive persistence/backups, and keep it out of public Git.

## 5. Actors, prohibited behavior and boundaries
- **Only user** sees dashboard and receives summaries on Windows/Android.
- **Absolutely no** Outlook/Teams sending, corporate calendar modifications, automated ticket changes, Softland writes, autonomous meetings or client communication.
- Career agent **must not access** corporate data; no common cross-agent tools, workspace or storage permissions.
- Graph tokens retained securely only in runtime configuration, not Git; support revocation.

## 6. Failure cases
No Graph permission: **ACCESS_BLOCKED**, no workaround. No new data: show last sync time, not 'all resolved'. LLM low confidence: `TRIAGE`, not hallucinated closed case. Message deletion: preserve only allowed audit reference, honor retention. API throttling: backoff and expose health. Calendar error: do not fabricate availability.

## 7. Acceptance and staged delivery
- **W0** Read-only inventory and corporate/tenant approval for processing. No deployment until authorization.
- **W1** Demonstrate Inbox+Sent and calendar Graph read without modifications; Teams scope optional separate authorization.
- **W2** On 20–30 representative authorized messages (including FYI, delegated, open, resolved), target at least 90% recall for explicit own commitments, no duplicate tasks or false auto-closures, source reference for every task.
- **W3** Five consecutive workdays of morning recommendations grounded in real calendar slots and realistic effort.
- **W4** Add allowed Teams streams; ensure deduplication across sources.
- **DONE:** zero manual re-entry for covered messages, credible daily prioritization, no corporate writes, no unapproved external processing, state surviving restart and backup restore.

## 8. Unresolved decisions
Tenant consent/Entra client registration, allowable message scope, employee policy, approved inference provider or local extraction method, retention duration, agreed workday/time buffers, notification channel, eventual dashboard UI. The work status is **DESIGNED — not yet connected**.

**Source-of-truth companion:** `docs/AURORA_WORK_SPEC.md`; reconcile changes between this FDD and that specification rather than maintaining conflicting requirements.
