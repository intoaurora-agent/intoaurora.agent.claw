# FDD-10 — Consolidated personal briefing and proactive alerts

> **Status:** FUNCTIONAL DESIGN — NOT IMPLEMENTED / NOT ACCEPTED  
> **Target:** Existing OpenClaw on OVH, Docker/headless, accessible from Windows and Android  
> **Timezone:** `America/Argentina/Buenos_Aires`  
> **Privacy:** Public-safe specification. Do not commit personal/corporate content or credentials.

**Cross-cutting contract.** Reuse the existing running OpenClaw, its supported agents/tools, native cron/heartbeat and persistent storage. Do not redesign VPS/network/authentication, change the main model, or incur API costs without explicit approval. Separate Work (corporate) from Career (personal recruiting). Scheduled tasks must not silently duplicate existing automations. No function is DONE based solely on a created cron job; prove live permitted data, persistence after restart, delivery, failure visibility and recovery. Android notifications must be checked, not assumed.

## 1. Objective
Deliver one concise, trustworthy daily briefing that merges status from **only enabled and authorized** Aurora functions, so the user knows what matters without opening ten dashboards. The briefing is a presentation layer, not a second parallel planner or a source of invented facts.

## 2. Input contract
Each upstream module returns `module`, `status` (`OK` / `STALE` / `UNAVAILABLE` / `NOT_CONFIGURED`), `last_checked_at`, limited top items with source references, confidence and next action. Data included only with applicable consent: personal mail, personal calendar, Work priorities, Career interest, infrastructure alerts, tax briefings, finance and language reminder. Work and Career remain logically isolated; private Work details must not be forwarded to recruiting workflows.

## 3. Requirements
- **FR01 Aggregate:** proposed daily 08:15 local, collect latest state with clear freshness cutoffs; never trigger expensive full re-scans of all modules solely for a briefing.
- **FR02 Rank:** urgent deadlines, actionable recruiter replies, service outages and time-bound promises above FYI. Collapse duplicates and related topics.
- **FR03 Format:** headline, top 3 priorities for today, relevant meetings, urgent messages, blocked/waiting items and at most a few optional extras. Offer source links/details upon request.
- **FR04 Availability:** show missing modules as **not checked/unavailable**, never as 'zero issues'. Indicate if corporate Work data has not been authorized.
- **FR05 Quiet delivery:** send once per day through a verified authorized channel, avoid repeating identical push notices. High-impact exceptions may alert outside daily briefing according to explicit policy.
- **FR06 Interactive:** user can ask 'why this priority?', 'what can wait?' or request rescheduling proposals, while source modules remain authoritative.

## 4. Example output (fictional)
`Today: 2 events, 3 high-priority tasks, 1 job recruiter reply, infrastructure healthy as of 08:10. Work tracker unavailable (authorization pending). Suggested: address one client promise before 11:00, then prepare afternoon meeting.`

The system must **not** state 'infrastructure healthy' without a successful recent check. Numeric examples above are invented for design demonstration.

## 5. Failure and security
If one module errors, produce a partial briefing clearly labeling the gap rather than suppressing the entire message. Avoid disclosing corporate client names, finance figures or sensitive recruiting replies on a lock-screen notification. No automatic posting into Teams/Outlook or external public channels.

## 6. Acceptance
Seven consecutive daily briefings with correct timestamp, no duplicate delivery, defensible top priorities, verified partial-failure behavior and accurate data freshness. Works without Windows powered on and from Android after the delivery channel is confirmed.

## 7. Dependencies and open decisions
Enabled upstream modules, briefing time, notification privacy level, quiet hours, Android access verification and fallback when no channel is available. Related: FDD-01 to FDD-09.
