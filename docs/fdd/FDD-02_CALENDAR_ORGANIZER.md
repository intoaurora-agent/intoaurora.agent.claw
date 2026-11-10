# FDD-02 — Personal calendar organizer

> **Status:** FUNCTIONAL DESIGN — NOT IMPLEMENTED / NOT ACCEPTED  
> **Target:** Existing OpenClaw on OVH, Docker/headless, accessible from Windows and Android  
> **Timezone:** `America/Argentina/Buenos_Aires`  
> **Privacy:** Public-safe specification. Do not commit personal/corporate content or credentials.

**Cross-cutting contract.** Reuse the existing running OpenClaw, its supported agents/tools, native cron/heartbeat and persistent storage. Do not redesign VPS/network/authentication, change the main model, or incur API costs without explicit approval. Separate Work (corporate) from Career (personal recruiting). Scheduled tasks must not silently duplicate existing automations. No function is DONE based solely on a created cron job; prove live permitted data, persistence after restart, delivery, failure visibility and recovery. Android notifications must be checked, not assumed.

## 1. Objective and scope
Provide a reliable daily view of personal commitments, preparation time and reminders so the user does not manually assemble the agenda. Do not modify, accept, cancel or send invitations during the initial implementation. Corporate working-calendar analysis for Work is specified in FDD-03 and requires its own authorization.

## 2. Sources and permissions
- Authorized personal Google Calendar (or other explicitly configured personal calendar) in **read-only** mode.
- Event metadata, attendee context where permitted, busy/free windows and time zone.
- Existing OpenClaw cron, persistent event IDs and briefing delivery.

## 3. Functional requirements
- **FR01 Sync:** collect next 48 hours incrementally, accounting for recurrent events, reschedules, cancellations and DST/time zone conversion.
- **FR02 Daily plan:** at proposed 08:00 local, present today/tomorrow, conflicts, travel/preparation buffers if explicitly supplied, and unscheduled task windows.
- **FR03 Reminder:** notify before explicitly marked important events; avoid duplicating native Calendar alerts by default.
- **FR04 Prepare:** link relevant approved personal notes and prior action items for a meeting; distinguish confirmed facts from suggestions.
- **FR05 Conflict detection:** highlight overlaps, tight turnarounds and overcommitment, but do not move events.
- **FR06 Updates:** changes and cancellations invalidate stale reminders without creating duplicates.

## 4. Output and data
Morning agenda: start time, event, location/link when permitted, actionable preparation, conflicts and available blocks. Minimal event index: provider calendar ID, event ID, start/end, state, last sync timestamp. Do not retain full private event descriptions unnecessarily.

## 5. Failure and security
If Calendar is inaccessible, explicitly report **CALENDAR_UNAVAILABLE**; never show stale events as current. Handle shared calendars carefully, avoiding leakage in notifications. No calendar-write OAuth scope in phase 1.

## 6. Acceptance
Five consecutive real days of accurate event lists, tested cancellation/reschedule, at least one conflict scenario, and no event mutations. Works without Windows running; persists after restart. Verify delivery to user's approved endpoint.

## 7. Open decisions
Which calendars, quiet hours, reminder lead times, travel estimates (not inferred), user workday boundaries and notification policy. Related: FDD-09 and FDD-10.
