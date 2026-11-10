# FDD-09 — Operational memory and durable task continuity

> **Status:** FUNCTIONAL DESIGN — NOT IMPLEMENTED / NOT ACCEPTED  
> **Target:** Existing OpenClaw on OVH, Docker/headless, accessible from Windows and Android  
> **Timezone:** `America/Argentina/Buenos_Aires`  
> **Privacy:** Public-safe specification. Do not commit personal/corporate content or credentials.

**Cross-cutting contract.** Reuse the existing running OpenClaw, its supported agents/tools, native cron/heartbeat and persistent storage. Do not redesign VPS/network/authentication, change the main model, or incur API costs without explicit approval. Separate Work (corporate) from Career (personal recruiting). Scheduled tasks must not silently duplicate existing automations. No function is DONE based solely on a created cron job; prove live permitted data, persistence after restart, delivery, failure visibility and recovery. Android notifications must be checked, not assumed.

## 1. Objective
Make Aurora remember decisions, pending actions and project status **across conversations and restarts** without treating a chat transcript as a reliable task database. This functionality supports all modules, especially Work and Career, while preserving isolation between them.

## 2. Inputs and scope
Explicit user decisions, user-authorized session data, module task state, structured results and event times. Respect existing working OpenClaw session/memory features; reuse before adding custom infrastructure. Do not indiscriminately memorize private mail, employer records or secrets.

## 3. Functional requirements
- **FR01 Capture:** distinguish verified decision, proposed idea, question, task, due date and completed task; only label a fact confirmed when evidence exists.
- **FR02 Recall:** retrieve history by topic/time/project, including source reference when available; never claim a missing context is known.
- **FR03 Lifecycle:** task states `PROPOSED`, `ACTIVE`, `WAITING`, `DONE_VERIFIED`, `CANCELLED`; record who/what changed a state and when.
- **FR04 Isolation:** separate agent-specific memory/workspace and structured records; Work restricted corporate data does not leak into Career.
- **FR05 Reconciliation:** update existing decision/task rather than making duplicate entries from repeated conversations or scheduled checks.
- **FR06 Persistence:** memory and task state survive container restart, recover from supported encrypted off-host backups and can be verified after restore.
- **FR07 Control:** user can inspect and correct inaccurate entries and identify records that should not be retained.

## 4. Storage and retention
Use supported OpenClaw memory/search where sufficient; a small structured ledger is justified only for strong state guarantees (e.g., Career application status). Backup runtime state encrypted to an approved location outside OVH; exclude tokens from Git. Set retention and deletion policies per data category. Public docs describe functionality only.

## 5. Failure cases
No memory search results must yield 'unknown', not fabricated recall. If persistent data store unavailable, scheduled tasks must not silently mark work done. If backup is stale or missing, alert and mark recovery protection degraded.

## 6. Acceptance
Recall 10 known user decisions and 5 tasks after a fresh session and container restart; avoid duplicated pending tasks; test supported non-destructive recovery of a backup in isolated environment. Confirm corporate/personal memory separation.

## 7. Dependencies and decisions
Exact state store and backup support in deployed OpenClaw version, retention schedule, offsite destination, encryption/key recovery, authorized user corrections and interplay with existing memory feature configuration. Related: all FDDs.
