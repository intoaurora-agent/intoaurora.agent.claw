# AURORA CAREER — Autonomous job-search and applications agent

Status: **FUNCTIONAL DESIGN; NOT DEPLOYED / NOT AUTHORIZED TO SEND**  
Date: 2026-11-09

## Mission and fixed identity

Build on the **existing persistent OpenClaw in OVH (Docker/headless)**. Candidate is the real user. Agent operates as an assistant, **not as a fictitious applicant**. Operational email: `intoaurora.agent@gmail.com`; code/docs target repository: `intoaurora-agent/intoaurora.agent.claw`. Do not use personal GitHub identity as the agent's repository or mix credentials/runtime data into Git.

The key requirement: **do more than search web vacancies**. Automatically discover, qualify, tailor verified CV/answers, apply using permitted channels, make cautious contact/follow-ups where authorized, interpret responses, track every application and only interrupt the user for genuine recruiter interest, interviews, personal judgments or decisions outside the standing mandate.

A fully universal unattended application bot is not realistic. LinkedIn restricts automation; employer ATS APIs may require employer-owned credentials; CAPTCHA, authentication, verification and terms must be respected. Do not promise 100% unattended applications and never evade controls or restrictions.

## Pipeline and durable state

`DISCOVERED → QUALIFIED/REJECTED → PREPARED → REVIEW_REQUIRED/AUTHORIZED → SUBMITTING → SUBMITTED_CONFIRMED → FOLLOW_UP_DUE → RECRUITER_RESPONSE → INTERVIEW_REQUEST / REJECTED / CLOSED`.

Persist in a private structured store, separate from conversational memory: source URL and discovery timestamp, job requisition and company, match breakdown and hard filters, evidence for claimed experience, CV version/hash, answers, contact channel, authorization basis, actual submission confirmation and timestamp, message IDs, follow-up schedule, next action, errors and audit trail. **Never** infer submission merely from button click; require confirmation/receipt or mark `SUBMISSION_UNCERTAIN`. Idempotency by company/job requisition/application identity prevents duplication. Separate backing store and backups from Work.

## Candidate profile and criteria

Initial **proposed** roles, requiring final user confirmation:

- Direct match: ERP Consultant, Technical-Functional Consultant, ERP Support, SQL/ERP Analyst.
- Adjacent: CRM Consultant, Implementation Specialist, Application Support, Business Systems Analyst.
- Transition (only truthful skills): Salesforce Administrator, Odoo Consultant.

Verified experience to emphasize: implementation/support of ERP/CRM in Argentina, Softland technical-functional operations, SQL and customer issue analysis. Do not claim Salesforce administration or other unproven skills. Truthfully specify languages (Spanish/Russian; English level must be verified), technologies, dates, seniority, education, compensation, work eligibility, availability and location.

**Proposed weights only:** technical match 35%, responsibilities/seniority 20%, salary 20%, mode/location 15%, language 10%. Bands proposed: 85–100 priority, 70–84 inspect, <70 reject/hold; hard exclusions apply first. A match score is not an interview probability. User must settle geography (Argentina/international/relocation), remote/hybrid/presential, salary threshold, contact mandate and sending policy before live actions.

## Source and application channels

- Public company career pages and published ATS job feeds, plus public vacancy sources allowed by their terms.
- Greenhouse/Lever public job listings are discovery sources; their submission APIs often require employer-side keys. Browser forms may work where site permits them, but verify terms and any identity challenges. No unsupported API POST claims.
- LinkedIn: discovery via permitted alerts/public pathways; do **not** automate restricted LinkedIn account actions, connection requests or Easy Apply via bots.
- Verified recruiting addresses: personalized application or outbound introductory email only with validated recruiting relevance, authorized by user and under limits; no mass mailing.
- Regional portals: classify per portal whether automation is permitted and practically viable before enabling submission.

## Permitted autonomy and escalation

**Autonomous immediately after setup:** sourcing, deduplication, fit analysis, drafts of CV/cover letters/questions, tracking and passive mailbox classification. No sending until approved policy and dry run.

**Progressive autonomy proposal:** first five real applications reviewed by user and submitted through approved channels; then permit autonomous applications **only** for verified matches/channels within precise standing rules. No automatic submission where TOS forbids bots, CAPTCHA/verification appears, qualifications are uncertain, or salary/location constraints are unknown. Initial ceiling suggestion: five new applications/day, one routine follow-up per application, bounded frequency and rate limits. These are proposals pending approval.

**May reply under standing authorization** only to routine factual requests using verified candidate profile, and acknowledge receipt where appropriate. Never invent credentials, misstate identity, negotiate salary, commit dates, accept offers/terms, impersonate anyone else, falsify answers or agree to interview slots. For recruiter interest, substantive questions, interview requests, salary discussion or offers: notify the user and pause for a decision. Outbound emails must identify the real candidate and be professional; do not falsely imply handwritten origin when that matters.

## Mailbox and schedule

Use `intoaurora.agent@gmail.com` **only after proper account OAuth and granted permissions** for hiring workflow. Mailbox monitors acknowledgements, recruiting replies, rejections, scheduling requests and actual offers. Initially read-only; enable outbound only for explicit approved mandate. Proposed routine: weekdays 08:00 discover, 09:00 rank, 11:00 apply where allowed, daytime inbox review roughly every 30 minutes (efficient event option if available), Tuesday/Friday follow-up checks, Friday 18:00 weekly report. Avoid duplicate scheduled runs, unnecessary model tokens and after-hours spam.

## Agent design on OpenClaw

Use a separate OpenClaw agent/workspace/tool permissions and browser profile for Career, inside existing Gateway. Do not build a new orchestration system. A small SQLite or similar durable job ledger is justified where native session memory cannot enforce application state and idempotency. Protect browser sessions and credentials; log minimal events, no CVs/secrets in public Git. Notifications via existing Android/Windows access **after verifying delivery**.

Model policy: preserve current Aurora Main GPT Plus/Codex OAuth. Test officially supported DeepSeek API for inexpensive bulk screening **only with explicit spending authorization**, small cap and a quality benchmark; OpenRouter optional later. Paid provider subscriptions not covered by Plus. Use deterministic rules for duplicate detection and state transitions, LLM only where needed. No hidden pay-as-you-go fallback.

## Practical stages and DONE criteria

- **C0 Inventory**: inspect existing repo/agent and runtime (AGENTS.md, README.md, docs/CURRENT_HANDOFF.md), available native agents, browser and Cron; no production changes.
- **C1 Candidate policy**: user validates real CV claims, targets, geography, compensation, languages, contact and consent rules. No invented experience.
- **C2 Discovery**: verify 30 live legitimate postings from approved channels, show defensible reasons and working URLs, remove duplicates, reject mismatches.
- **C3 Real applications**: first five user-reviewed applications from permitted channels; stored versioned CV and confirmation evidence, no accidental duplicates. Only then consider autonomous sending.
- **C4 Recruiting replies**: evidence-based classification and one bounded follow-up, escalate recruiter interest and interviews immediately; no user commitments without approval.
- **C5 Stable autonomous operation**: seven days without duplicate sends or unauthorized actions, durable ledger after restart, real alerts, periodic backup and controlled budget.

## Risks and open decisions

Platform restrictions, recruiter-address verification, CV truthfulness, application/communication authorization, email account access, candidate consent, payout/API caps, browser identity challenges, potential recruiter reputation damage, secure storage and recovery. Career must be entirely separated from corporate Work data.

**Current state:** design captured, no registered agent, Gmail OAuth, deployed automation, API spend or submitted applications verified by this document. Do not label IMPLEMENTED until validated on live infrastructure.
