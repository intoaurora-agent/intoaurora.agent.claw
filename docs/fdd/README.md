# Aurora Agent — Functional Design Documents (FDD 01–10)

**Status: all DESIGN ONLY; no automated behavior has been deployed by publishing these files.**  
**Prepared:** 2026-11-09  
**Target repository:** `intoaurora-agent/intoaurora.agent.claw`  
**Runtime:** existing 24/7 OVH OpenClaw, no redesign.

These ten standalone specifications translate `docs/AURORA_AUTOMATIONS_MASTER.md` into implementable functional requirements. They are complementary to (not replacements for) existing `docs/AURORA_WORK_SPEC.md` and `docs/AURORA_CAREER_SPEC.md`. In case of conflict, resolve requirements explicitly rather than silently picking one version.

| ID | Function | Document | Priority |
|---|---|---|---|
| 01 | Personal Gmail triage | `FDD-01_PERSONAL_EMAIL_TRIAGE.md` | Later |
| 02 | Personal calendar organizer | `FDD-02_CALENDAR_ORGANIZER.md` | Later |
| 03 | **Corporate Work private task organizer** | `FDD-03_AURORA_WORK.md` | **Focus** |
| 04 | Argentina ERP/tax regulatory watch | `FDD-04_ARGENTINA_ERP_TAX_WATCH.md` | Later |
| 05 | Personal finance overview | `FDD-05_PERSONAL_FINANCE_OVERVIEW.md` | Later |
| 06 | Infrastructure monitoring | `FDD-06_INFRASTRUCTURE_MONITORING.md` | Later |
| 07 | English practice coach | `FDD-07_ENGLISH_PRACTICE_COACH.md` | Later |
| 08 | **Career discovery-to-interview assistant** | `FDD-08_AURORA_CAREER.md` | **Focus** |
| 09 | Operational memory | `FDD-09_OPERATIONAL_MEMORY.md` | Foundation |
| 10 | Consolidated daily briefing | `FDD-10_DAILY_BRIEFING.md` | Foundation |

## Usage for implementers
1. Read repository `AGENTS.md`, `README.md`, and `docs/CURRENT_HANDOFF.md` **when they exist**, plus the master plan and relevant FDD.
2. Inspect the **running** OpenClaw and reuse supported native capabilities. Do not assume an FDD feature already exists.
3. Confirm access/authorization gates, user decisions, and no unapproved paid API calls before enabling an integration.
4. Implement one functional slice at a time; verify source → action → persistent record → notification and failure states.
5. Record accepted evidence concisely in normal Git changelog/handoff, never write secrets or runtime databases to public Git.

## Known boundaries
- Corporate Work (#03): strictly read-only Microsoft 365; external access/processing needs employer authorization. Never cross its data into Career.
- Career (#08): actual applications and communications require explicit standing mandate, allowed platforms and controlled testing; no fabricated credentials or automatic negotiation.
- GPT Plus OAuth is not free DeepSeek/OpenRouter API. Never add paid spend without approval.
- Public repository must contain only sanitized docs and code. No resumes with private contact details, corp messages, tokens, SSH paths or SQLite records.
