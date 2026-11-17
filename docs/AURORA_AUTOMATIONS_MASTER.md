# AURORA PERSONAL — Functional automations master plan

Status: **DESIGNED / NOT DEPLOYED**  
Date: 2026-11-09  
Repository target: `intoaurora-agent/intoaurora.agent.claw`  
Operational email: `intoaurora.agent@gmail.com`  
Timezone: `America/Argentina/Buenos_Aires`

## Operating context and principles

The single persistent OpenClaw installation runs headless in Docker on OVH, with existing Windows access and the Android companion path. Keep its existing Gateway, authentication, OAuth model and memory unchanged unless a specific feature requires a justified change. The VPS operates 24/7 independently from Windows. Use OpenClaw's supported agent, tools, configuration, skills and scheduler before custom code. Git is for code and sanitized specifications, **not** email, credentials, CVs, sensitive corporate data or runtime databases. Codex performs technical work; technical prompts to Codex must be in professional English.

A proposed capability is not a deployed capability. Each item becomes DONE only after verified operation against live authorized data, reliable persistence and user-visible results. Never confuse ChatGPT Plus OAuth with paid model API entitlement; DeepSeek and OpenRouter are separately billed and need explicit authorization and spending caps.

## Ten personal automation candidates

| # | Capability | Input / trigger | Expected output | Implementation caveat |
|---|---|---|---|---|
| 1 | Personal email triage | Authorized Gmail; 15–30-minute check or event | Priority alerts, classification, proposed drafts | No outbound send or delete without explicit policy |
| 2 | Calendar organizer | Personal calendar, morning and before event | Daily agenda, meeting preparation, reminders | Read-only initially |
| 3 | **Aurora Work — private work tracker** | Corporate Outlook, Teams and calendar via authorized Microsoft Graph | Per-client task/status board, priorities, effort and daily plan | See dedicated spec; no corporate outbound action, access and external processing subject to employer policy |
| 4 | Argentine tax/ERP change watch | Weekly official ARCA, ARBA and provincial references | Source-linked compliance-impact briefing for ERP | Verify effective dates; never silently modify production |
| 5 | Personal finance overview | Authorized extracts/user records | Monthly spending, estimated balance/savings | No assumed bank access; no transfers |
| 6 | Infrastructure monitoring | OVH, Contabo, GitHub service status, periodic deterministic checks | Failure alerts and operational summaries | No LLM per heartbeat; no autonomous root/SSH repairs |
| 7 | English practice coach | Weekday scheduled nudge and user practice | Short ERP interview conversation, error tracking | Real-time voice availability requires separate verification |
| 8 | **Aurora Career — autonomous job-search pipeline** | Public permissible sources, candidate profile, personal recruiting mailbox | Ranking, tailored applications where allowed, cautious outreach and follow-up, escalation for interviews | See dedicated spec; platform terms, identity and approval boundaries |
| 9 | Operational memory | Authorized conversations, choices and commitments | Searchable decisions, progress and reminders | Persistent state + tested backup, minimize secrets |
| 10 | Consolidated morning briefing | Data from other enabled modules, 08:15 proposed | Short actionable overview | Do not report unavailable inputs as successful checks |

Suggested cadence, not yet approved: 08:00 calendar; 08:15 briefing; weekday 17:30 work check; Mondays 09:00 tax; Fridays 18:00 jobs; weekdays 20:00 English; 5-minute deterministic service checks. Avoid duplicating existing ChatGPT automations without review.

## Delivery and sequencing

1. **Foundation**: inventory running OpenClaw version, Docker persistence, native Cron/Heartbeat, access/notification channels, existing tasks and backup/restore; read-only inspection before changes. Confirm actual Android notification delivery rather than assume it. Preserve existing successful deployment.
2. **Core productivity**: calendar + daily briefing + task memory; Gmail triage after account authorization.
3. **High-value prioritized tracks**: Aurora Work (#3) and Aurora Career (#8), independent identities, permission sets and storage; detailed contracts in adjacent files.
4. **Remaining workflows**: regulatory briefings, finance, deterministic monitoring, language practice.
5. **Acceptance**: objective evidence, real source data, no duplicates, alerts when missing, validated persistence and recoverability.

## Risk, privacy and operational controls

- **Isolation**: Career cannot access corporate Outlook/Teams or company documents; Work cannot read Career recruiting mail or impersonate user. No common privileged tools by default.
- **Corporate data**: even summarized client/task/status information can be confidential. Reading and transiently processing Microsoft 365 content on an external personal VPS is data transfer. Approval and minimization are required; local-first processing on OVH does not mean the raw source never leaves Microsoft 365. Paid/API LLM calls could transfer it to additional processors.
- **Actions**: personal Gmail drafts are not sends. Career sending is permitted only after defined user authorization, tested channels and limits. Work always remains read-only in Microsoft 365.
- **Resilience**: off-host encrypted backup of OpenClaw state, integrations configuration and task state; restore verification; do not commit secrets or live SQLite databases.
- **Cost**: use deterministic checks for scheduling/deduplication/state; cap recurring AI calls and monitor API spend. Existing GPT Plus/Codex OAuth works within provider limits; do not assume unlimited/background access.
- **Change management**: one narrow production change at a time, reversible, recorded briefly in changelog/handoff. Do not touch VPS SSH/firewall without explicit approval.

## Acceptance gates

- Data retrieval performed with the user's/organization's permission, source references retained where permitted.
- Useful, correct results from live authorized sources; identify unknowns instead of inventing status.
- Scheduled work executes without a running Windows PC and can be consulted from Windows and Android.
- Repeated execution is idempotent, failures visible, no silent duplicate sends or cases.
- State survives agent/container restart and is covered by an offsite verified backup.

## Current disposition

All 10 automations above are **design proposals, not confirmed production features**. Work and Career are the immediate design priorities. The present file captures decisions and requirements so future chats/implementers should read the repository rather than reconstruct project intent from conversation history.
