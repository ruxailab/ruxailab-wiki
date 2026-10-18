# GSoC 2026 — Unified Logging and Traceability System for Usability Studies

✅ Merged · 🔍 Open, in review · ⏳ Not started

## Contributor

- **Name:** Justin Timothy
- **GitHub:** [@tim48-robot](https://github.com/tim48-robot)
- **Email:** [justintimothy303@gmail.com](mailto:justintimothy303@gmail.com)
- **LinkedIn:** [Justin Timothy](https://www.linkedin.com/in/justin-timothy-w-b6b28817b/)

## Project

**Unified Logging and Traceability System for Usability Studies** (medium, 175 hours; mentors: Marc G.C and Karine Pistili; organization: Uramaki LAB). The project adds study activity logging to RUXAILAB: participant activity is recorded through a trusted server boundary, without storing answers or personal data, and researchers can read it in a Log Explorer.

- **Project proposal:** [Unified Logging and Traceability System for Usability Studies — GSoC 2026](https://summerofcode.withgoogle.com/programs/2026/projects/mTtZZ2Lq)
- **Project source:** [RUXAILAB](https://github.com/ruxailab/RUXAILAB)

## Deliverables completed

| Milestone | Status | PRs |
| --- | --- | --- |
| M1 — Backend logging ingestion | ✅ Merged | [#2111](https://github.com/ruxailab/RUXAILAB/pull/2111), [#2295](https://github.com/ruxailab/RUXAILAB/pull/2295) |
| M2 — Log Explorer (unmoderated, moderated, heuristic) | ✅ Merged | [#2338](https://github.com/ruxailab/RUXAILAB/pull/2338), [#2379](https://github.com/ruxailab/RUXAILAB/pull/2379), [#2402](https://github.com/ruxailab/RUXAILAB/pull/2402), [#2405](https://github.com/ruxailab/RUXAILAB/pull/2405) |
| M2 — Card sorting and focus group logging | 🔍 Open, in review | [#2450](https://github.com/ruxailab/RUXAILAB/pull/2450) |
| M3 part 1 — Overview dashboard | 🔍 Open, in review | [#2451](https://github.com/ruxailab/RUXAILAB/pull/2451) |
| M3 part 2 — Server-side export | 🔍 Open, in review | [#2451](https://github.com/ruxailab/RUXAILAB/pull/2451) |
| M4 — Tests and contributor guide | ✅ Merged (guide rewrite 🔍 in [#2450](https://github.com/ruxailab/RUXAILAB/pull/2450)) | Tests in each PR above; [logging extension guide](https://github.com/ruxailab/RUXAILAB/blob/develop/docs/logging-extension-guide.md) |

### M1 — Backend logging ingestion ✅

Two callable Cloud Functions in `functions/src/https/logEvents.js`:

- `logEvents` receives batches of up to 25 events observed in the participant's browser (study opened, task started, answer edited, recording outcome, and similar).
- `requestLogEvent` records the lifecycle events that matter for analysis: consent accepted, task finished, and study submitted. The server checks each one against the participant's saved answer instead of trusting the browser.

What the server enforces:

- **Authorization:** only a user allowed to answer the study can log to it. For studies with a consent step, nothing is stored before consent is saved. Direct browser writes to the logging collections are denied by Firestore rules, and reading logs needs the separate `logs.view` capability.
- **Sanitization:** every event type has a fixed list of allowed detail fields. Unknown event types and extra fields are rejected. Answer text, card names, names, emails and user IDs are never stored; details are counts and controlled references such as `task:2`.
- **Pseudonymous identity:** the session ID is a SHA-256 hash of a server secret, the study ID and the user ID. Researchers see a stable label (`P-001`, `P-002`, …) assigned by the server.
- **Idempotency:** events and batches have stable IDs, so a retry never creates a duplicate. Each session has a budget of 1,000 browser-observed events.
- **Server-derived fields:** message, level, source, actor role, participant label and receipt time are set by the server, not sent by the client.

In the browser, events wait in an IndexedDB queue and are retried until delivered. Logging is fail-open: a logging failure never blocks answering, saving or submitting, and it shows the participant nothing.

### M2 — Log Explorer ✅

The Logs page (`src/shared/views/LogsView.vue`) is available for unmoderated user tests, moderated user tests and heuristic evaluations.

- **All events:** a paged table, 20 events per page by default, with page-size options and an exact event count. Filters: participant label (with autocomplete), event type, level, source and date range. Selecting a row opens a details drawer; delivery metadata is collapsed by default ([#2338](https://github.com/ruxailab/RUXAILAB/pull/2338)).
- **Readable activity:** rows show task numbers, task type, questionnaire activity, task outcomes and recording results (saved, failed, denied). `TASK_STARTED` is logged when a task actually opens. Response values are still never logged ([#2379](https://github.com/ruxailab/RUXAILAB/pull/2379)).
- **Moderated user tests:** moderated sessions had bugs that made them unusable ([#2401](https://github.com/ruxailab/RUXAILAB/issues/2401)). After fixing them, moderated studies log the same events as unmoderated ones ([#2402](https://github.com/ruxailab/RUXAILAB/pull/2402)).
- **Heuristic evaluations:** one `QUESTION_RESPONSE_UPDATED` event per question interaction, with counts only. Selected values and comment text are not logged.
- **Participant timeline:** a second view that groups one participant's events by study step (consent, pre-test, each task, post-test, submission), with timing and a summary per step ([#2405](https://github.com/ruxailab/RUXAILAB/pull/2405)).

**How this differs from the proposal:** there is no free-text search. Filters run as Firestore queries over the study's complete history, before pagination, so the browser never downloads all logs to search them. The participant timeline was not in the proposal; it was added because the flat event list was hard to read ([#2403](https://github.com/ruxailab/RUXAILAB/issues/2403)).

### M2 — Card sorting and focus group logging 🔍

In review in [#2450](https://github.com/ruxailab/RUXAILAB/pull/2450):

- **Shared change:** the per-study-type logging rules in `logEvents.js` (which answer field to verify against, whether there is a consent step, which roles may log) are kept in one table, instead of separate checks spread over several functions. Unknown study types are still denied.
- **Card sorting:** logs study opened, consent accepted and study submitted. Consent and submission are verified against the saved `cardSortingAnswers`. Card and category names are free text, so they are never logged. Adds the card sorting Logs route; before this, the sidebar's Logs link for card sorting had no page behind it.
- **Focus group:** the facilitator's client logs `SESSION_STARTED` and `SESSION_ENDED`. The server checks them against the live room and the scheduled session's status. Each event is stored once per session, and only the facilitator can send them. Adds the focus group Logs route.

### M3 — Overview and export 🔍

In review in [#2451](https://github.com/ruxailab/RUXAILAB/pull/2451):

- **Overview tab:** sessions, submitted, recorded events, warnings and errors, plus the 5 latest events. Each card opens All events with the matching filter applied.
- **Export:** an `exportStudyLogs` callable produces CSV or JSON, page by page with a cursor. It checks `logs.view` on every page and runs the Explorer's filters on the server. The export covers a fixed point in time: events received after it starts are left out. Rows are rebuilt from an allowlist, so session, event and batch IDs, document IDs and UIDs are never included, while participants appear by their stable label (`P-001`). CSV cells are escaped against formula injection.

**How this differs from the proposal:**

- The overview counts with live `count()` queries instead of a pre-aggregated `_stats` document updated on every write.
- The export streams pages to the browser instead of writing a file to Firebase Storage with a 15-minute signed URL and deletion after 24 hours.
- The export has no row limit.

### M4 — Tests and contributor guide ✅

Tests were written with each PR instead of as a separate suite at the end:

- Functions tests on the Firestore emulator for ingestion (80 tests in `functions/tests/logEvents.spec.js` as of [#2402](https://github.com/ruxailab/RUXAILAB/pull/2402)). They cover allowed and denied users, the consent gate, verified events, rejected fields and duplicate batches.
- Frontend unit tests for the logging client, the runtime, the Logs view and the participant timeline.
- Membership security tests (14 cases) and rules tests for anonymous participants ([#2404](https://github.com/ruxailab/RUXAILAB/pull/2404)).

The [logging extension guide](https://github.com/ruxailab/RUXAILAB/blob/develop/docs/logging-extension-guide.md) explains how to add a study method or an event type. The guide is rewritten for the per-type table in [#2450](https://github.com/ruxailab/RUXAILAB/pull/2450) (in review).

## Deliverables not completed, and why

**Changes to the plan.** I dropped the Trace View (trace lifecycle), because I judged it would add little for researchers. I used that time to make logging work across study methods. I did the most-used methods first: unmoderated user tests, then moderated user tests (whose sessions first had to be fixed), then heuristic evaluations. This methodology work delayed the overview and export.

- **Overview dashboard and export (M3)** 🔍 — delayed by the methodology work above; in review in [#2451](https://github.com/ruxailab/RUXAILAB/pull/2451).
- **Card sorting logging** 🔍 — the card sorting module was less developed than the others, so I left its logging for later. In review in [#2450](https://github.com/ruxailab/RUXAILAB/pull/2450).
- **Focus group logging** 🔍 — another GSoC contributor built the Focus Group module this summer, so its logging had to wait for the module to exist. A focus group session has one facilitator and many attendees, so this first version logs only the session start and end, sent by the facilitator. In review in [#2450](https://github.com/ruxailab/RUXAILAB/pull/2450).
- **Accessibility logging** ⏳ — accessibility studies have no Logs page yet, and the ingestion function does not accept them.

## Stretch goal (not committed)

**M5 — AI emotion logging from audio/video recordings** ⏳ Not started. This was a stretch goal in the proposal and was never committed. The time went to the methodology work above.

## Pull requests

All PRs I opened during GSoC 2026, grouped by topic.

### Logging pipeline

- [#2111 — Milestone 1: backend logging pipeline](https://github.com/ruxailab/RUXAILAB/pull/2111) — ✅ Merged
- [#2295 — Trusted study-log ingestion](https://github.com/ruxailab/RUXAILAB/pull/2295) — ✅ Merged

### Log Explorer and researcher view

- [#2338 — Log Explorer](https://github.com/ruxailab/RUXAILAB/pull/2338) — ✅ Merged
- [#2379 — Improve unmoderated study activity logs](https://github.com/ruxailab/RUXAILAB/pull/2379) — ✅ Merged
- [#2405 — Participant timeline view](https://github.com/ruxailab/RUXAILAB/pull/2405) — ✅ Merged
- [#2451 — Study log overview and server-side export](https://github.com/ruxailab/RUXAILAB/pull/2451) — 🔍 Open, in review

### Making study methods work and log

- [#2402 — Fix moderated studies and enable their logging](https://github.com/ruxailab/RUXAILAB/pull/2402) — ✅ Merged
- [#2329 — Add moderated session group indexes](https://github.com/ruxailab/RUXAILAB/pull/2329) — ✅ Merged
- [#2404 — Fix invite membership and support anonymous participants](https://github.com/ruxailab/RUXAILAB/pull/2404) — ✅ Merged. Joining a study now requires a valid invitation, and participants on a no-login link get an anonymous account, so their answers and logs are saved.
- [#2450 — Card sorting and focus group logging](https://github.com/ruxailab/RUXAILAB/pull/2450) — 🔍 Open, in review

### Other fixes during GSoC

- [#2169 — Study access control and security fixes](https://github.com/ruxailab/RUXAILAB/pull/2169) — ✅ Merged
- [#2124 — Fix sorting in Community Studies](https://github.com/ruxailab/RUXAILAB/pull/2124) — ✅ Merged

## Additional materials

- [Logging extension guide](https://github.com/ruxailab/RUXAILAB/blob/develop/docs/logging-extension-guide.md)
- [Figma: PoC Unified Logging](https://www.figma.com/design/fbnBw4aNg6EcBf88Sp0TGp/PoC-Unified-Logging?node-id=0-1&p=f&t=PKIEFl41DPHFPKfw-0)
- [GitHub project (Kanban)](https://github.com/users/tim48-robot/projects/1)
- [Milestones](https://github.com/tim48-robot/RUXAILAB/milestones)
- Demo videos:
  - [Log Explorer preview (#2338)](https://youtu.be/mHG_UilcHTc)
  - [Moderated studies after the fix (#2402)](https://youtu.be/YCAf7uTm1Yg)
  - [Invite rules and anonymous participants (#2404)](https://youtu.be/U6N_bdFRRG4)
  - [Access control and security walkthrough (#2169)](https://youtu.be/qPeiw2-dgfk)

## Future work

1. Make RUXAILAB easier for researchers to use, starting with a clearer UI for setting up studies and reading their results.
2. Study whether M5 (emotion analysis of recordings) is feasible: what the recordings and consent allow, and how results would be labelled as AI-derived in the logs.
3. Finish the review of #2451 and #2450, then extend logging to focus group attendees (after agreeing the attendee model with the maintainers) and to accessibility studies.

## Conclusion

The project delivered trusted, pseudonymous activity logging for unmoderated user tests, moderated user tests and heuristic evaluations. Researchers can filter every event in a study, or follow one participant step by step, without seeing answers or identities. I changed the plan during the summer: I dropped the Trace View and spent the time on more study methods, including fixing moderated sessions so they could be logged at all. As a result, the overview, export, card sorting and focus group logging are still in review rather than merged, and the AI stretch goal was not started.
