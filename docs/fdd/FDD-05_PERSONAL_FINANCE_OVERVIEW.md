# FDD-05 — Personal finance overview

> **Status:** FUNCTIONAL DESIGN — NOT IMPLEMENTED / NOT ACCEPTED  
> **Target:** Existing OpenClaw on OVH, Docker/headless, accessible from Windows and Android  
> **Timezone:** `America/Argentina/Buenos_Aires`  
> **Privacy:** Public-safe specification. Do not commit personal/corporate content or credentials.

**Cross-cutting contract.** Reuse the existing running OpenClaw, its supported agents/tools, native cron/heartbeat and persistent storage. Do not redesign VPS/network/authentication, change the main model, or incur API costs without explicit approval. Separate Work (corporate) from Career (personal recruiting). Scheduled tasks must not silently duplicate existing automations. No function is DONE based solely on a created cron job; prove live permitted data, persistence after restart, delivery, failure visibility and recovery. Android notifications must be checked, not assumed.

## 1. Objective
Provide a monthly financial snapshot that can answer: What were income and expenses, what remains available, what savings were achieved and what obligations are upcoming? Avoid burdensome per-purchase manual entries.

## 2. Input policy
Only user-authorized statements, exports and aggregate manual updates from personal accounts. No assumed bank connectivity, direct transfers or payment execution. Internal transfer between user's accounts must not be counted as expense or income. Cash withdrawals may be categorized as movement to cash balance rather than immediate expense unless user confirms otherwise.

## 3. Functional requirements
- **FR01 Import:** ingest CSV/statement or brief aggregate updates; source timestamp, currency, account and completeness flag.
- **FR02 Normalize:** date, amount, sign, merchant/category, source ID, account and original currency; handle ARS and USD/USDT without treating conversions as gains.
- **FR03 Deduplicate:** match transactions and inter-account transfers; prompt on uncertain cases instead of double counting.
- **FR04 Categorize:** rent/housing, utilities, food, transport, subscriptions, health, other, savings; do not over-categorize tiny expenses.
- **FR05 Reconcile:** opening balance + real flows = closing balance, distinguish cash, bank and investments with data coverage indicators.
- **FR06 Report:** monthly income, fixed/variable expense, estimated net surplus, planned obligations, savings rate, missing data and month-to-month comparison.
- **FR07 Alert:** unusual increases and upcoming confirmed obligations; avoid inaccurate 'you can spend' claims based on incomplete accounts.

## 4. Data and privacy
Private financial data stays in protected persistent storage, never public Git. No credentials, card details or full statements in notifications. Explicitly label missing utilities, accounts and unverified prices; FX conversion must have date/source or remain an unconverted currency amount.

## 5. Acceptance
Sample statements with transfers, cash withdrawal and installment; reconcile with user-provided totals and no double count. Show incomplete-month caveat, survive restart, restore from backup. **No financial transactions initiated**.

## 6. Dependencies and open decisions
Actual personal data sources and permitted retention, account taxonomy, monthly cutoff, currency conversion policy and whether an existing scheduled finance review is already in use. Related: FDD-09 and FDD-10.
