# AURORA Career — continuation handoff

Updated **2026-11-17**. Overall operational acceptance: **PARTIAL**. Standing unlimited-qualified mode is enabled; a complete real employer-delivery/reply/browser-application lifecycle has not been proven.

## Repository and source of truth

Repository: **https://github.com/intoaurora-agent/intoaurora.agent.claw**, branch **main**. This is the project identified by the existing Career design and verified managed GitHub identity. The pre-closure branch head was `b80cf009f7470b108460c4a05a9c5de6a7c63ff9`. Use this file's GitHub History, or `git log -1 --format=%H -- docs/CURRENT_HANDOFF.md`, to identify its documentation commit; do not confuse the baseline SHA with the closure commit.

Read [Career operational status and evidence matrix](AURORA_CAREER_SPEC.md), [README](../README.md) and [changelog](../CHANGELOG.md). The older automation master and FDDs are historical design references, not proof of runtime acceptance. This handoff supersedes the old local statements that Google consent is pending or Career does not exist. Do not repeat OAuth or run inactive Google prototype scripts based on those historical reports.

The local `/home/ubuntu/aurora-openclaw` deployment directory has no initialized Git checkout/remote. Publish only an explicit sanitized documentation allowlist to the existing repository. Do not initialize/import the deployment or persistent agent workspace into Git. The repository is public; no CV, candidate/contact data, application records, raw logs, cookies, OAuth artifacts or personal Google account details belong here.

## Objective and fixed boundaries

Continue a genuinely autonomous recruitment workflow using the EXISTING OpenClaw deployment, not a new platform. Preserve state/history, candidate truthfulness, privacy, official channels and Professional Communication v1.0. No new agents, services, databases, middleware, recurring jobs, paid APIs, OpenClaw upgrade, OAuth changes, sandbox weakening, CAPTCHA/access-control bypass, unsolicited generic campaigns or employment commitments.

This closure audit sent no applications, recruiter messages or follow-ups and did not trigger a live application cycle, disable schedules, or alter production instructions/authorization. Any future task must state its allowed external effects; do not use a live Daily cycle as a harmless test.

## Functional architecture and current schedules

- Existing healthy OVH Gateway: **OpenClaw 2026.11.1 (4ffdd20)**; persistent Docker state at `/home/node/.openclaw`.
- Aurora Main is the owner interface; existing `career` agent is the recruitment specialist. Native Main/Career messaging has historical actual acknowledgements; owner-device delivery is separate and unverified.
- Career and both recruitment jobs: **`openai/gpt-6.1-sol`, medium reasoning**, existing isolated sessions and tool policy, delivery `none`.
- **Daily Job Discovery:** enabled, daily **09:00**, timezone **America/Argentina/Buenos_Aires**.
- **Recruitment Inbox Manager:** enabled, hourly, same timezone, native staggering up to five minutes. No extra recurring task.
- Native managed Chromium is headless and ready with sandbox enabled. Existing Gmail read/send and original PDF attachment functionality have actual evidence; use protected Gateway execution, never arbitrary shells or credential dumps.

The private Career workspace is `/home/node/.openclaw/openclaw/workspace/career`. Read FULL live AGENTS.md, USER.md, MEMORY.md, recruitment/operations.md v4.0, candidate-profile.md, pipeline.json, inbox-state.json, workflow-control.json and the owner-authorization source. Bootstrap context may be truncated; do not infer missing facts or authorization from old messages.

## Standing authorization and queue behavior

Current owner authorization is **approved=true**, **ALL_QUALIFIED_OPPORTUNITIES**, with **no daily, weekly, per-run attempt/success, discovery-result or queue-size numerical quota**. Numerical limits in old test/grant history are superseded. Require score **>=75/100 AND verified mandatory eligibility**, a genuinely active vacancy and a verified legitimate application destination. Exclude the current employer, duplicates and unresolved blocked/uncertain channels. Use the original verified CV; no invented candidate facts, terms, availability, salary, qualifications or consent.

Existing Daily discovers/evaluates all encountered permitted opportunities, persists every qualified item and processes sequentially. Queue and per-opportunity execution_ledger reservations live in the EXISTING pipeline.json. Short atomic state transactions preserve history; final-action intent is checkpointed before send/submit. Persist independent SENT/browser confirmation evidence before the next item, then merge inbox tracking. Preserve unfinished queue and discovery continuations when real session/time/tool capacity interrupts; the next EXISTING scheduled execution resumes.

A pre-submit block is isolated. SUBMISSION_PENDING without an independently established result becomes UNCERTAIN and stays held across restarts/date changes; do not re-send, change channels or clear it by age. Reconcile the original action first. Already submitted/bounced applications stay deduplicated; continue independent qualified records. Pipeline evidence can reconstruct a missing inbox registry write. These are agent procedures with simulated recovery evidence, not an enforced distributed exactly-once guarantee.

Inbox handles all relevant threads, separate DSNs, routine factual replies, evidenced follow-ups and important escalations. Keep SENT/SUBMITTED, independently supported DELIVERED, BOUNCED, BLOCKED and UNKNOWN distinct. A bounce is not rejection; SENT/silence is not receipt. Interviews, offers, sensitive declarations and personal commitments go to Main; no automatic acceptance or promises.

## What is actually confirmed

**VERIFIED_REAL:** scheduled public-source discovery and profile-based evaluation; historical individual official-email applications with original PDF and independent SENT readback; tracked threads; authenticated DSN correlation and blocked-delivery preservation; normal hourly Gmail processing; persistent queue reconciliation; recorded Main acknowledgements. The November 17 09:00 ART Daily search ran successfully. The inspected 13:00 ART hourly cycle completed quietly, reconciled 14 queue records, found no new relevant reply and sent nothing.

**VERIFIED_SIMULATION:** the actual Daily scheduler executed isolated local fixtures: 25 qualified items -> five pre-submit blocks plus twenty simulated sends; an 80-item fixture completed; disk/new-process continuation, repeated-run deduplication, unresolved uncertainty isolation and simulated send-before-checkpoint crash recovery passed. No real employer transport was used.

**CONFIGURED_NOT_YET_VERIFIED:** positive employer receipt, genuine recruiter reply and autonomous follow-up, completed permitted browser application, real-service crash/reboot/concurrency recovery, interview/offer escalation and final owner-device delivery. The latest Daily after unlimited activation was validation, not a live unlimited application run.

**BLOCKED:** selected channels/forms for missing mandatory facts, human verification or authenticated recipient-policy non-delivery. The private 14-case snapshot has seven blocked-before-submission, one submitted/SENT with receipt unknown, five closed and one bounced; no runnable qualified item then. Existing named case histories remain private and unchanged, including the correction of a prior overclaimed email E2E PASS after a bounce. Never report those cases as confirmed delivery or successful browser submission.

The full public-safe matrix distinguishes these evidence levels in AURORA_CAREER_SPEC.md. Detailed records stay privately on OVH.

## Closed portal investigation

Computrabajo Argentina: owner-reported HTTP 403 from OVH Chromium. ZonaJobs Argentina: owner-reported security block before Google authentication. Bumeran Argentina: documented platform restriction; no equivalent technical block observed. Existing accounts use Google Sign-In; no Google login completed on OVH. Session persistence does not override site rules; Windows requires a running Windows environment and cannot provide the independent OVH goal. All three integrations are **BLOCKED / DEFERRED**. No further implementation, proxies, bypasses or custom middleware are authorized. Independent permitted discovery/application channels remain active.

## Next practical phase

Observe normal scheduled operation rather than build another layer. Inspect targeted scheduler receipts, actual eligible queue items and outcome evidence. If a suitable permitted opportunity exists, let the standing workflow establish a genuine confirmed transport/receipt and recruiter-response lifecycle; do not manufacture a test recipient or infer success from SENT. Resolve only genuinely essential candidate unknowns, preserve all blocked/uncertain history and avoid repeated portal work. After legitimate real outcomes, validate narrowly scoped recovery and owner-notification delivery without replaying uncertain submissions.

For troubleshooting: inspect health, browser status, cron list/runs and current private control/records read-only. Verify an old lock's owner run has ended before recovery. Use fresh backups and merge affected records; never replace the live state volume. Do not expose or replace existing credentials. No critical recruitment regression was confirmed at closure; remaining gaps are explicitly unverified outcomes and channel limitations.
