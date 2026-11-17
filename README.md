# AURORA — OpenClaw operations

Current operational audit: **2026-11-17 — PARTIAL**. Aurora Career is deployed on the existing OVH OpenClaw Gateway. Discovery, Gmail sending with the original PDF, delivery-failure handling and scheduled inbox reads have real evidence. Unlimited qualified queue processing and interrupted-execution recovery have simulated-transport evidence. Successful employer delivery, a genuine recruiter-response cycle and completed browser submission remain unverified.

- [Current handoff — read first](docs/CURRENT_HANDOFF.md)
- [Career status, evidence matrix, portal decision and recovery](docs/AURORA_CAREER_SPEC.md)
- [Changelog](CHANGELOG.md)
- [Automation design master](docs/AURORA_AUTOMATIONS_MASTER.md) — other proposed modules are not accepted by this Career audit.
- [Career functional design](docs/fdd/FDD-08_AURORA_CAREER.md) — historical design; current operating rules are in the audit/handoff and private live workspace.
- [Work design](docs/AURORA_WORK_SPEC.md) — separate scope, not validated by this audit.

Career uses `openai/gpt-6.1-sol` with medium reasoning. Its two existing isolated automations remain enabled: Daily Job Discovery at 09:00 and Recruitment Inbox Manager hourly, timezone `America/Argentina/Buenos_Aires`. Standing authorization is approved for all genuinely qualified opportunities, with no owner-imposed numerical application quota. Mandatory eligibility, score >=75/100, verified channels, original CV, deduplication and no-commitment rules remain binding.

This repository contains sanitized documentation, not the live deployment or recruitment database. Never commit CVs, candidate/contact details, application records, raw mail/logs, cookies, OAuth material, `.env`, `.private/` or runtime SQLite files. The deployment directory is not an initialized Git checkout and must not be imported wholesale. Legacy local Google prototype scripts/reports are inactive historical artifacts; do not run them or repeat OAuth based on stale documentation.

The final audit is non-sending and makes no Gateway, OAuth, browser-security or schedule changes. No new agents, services, databases, middleware or recurring jobs were introduced.
