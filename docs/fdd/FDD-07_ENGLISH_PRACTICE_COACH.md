# FDD-07 — English practice coach

> **Status:** FUNCTIONAL DESIGN — NOT IMPLEMENTED / NOT ACCEPTED  
> **Target:** Existing OpenClaw on OVH, Docker/headless, accessible from Windows and Android  
> **Timezone:** `America/Argentina/Buenos_Aires`  
> **Privacy:** Public-safe specification. Do not commit personal/corporate content or credentials.

**Cross-cutting contract.** Reuse the existing running OpenClaw, its supported agents/tools, native cron/heartbeat and persistent storage. Do not redesign VPS/network/authentication, change the main model, or incur API costs without explicit approval. Separate Work (corporate) from Career (personal recruiting). Scheduled tasks must not silently duplicate existing automations. No function is DONE based solely on a created cron job; prove live permitted data, persistence after restart, delivery, failure visibility and recovery. Android notifications must be checked, not assumed.

## 1. Objective
Deliver sustainable, short English practice anchored in actual ERP/CRM professional conversations and interviews, while tracking progress and common errors. The system should prompt practice but not over-notify or require a 24/7 voice channel.

## 2. Inputs
User's confirmed language goals, practice history, preferred topics, available time and verified voice capability on the chosen Android/Windows client. Personal data only; corporate communications are not imported.

## 3. Requirements
- **FR01 Nudge:** proposed weekday 20:00 local invitation to a 10-minute session; respect snooze/skip and quiet hours.
- **FR02 Session:** short real-world scenario, incremental difficulty, conversational turns, feedback on vocabulary/grammar/clarity.
- **FR03 Professional context:** practice incident explanation, project handover, client follow-up and interview self-introduction without fabricating professional credentials.
- **FR04 Memory:** record session completed/skipped, recurring errors, vocabulary targets and recommended next activity.
- **FR05 Adaptive:** use previous difficulties to set next session; one core skill per session; optional weekly recap.
- **FR06 Voice:** if native client real-time audio is actually available, allow it; otherwise deliver chat/audio-compatible content without claiming live talk support.

## 4. Output and storage
Short notification, interactive 10-minute exercise, 3–5 targeted corrections, one next-step suggestion. Store minimal skills metrics and corrections, not raw long recordings by default.

## 5. Security and failures
No always-on microphone assumption; no unverified 'wake word' promise. Avoid automatic transcription/storage without consent. If Android notifications fail, present task in accessible client and mark delivery failure honestly.

## 6. Acceptance
Three completed sessions with continuity: repeated errors influence later exercise; correct local reminders and skip behavior; progress survives restart. Voice-specific acceptance is separate from text mode.

## 7. Open decisions
Current English benchmark, live voice availability/cost, desired days and duration, feedback style and optional weekly review. Related: FDD-09 and FDD-10.
