# Aurora Career — final operational audit and implementation status

Audit date: **2026-11-17**. Overall status: **PARTIAL**. Unlimited qualified application authorization is enabled; this is not proof of a complete real-world recruitment lifecycle. This document supersedes the November 9 design-only implementation status and proposed numerical quotas. Prior versions remain in Git history. Current live owner instructions take precedence over historical designs.

## Production architecture and authorization

Reuse the existing OpenClaw **2026.11.1 (4ffdd20)** on OVH. Aurora Main is the owner interface; the existing `career` agent is the specialist. Career and both recruitment automation payloads select `openai/gpt-6.1-sol`, medium reasoning. Native Main/Career permissions and recorded acknowledgements establish an existing communication route; notifications reaching the owner's devices are a separate unverified step.

| Component | Current state |
| --- | --- |
| Gateway | Running and healthy; the audit did not restart or reconfigure it |
| Daily Job Discovery | Enabled; `0 9 * * *`, `America/Argentina/Buenos_Aires`; agent `career` |
| Recruitment Inbox Manager | Enabled; `0 * * * *`, same timezone; native staggering up to five minutes; agent `career` |
| Execution | Existing isolated `agentTurn` sessions, medium reasoning, full-context disk reads, existing trusted tool policy; runner delivery remains `none` |
| Browser | Native managed headless Chromium; running, CDP/page ready, `noSandbox=false`; persistent profile in the existing state volume |
| Gmail | Existing verified integration, protected Gateway execution and managed credentials; no OAuth changes |
| State | Existing `openclaw-state` Docker volume mounted at `/home/node/.openclaw`; scheduler in its existing SQLite store, Career pipeline/queue as workspace JSON |
| Authorization | `approved=true`, `ALL_QUALIFIED_OPPORTUNITIES`, no daily/weekly/per-run attempt, success or discovery-count quota; configuration validation guard is off |

The private Career workspace is `/home/node/.openclaw/openclaw/workspace/career`. Read full AGENTS.md, USER.md, MEMORY.md, recruitment/operations.md v4.0, candidate-profile.md, pipeline.json, inbox-state.json, workflow-control.json and the current owner-authorization source. Bootstrap snippets can be truncated; configured context is not a substitute for reading required files. Do not copy private workspace contents to Git.

Compatibility must be >=75/100 **and mandatory eligibility independently verified**. Unknown essential facts block that opportunity. Exclude the current employer; use verified official application channels and the original verified CV. No invented facts, generic unsolicited campaigns, duplicate applications, security/access-control bypasses, paid additions or employment commitments. Professional Communication v1.0 governs truthful individualized representation. Interviews, offers, sensitive declarations and personal commitments go to Main. Historical one-off permissions and capped grants remain evidence, not current admission rules.

## Evidence classification

`VERIFIED_REAL` means an actual external operation or real production execution/readback was observed. `VERIFIED_SIMULATION` means isolated fixtures with simulated transport. `CONFIGURED_NOT_YET_VERIFIED` means instructions/availability without the needed real outcome. `BLOCKED` identifies a confirmed channel/data/policy barrier. `FAILED` is reserved for an unsuccessful tested outcome; no successful overall E2E result is asserted.

| Capability | Evidence level | Actual evidence and boundary |
| --- | --- | --- |
| A. Autonomous discovery | VERIFIED_REAL | Scheduled November 16 and 17 searches inspected permitted public employer/ATS/indexed sources and saved outcomes; coverage is selective |
| B. Profile-based evaluation | VERIFIED_REAL | Real vacancies scored and rejected/held for mandatory data, closed listings or unsupported product requirements; score is not hiring probability |
| C. Discovery/application deduplication | VERIFIED_REAL | Existing sent/blocked records persisted across subsequent cycles without repeat applications; follow-up-send deduplication is CONFIGURED_NOT_YET_VERIFIED |
| D. All-qualified sequential queue, no numerical quota | VERIFIED_SIMULATION | Scheduler-run fixture: 25 entries, five pre-submit blocks, twenty simulated submissions; separate 80-entry fixture completed. Active quota fields/stop rules removed; no live multi-application cycle yet |
| E. Verified recruitment email channel | VERIFIED_REAL | Two prior owner-authorized individual sends with independent SENT readbacks. One later bounced; this is not proof of employer delivery |
| E. Completed employer browser submission | BLOCKED | A real ATS CV upload was initiated, then human verification failed; no confirmed submission or parsing/acceptance. Another form remains blocked by essential unknown candidate data |
| F. Original PDF attachment | VERIFIED_REAL | Actual Gmail readbacks showed the original PDF; source integrity verified. Local browser-control selection also tested, with synthetic-page scope; employer acceptance is not established |
| G. Individualized truthful communication | VERIFIED_REAL | Prior vacancy-specific application messages were recorded/reviewed. Current v1.0 instructions retained; future autonomous factual replies are not proven by those sends |
| H. Gmail SEND and thread registry | VERIFIED_REAL | Original SENT IDs, PDF metadata, thread tracking and later hourly readbacks exist privately |
| H. Positive employer delivery/receipt | CONFIGURED_NOT_YET_VERIFIED | One case has no positive delivery evidence; another has authenticated non-delivery. Silence and SENT never imply receipt |
| I. Outcome separation | VERIFIED_REAL | Production separates SENT, transport submission, known bounce, blocked form and unknown receipt. Positive DELIVERED/employer-response transitions remain CONFIGURED_NOT_YET_VERIFIED |
| J. Delivery-failure inbox handling | VERIFIED_REAL | A genuine authenticated DSN matched the original message/recipient; recorded as bounce/technical block, not employer rejection; no resend or repeated alert |
| J. Genuine recruiter reply and routine follow-up | CONFIGURED_NOT_YET_VERIFIED | Latest inspected cycle found no new recruiter response or due follow-up; no real autonomous reply/follow-up lifecycle demonstrated |
| K. Durable state writes and reconciliation | VERIFIED_REAL | Normal hourly production cycle reconciled all 14 existing cases into the queue and retained two tracked email threads in persistent workspace files |
| K. Interrupted queue recovery/failure isolation | VERIFIED_SIMULATION | Separate processes resumed disk checkpoints, preserved independent blocks, held unresolved uncertainty and reconciled simulated send-before-checkpoint crash without duplicate transport events. Real-service crash/reboot/concurrency behavior remains unverified |
| L. Existing Main/Career route | VERIFIED_REAL | Stored records include actual Main acknowledgement of blocked-case reports; queue acceptance alone is not receipt |
| L. Real interview/offer escalation and owner notification | CONFIGURED_NOT_YET_VERIFIED | Policy and route configured; no genuine interview/offer or device-delivery acceptance test observed |

## Actual scheduler and case evidence

Real scheduled Daily discovery completed at **09:00 ART on November 16 and 17**. The latest manual Daily validation at **12:27 ART on November 17** completed successfully in about 97 seconds, but used simulated transport. Earlier native browser/Gmail validation proved reads and local file selection; browser SHA-256 was unavailable on about:blank, so its original PARTIAL verdict is retained. Independent file-size/header/full-byte fingerprint comparison confirmed selection, without asserting employer acceptance.

The latest inspected normal hourly Inbox cycle began at **13:00:16 ART (16:00:16 UTC) on November 17**, completed successfully in about 91 seconds and finished quietly. Its private evidence records nine messages discovered, a delivery notification, two tracked threads, no new relevant response, no reply/follow-up/escalation sent, and 14 queue records reconciled. Both job histories show the intended Career model. These receipts prove execution, not an application outcome.

The 14-case queue snapshot contains seven BLOCKED_BEFORE_SUBMISSION, one SUBMITTED (email SENT only), five CLOSED and one BOUNCED. No runnable qualified item was present in that snapshot. The original named cases and detailed history were inspected privately; this public repository intentionally omits employer-to-candidate mappings, recipients, message IDs and candidate details. Their private outcomes are: email case A SENT/awaiting response with receipt unknown; email case B SENT then authenticated policy bounce; form case A not submitted due to missing essential data; form case B not submitted after human-verification failure. No blocked form is reported as an application success.

Source evidence stays on OVH: existing scheduler receipts/run summaries, recruitment role/evidence files and inbox-state, private configuration before/after audits, and isolated queue-validation artifacts under the existing OpenClaw tmp area. Raw evidence, email bodies, authentication metadata, candidate/CV hashes and recruitment records are excluded from Git. Some portal observations are explicitly owner-reported, not independently replayed.

## Queue, application and inbox execution

Daily resumes unfinished work fairly, discovers/evaluates permitted vacancies, persists every qualified item and processes sequentially until actual session/time/tool capacity prevents more work. There is no numerical application stop condition. Persist queue/source continuations for the next existing scheduled execution; do not add continuation jobs.

Use per-opportunity reservations and stable cross-source/channel deduplication keys in the existing pipeline/ledger. Short shared-state transactions re-read fresh state, merge affected records and atomically replace/fsync JSON; do not hold the shared lock during network calls. Persist SUBMISSION_PENDING before irreversible send/submit; save independent outcome evidence before moving on. The inbox registry can be reconstructed from authoritative pipeline evidence if a crash separates the two writes.

A known pre-submit block affects only that opportunity/channel. An uncertain final action stays held for reconciliation across date changes and restarts; no blind retry, alternate-channel reapplication or timeout-based release. A sparse negative Gmail search alone is insufficient proof of non-submission. SENT/submitted/bounced entries remain deduplicated. An ordinary failure must not stop independent qualified items; genuine shared persistence/tool/rate-limit failures may defer their affected scope.

Inbox searches messages and separate DSNs, checks tracked threads, correlates original IDs/headers/recipients privately, and separates delivery and employer response. SUBMITTED/SENT is not DELIVERED, review or acceptance; BOUNCED is not rejection. Routine replies stay inside authorized factual conversations. Follow-up needs an evidenced due date and applicable policy, not an invented campaign cadence. No interview, offer or binding-condition commitment is automatic.

These are agent instructions and durable state conventions, not a separately enforced exactly-once transaction engine. Simulated checkpoint success must not be presented as a guarantee for real Gmail/ATS side effects.

## Final portal decision: BLOCKED / DEFERRED

| Portal | Final finding | Decision |
| --- | --- | --- |
| Computrabajo Argentina | Owner reported HTTP 403 from OVH managed Chromium; platform restriction also recorded | BLOCKED / DEFERRED |
| ZonaJobs Argentina | Owner reported security blocking before Google authentication; restriction recorded | BLOCKED / DEFERRED |
| Bumeran Argentina | Documented platform-policy restriction; no equivalent technical block was observed | BLOCKED / DEFERRED |

Existing personal portal accounts use Google Sign-In. No Google authentication was completed in the OVH browser. Persistent browser sessions are technically available but do not override website rules. Windows integration requires a running Windows environment and does not satisfy independent 24/7 OVH operation. No bypass, proxies, custom middleware or further portal implementation is authorized. General permitted discovery, direct employer/ATS channels and Gmail workflows remain enabled.

## Minimal troubleshooting and next phase

1. Inspect `openclaw health --json`, browser status, `openclaw cron list --json` and targeted `cron runs`; a job's ok status is not submission evidence. Do not run Daily as a diagnostic while standing authorization is active.
2. Check full current instructions/control, actual remaining queue and per-opportunity evidence. Do not restore historical capped grants or obsolete OAuth-pending instructions. Never rerun inactive local Google prototype scripts.
3. If blocked, record exact data/channel/rate-limit evidence and continue independent work. If uncertain, reconcile the original action; never clear a reservation just to make progress.
4. Before stale-lock recovery prove the owning native run has finished; preserve current state/backups. Never replace the whole live volume or roll back newer application history. Gmail requires protected Gateway execution; do not expose keyring or token values.
5. Observe the next normal Daily execution, then obtain genuine positive receipt/recruiter-response evidence through an eligible permitted opportunity. Validate browser employer confirmation only where legitimately available. Full real recovery/device notification/long-term unattended acceptance remain open; any later sending test requires its appropriate authorized scope.

No critical recruitment regression was confirmed in this audit. The confirmed documentation regression was stale design/OAuth-pending status; it is corrected here. The connected GitHub account cannot write this repository and `gh` is absent in the Gateway; documentation publication uses the already configured managed identity through protected execution, without installing software or changing OAuth. The implementation phase can close with PARTIAL operational acceptance and this explicit real-world validation backlog.
