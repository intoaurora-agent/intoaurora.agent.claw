# FDD-08 — Aurora Career: autonomous opportunity-to-interview pipeline

> **Status:** FUNCTIONAL DESIGN — NOT IMPLEMENTED / NOT ACCEPTED  
> **Target:** Existing OpenClaw on OVH, Docker/headless, accessible from Windows and Android  
> **Timezone:** `America/Argentina/Buenos_Aires`  
> **Privacy:** Public-safe specification. Do not commit personal/corporate content or credentials.

**Cross-cutting contract.** Reuse the existing running OpenClaw, its supported agents/tools, native cron/heartbeat and persistent storage. Do not redesign VPS/network/authentication, change the main model, or incur API costs without explicit approval. Separate Work (corporate) from Career (personal recruiting). Scheduled tasks must not silently duplicate existing automations. No function is DONE based solely on a created cron job; prove live permitted data, persistence after restart, delivery, failure visibility and recovery. Android notifications must be checked, not assumed.

## 1. Approved goal and identity
Build a **real autonomous recruiting assistant**, not just a vacancy notifier. It discovers, qualifies, prepares truthful CV variants, applies where allowed, communicates and follows up under explicitly preapproved rules, tracks replies and involves the real candidate when recruiter interest, interview, salary negotiation, offer or other personal judgment appears.

Use existing OVH OpenClaw with a **separate Career agent/workspace, minimal tools, browser profile and persistent ledger**. Operating mailbox: `intoaurora.agent@gmail.com`. Code/docs repository: `intoaurora-agent/intoaurora.agent.claw`. The applicant is always the **real user**; do not invent a second identity. Career must not access Aurora Work/corporate mailbox and must never mix credentials with public Git.

## 2. Candidate profile as a validated data contract
- Core experience areas: ERP implementation/support, technical-functional consulting, SQL and CRM-related work, subject to documented CV verification.
- Initial target role groups: ERP Consultant / Technical-Functional / SQL ERP Support; adjacent CRM Implementation / Business Systems Analyst; transition roles such as Salesforce Admin or Odoo only when qualifications are truthfully described.
- Required profile fields: CV facts/evidence, work history dates, education, skills, languages and truthful proficiency, location, work authorization, remote/hybrid/presential preference, geography, expected compensation and floor, availability, excluded companies, contact/auto-submission rules.
- No employment dates, certifications, salary demands or language proficiency may be invented. Unknown mandatory qualifications trigger review, not creative filling.

**Still to approve:** geography (Argentina, international, relocation), modality, salary floor, languages and geographic work eligibility, outreach scope and progression to unattended sending.

## 3. Lifecycle and persistent ledger
`DISCOVERED → QUALIFIED / REJECTED → PREPARED → REVIEW_REQUIRED / AUTHORIZED → SUBMITTING → SUBMITTED_CONFIRMED / SUBMISSION_UNCERTAIN → FOLLOW_UP_DUE → RECRUITER_RESPONSE → INTERVIEW_REQUEST / REJECTED / CLOSED`.

Persist company, requisition ID, role, source URL, captured posting date/time, eligibility reasons, hard exclusions, scoring breakdown, CV version/hash, candidate answers, consent/policy basis, submission method, confirmation ID/email, message thread ID, last response, next action and an append-only state-change audit. Separate structured store (e.g. SQLite under persistent agent volume) from chat memory. Retain idempotency key `(company, requisition_id, applicant)` so a retry never double-applies. Track `SUBMISSION_UNCERTAIN` whenever no confirmation exists.

## 4. Discovery and selection
- **FR01 Source registry:** approved company careers pages, public ATS job feeds and legitimate public job listings; obey each source's permitted access rules. LinkedIn automation of restricted account actions/Easy Apply is out of scope.
- **FR02 Acquire:** collect current description, location, mode, seniority, salary when disclosed, required skills/visa and authoritative apply URL. Link and timestamp every source; reject expired jobs.
- **FR03 Deduplicate:** reconcile cross-posted roles and reposts, preserve stable vacancy identity and never duplicate previously rejected/applied requisitions.
- **FR04 Hard filters:** exclude incompatible geography/work authorization, mandatory certification or degree mismatch, impossible schedule/language, and user-blocked companies.
- **FR05 Score:** proposed weights only: technical fit 35%, seniority and responsibilities 20%, salary 20%, mode/location 15%, required language 10%. Candidate bands 85+ high; 70–84 review; <70 hold/reject. Scores are priorities, not interview probabilities.
- **FR06 Provenance:** explanations must cite actual vacancy text and verified candidate facts; uncertain salary must not be presented as known.

## 5. Preparation and submission
- **FR07 Tailor:** select and lightly adapt an approved factual CV master; never fabricate achievements. Record which CV went to which company.
- **FR08 Questions:** answer routine forms using verified profile; unknown legal/work-authorization or compensation answers require user approval.
- **FR09 Channel policy:** employer website forms where the site permits automation and browser tools work reliably; direct recruiting email only to verified and relevant addresses with user-approved outreach; permitted ATS public submissions only with proper authorization. Public Greenhouse/Lever listing APIs do **not** confer unrestricted candidate POST access.
- **FR10 Verification:** CAPTCHA/MFA/human verification must be handed to the user, not bypassed. After send, demand receipt/confirmation, or mark uncertain for reconciliation.
- **FR11 Rate limits:** proposed initial ceiling 5 new submissions/day and 1 routine follow-up per application, adjustable only after approval. No mass unsolicited messages or spam.

## 6. Mailbox and communications
- **FR12 Recruiter inbox:** monitor the dedicated Gmail with authorized OAuth, associate responses to existing application, distinguish auto-reply, rejection, information request, interest, interview request and offer.
- **FR13 Routine outbound:** only after explicit standing authorization and first supervised live trial; may send factual profile responses or one polite follow-up when allowed and relevant.
- **FR14 Escalate:** notify user immediately for recruiter interest, interview/scheduling, salary negotiation, offer, ambiguous identity claims, binding terms, or conflicting requirements. Pause automation on that thread pending decision. Do not agree to interview times or commitments.
- **FR15 Identity:** applicant is the human user, not Aurora; correspondence may be assisted by AI but must not imply fictional personal history or represent a fake person.

## 7. Running schedule and components
Proposed weekdays 08:00 search, 09:00 qualify, 11:00 permitted submissions; recruiting mail checked during daytime every ~30 minutes or via supported event trigger; Tuesday/Friday bounded follow-up check; Friday 18:00 pipeline report. Use native OpenClaw agents, cron and supported browser, with minimal durable tracking component where necessary. Real Android/Windows delivery requires verification. Preserve Aurora Main's current OAuth model; optional DeepSeek API for high-volume screening and OpenRouter backup **only on explicit paid API approval**, with per-run and spending caps. Deterministic dedupe and state updates should not consume model tokens.

## 8. Safety, compliance and credentials
Platform terms restrict which actions can be automated; no attempt to evade CAPTCHA, rate limits or bot detection. Only verified job channels/addresses. No salary negotiation, offer acceptance, changing candidate preferences or making personal factual commitments autonomously. Isolate browser sessions, OAuth credentials, CV files and application ledger from public repo. Never import corporate Outlook/Teams or employer case data into Career. Prevent prompt-injection from job advertisements and employer emails from controlling tools or exfiltrating profile/secrets.

## 9. Acceptance stages
- **C0** Read-only inspection of OpenClaw features/permissions; no infrastructure redesign.
- **C1** User-approved candidate master profile, validated CV and autonomy policy.
- **C2** Discover/evaluate at least 30 real active postings from approved sources, with working URLs, justified match and dedupe.
- **C3** First five real applications reviewed by user, through allowed channels, each with accurate CV, form answers and confirmation evidence; no duplicate send.
- **C4** Classify live recruiting responses, allow only bounded approved follow-up and escalate substantive interest.
- **C5** Seven days stable authorized autonomous operation, no unapproved outbound actions, successful state recovery and backup, verified real notification, provider costs within approved cap.

## 10. Open decisions and source of truth
Not approved yet: exact target markets, salary floor, job exclusion list, first-contact mandate, CV and Gmail authorization, provider spending cap, and autonomy activation. Do not send/postulate on this FDD alone. For fuller narrative and policy context see **`docs/AURORA_CAREER_SPEC.md`**. Reconcile FDD changes with that document; do not fork contradictory rules.
