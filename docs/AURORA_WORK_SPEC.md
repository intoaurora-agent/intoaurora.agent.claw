# AURORA WORK — Private corporate work organizer

Status: **FUNCTIONAL SCOPE AGREED; ACCESS AND IMPLEMENTATION NOT VERIFIED**  
Date: 2026-11-09  
Owner: user, for **exclusive personal internal work organization**

## Explicit product decision

Aurora Work is **not** a CRM or a company-facing bot. It is a private dashboard and day planner for the user's own pending consulting work. The user uses **Microsoft Teams, corporate Outlook email and Teams/Outlook calendar**. Manual duplication of tasks is unacceptable: agent must derive candidate commitments automatically from messages, sent replies, incoming replies and calendar within authorized scope.

It must **never send emails, write Teams messages, attend or impersonate the user in meetings, change calendar events, contact clients, modify Softland or update corporate systems**. There is no need to participate in employer workflows on the user's behalf. All outputs are displayed privately in the same persistent OpenClaw on OVH, consulted from Android and Windows.

## Proposed data flow

Corporate Outlook / Teams / calendar → authorized **read-only Microsoft Graph** → temporary inspection/extraction → minimal task/status records → persistent private Aurora Work dashboard and morning briefing.

Data retained per task (minimum practical): `task_id`, client/alias, normalized topic, short sanitized task title, status, priority, estimated remaining effort, last activity date, due/follow-up date if known, responsible party / waiting-on flag, provenance identifier or message deep-link if policy allows, extraction confidence and last reconciliation time. Raw email, complete chat transcripts and attachments are **not** required in the persistent board. References should support review without copying message bodies. Avoid exposing full sensitive content in notifications.

**Important security truth**: with direct Graph→OVH reading, original message content transits the user's personal OVH environment even if discarded immediately. Client name and case status can themselves be sensitive. Employer authorization for access, external processing and any external LLM processing must be established. Graph delegated permission is not automatically organizational approval. If employer forbids data transfer, the direct OVH approach is blocked; do not bypass via browser scraping or local shadow synchronization. An organization-approved internal extractor could be an alternative but contradicts the initially preferred all-on-OVH arrangement and requires a separate decision.

## Core behavior and interpretation

1. **Discover** messages relevant to the user, including inbox and sent items, and authorized Teams messages. Calendar reveals real available windows. Begin with Outlook + calendar; add Teams only after verified rights and retrieval.
2. **Group** threads by client and issue; deduplicate repeated subjects and replies. Preserve lineage/provenance, suppress newsletters and irrelevant FYIs.
3. **Extract obligations**: a request from a client, promise by the user ('I will check tomorrow'), confirmed dates, dependencies, blockages, hand-offs, explicit resolutions. Do not interpret mere silence as resolution. Do not assign to user what another employee owns.
4. **Track states**: `NEW`, `TO_TRIAGE`, `IN_ANALYSIS`, `WAITING_ON_CLIENT`, `WAITING_ON_INTERNAL`, `BLOCKED`, `POSSIBLY_RESOLVED`, `CLOSED_CONFIRMED`. Ambiguous resolution is flagged rather than silently closed.
5. **Prioritize** by explicit deadline, work urgency, client impact, age, blocks, response obligations and user preferences, not solely newest email. Expose why item ranks high.
6. **Plan** from Outlook calendar busy slots and user-defined work hours, buffer for urgencies. Initial rough effort classes: 30/60/90 minutes; learn only from authorized feedback/actual logs, not invented billable time. Distinguish *estimated remaining effort* from *billable hours actually recorded*.
7. **Brief** each morning with at most a few important actionable items, available focus time, overdue promises and waiting-on items. When no access or no new evidence, say so explicitly.
8. **Reconcile** new messages with existing tasks instead of creating duplicates; retain audit trail of status changes from relevant source metadata.

## Example board (fictional)

| Client | Task | Status | Priority | Effort |
|---|---|---|---|---|
| Geo Construcciones | Validate IVA export interface | IN_ANALYSIS | High | 90m |
| Client B | Investigate report issue | NEW | Medium | 60m |
| Client C | Await correction confirmation | WAITING_ON_CLIENT | Medium | 30m |

These are examples only, **not live retrieved corporate records**.

## Graph access and architecture constraints

- Preferred technical path: supported OpenClaw tool/plugin or minimal read-only Microsoft Graph connector, scoped to user's delegated identity. Candidate permissions: `Mail.Read`, `Calendars.Read`, `Chat.Read`, but exact minimums and consent policies require tenant verification.
- Microsoft Teams bot integration is **not** equivalent to access to personal Teams chat history. Determine Graph permissions and actual reachable messages before promising coverage.
- Do not persist Graph refresh/access tokens in Git. Restrict scope, host storage and backups; implement token revocation instructions. No write scopes.
- Azure/Entra application registration and user/admin consent may be restricted. Check actual tenant status rather than infer permission from another employee's Power BI/Teams integration.
- Prefer a small task store under existing OpenClaw persistent volume, not independent infrastructure or a second orchestration platform.
- Direct inference with GPT Plus OAuth / DeepSeek / OpenRouter may disclose content to external model providers. Do not send corporate text until such processing is authorized; if permission only covers on-VPS processing, design non-LLM extraction or authorized local inference instead.

## Phases / acceptance

**W0 Access gate:** authorized read-only Graph and approved data processing; no deployment until permission is established. Verify OpenClaw version and read existing AGENTS.md/README.md/docs/CURRENT_HANDOFF.md.

**W1 Outlook/calendar read-only:** access inbox and sent, metadata and calendar; no writes; retrieve a small authorized sample and handle consent failure clearly.

**W2 Task extraction and board:** 20–30 known authorized messages spanning open, closed, FYI and delegated cases; target ≥90% recall for explicit user commitments on that sample, no false auto-closure, every task has traceable source, no duplicates.

**W3 Daily planning:** available time derived from real calendar; estimated effort explained and feasible; five workdays of useful concise briefings. No fabricated billable hours.

**W4 Teams read-only (optional):** prove actual permitted scope; add chat-derived commitments without over-collecting unrelated conversations.

**DONE:** the user receives a credible morning prioritization and follow-ups without manual entry, while corporate M365 has not been modified and all privacy gates are met.

## Decisions settled vs pending

**Settled:** private use only; run the organizer under existing OVH OpenClaw; no corporate outbound actions; minimal summarized persistent dashboard; automatic detection essential; Work isolated from Career.

**Pending:** organizational approval for data extraction/processing on personal VPS, Entra delegated access / tenant consent, allowed AI provider, sources/chats exact scope, actual Android delivery, retention policy and effort calibration. No production capability asserted.
