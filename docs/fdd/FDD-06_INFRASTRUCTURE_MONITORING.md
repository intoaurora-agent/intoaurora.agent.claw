# FDD-06 — Infrastructure monitoring and alerting

> **Status:** FUNCTIONAL DESIGN — NOT IMPLEMENTED / NOT ACCEPTED  
> **Target:** Existing OpenClaw on OVH, Docker/headless, accessible from Windows and Android  
> **Timezone:** `America/Argentina/Buenos_Aires`  
> **Privacy:** Public-safe specification. Do not commit personal/corporate content or credentials.

**Cross-cutting contract.** Reuse the existing running OpenClaw, its supported agents/tools, native cron/heartbeat and persistent storage. Do not redesign VPS/network/authentication, change the main model, or incur API costs without explicit approval. Separate Work (corporate) from Career (personal recruiting). Scheduled tasks must not silently duplicate existing automations. No function is DONE based solely on a created cron job; prove live permitted data, persistence after restart, delivery, failure visibility and recovery. Android notifications must be checked, not assumed.

## 1. Objective
Detect meaningful outages of **authorized** Aurora-related services while OpenClaw runs 24/7 on OVH, without consuming LLM tokens for basic checks or risking SSH access. Monitoring must distinguish 'checker itself failed' from 'target is down'.

## 2. Monitored services
Only endpoints explicitly approved by owner: OpenClaw Gateway readiness, reverse proxy/HTTPS, allowed OVH/Contabo app health endpoints, GitHub repository API availability and optional backup freshness. Avoid scanning arbitrary hosts or exposing sensitive ports.

## 3. Requirements
- **FR01 Deterministic checks:** schedule proposed every 5 minutes using non-LLM HTTP/TLS/container health where authorized; record latency and status, not credentials.
- **FR02 Detect:** require consecutive failures before alarming to reduce transients; label `UNKNOWN` when network/checker is broken.
- **FR03 Alert:** new incident notice with endpoint alias, failed checks, start time and next retry; notify recovery once; suppress duplicate notifications.
- **FR04 Escalate:** repeated critical outage or expired backup gets higher priority and actionable diagnostics, but no automatic remediation.
- **FR05 Retain:** rolling minimal history and daily uptime summary (only if measuring continuously), last success, last error, retry count.
- **FR06 Cost:** never call AI on healthy repetitive checks; invoke model only for user-requested troubleshooting or concise incident synthesis.

## 4. Safety rules
Read-only status tools. No root shell, SSH mutation, firewall changes, docker restarts, deployment, config edits or credentials in Git. Monitoring its own host from that same host cannot guarantee notification when VPS is offline; external independent watchdog/alert transport is a later option requiring explicit approval.

## 5. Failures and acceptance
Test false-positive suppression, a controlled unreachable test endpoint, recovery notice and logger restart. No disruptive tests on production services. Prove alerts from Android or agreed channel. Alerts cannot depend solely on a Gateway that is itself unavailable unless an out-of-band channel exists.

## 6. Dependencies and open decisions
Target list and owner consent, stable low-privilege status endpoints, transport (mobile/email), quiet-hours override for critical cases, failure threshold and whether offsite watcher is needed. Related: FDD-09 and FDD-10.
