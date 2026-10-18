# Study activity logging - developer guide

This guide explains how to add logs to RUXAILAB: more events for a study type that already logs, or logging for a new study type. The full reference (every event, its allowed fields and how it is verified) is in the repository: [`docs/logging-extension-guide.md`](https://github.com/ruxailab/RUXAILAB/blob/develop/docs/logging-extension-guide.md).

> This page describes the code after [#2450](https://github.com/ruxailab/RUXAILAB/pull/2450) (per-type logging table, card sorting and focus group) and [#2451](https://github.com/ruxailab/RUXAILAB/pull/2451) (overview and export). Until they merge, the per-type rules are separate checks in `functions/src/https/logEvents.js` (`canAnswerStudy`, `consentAccepted`, `participantAnswerFor`), and the export step below does not apply yet.

## How logging works

Logs record what happened during a study (opened, consented, task finished, submitted), never what anyone wrote or chose. Answers stay in Results.

```text
participant view (e.g. UserTestView.vue)
  └─ createStudyLoggingRuntime            src/shared/services/studyLoggingRuntime.js
       ├─ observations → IndexedDB queue  src/shared/services/studyLoggingClient.js
       │    └─ logEvents (callable)        batches of up to 25, retried until delivered
       └─ lifecycle events
            └─ requestLogEvent (callable)  verified against the saved answer
                                           functions/src/https/logEvents.js
Firestore tests/{studyId}/
  ├─ logs           one document per event
  ├─ studySessions  one per participant, with the P-001 label
  ├─ logBatches     idempotency markers
  └─ loggingMeta    the label counter
researcher
  └─ Logs view (needs logs.view)          src/shared/views/LogsView.vue
       ├─ All events, Participant timeline, Overview
       └─ Export (exportStudyLogs callable)
```

Browsers cannot write to the logging collections; `firestore.rules` denies it. Everything goes through the two callables, and the server sets the message, level, layer, source, actor role, session ID (a salted hash, `LOG_ACTOR_HASH_SALT`), participant label and receipt time.

There are two kinds of events:

| Kind | Callable | Example | Trust |
| --- | --- | --- | --- |
| Observation | `logEvents` | `TASK_STARTED`, `ANSWER_EDITED` | What the browser saw. The server checks every field against the study, but it can't prove the event happened. |
| Verified lifecycle event | `requestLogEvent` | `CONSENT_ACCEPTED`, `STUDY_SUBMITTED` | The server writes it only if the participant's saved answer shows it happened. One fixed event ID per session, so a retry is a `duplicate`, not a second log. |

Use a verified event when researchers will rely on the fact (did they submit?). Use an observation for behavior that has no saved evidence (how many edits, which task was opened).

## Rules every log must follow

1. **No free text, answers or identity.** Details hold counts, controlled values (`completed`, `screen`) and references (`task:2`). Never log answer values, comments, card or category names, names, emails or user IDs.
2. **Allowlist, don't filter.** Each event type lists its exact detail keys on the client and the server. Unknown event types and extra keys are rejected.
3. **Check references on the server.** If an event says `task:7`, the server confirms task 7 exists in that study.
4. **Fail open.** Log after the primary save succeeds, never before. A logging failure must not block, delay or change the study, and must not show the participant anything.
5. **Respect consent.** For study types with a consent step, nothing is queued before consent is saved.

## Add more logs to an existing study type

Example: logging when a heuristic participant opens the help panel.

1. **Write down the research question.** Who reads this log, and what will it tell them? If it can only be answered with participant text, it can't be logged.
2. **Pick the kind.** Observation (`logEvents`) or verified (`requestLogEvent`), as described above.
3. **Server policy** (`functions/src/https/logEvents.js`):
   - observation: add an entry to `CLIENT_EVENT_POLICIES` with its exact `detailKeys` and validation of every value and reference against the study;
   - verified: add a case to `verifiedEventFor` that reads the saved answer and returns a deterministic event ID.
4. **Client sanitizer** (`src/shared/services/studyLoggingClient.js`): mirror the same detail keys in `sanitizeDetails`, so nothing else is stored in IndexedDB.
5. **Producer:** add a runtime method in `studyLoggingRuntime.js` if none fits, and call it from the participant view after the related save succeeds.
6. **Logs view** (`src/shared/views/LogsView.vue`): add the event type to `EVENT_TYPES_BY_STUDY` for the filter, and give its row a readable description.
7. **Participant timeline:** place the event in a study step in `stepKeyFor` (`src/shared/utils/participantTimeline.js`). Events with no step end up in "Other activity".
8. **Export:** add the event's detail keys to `EXPORTED_DETAILS` in `functions/src/features/logExport/models/LogExportRow.js`. Without that, the event still exports, but with empty details.
9. **Tests** (see below), then update [`docs/logging-extension-guide.md`](https://github.com/ruxailab/RUXAILAB/blob/develop/docs/logging-extension-guide.md) with the new event.

Changing `logEvents.js` means redeploying `logEvents` and `requestLogEvent`. Changing the export means redeploying `exportStudyLogs`.

## Add logging to a new study type

1. **Add a row to `STUDY_LOGGING`** in `functions/src/https/logEvents.js`:

   | Field | Meaning |
   | --- | --- |
   | answer field | where the participant's saved answer lives, e.g. `cardSortingAnswers`; `requestLogEvent` verifies against it |
   | consent gate | whether logging waits for `consentCompleted` in that answer |
   | roles | which study roles may log, besides owners, admins, managers and public studies |

   A study type without a row cannot log, so nothing is accepted by accident.
2. **Start with the minimum events:** `STUDY_VIEW_OPENED`, `CONSENT_ACCEPTED` (if gated) and `STUDY_SUBMITTED`. Card sorting in #2450 is a small example to copy: `src/ux/CardSorting/components/CardSortingTest.vue`.
3. **Producer:** in the participant view, create one runtime with `createStudyLoggingRuntime` (user ID, study ID, study type, `consentRequired`), then call:
   - `open()` on entry (types without consent);
   - `consentAccepted(occurredAt)` after the consent save, and `resumeAfterConsent()` on entry when consent was already saved;
   - `submitted()` after the final save;
   - `destroy()` on unmount.
4. **Route:** add `/<type>/logs/:id` with the shared `LogsView`, guarded by the `LOGS_VIEW` capability. Copy `src/ux/Heuristic/router.js`. Check that the sidebar's Logs item (`src/shared/utils/studyNavigation.js`) opens it.
5. **Logs view:** add the type's events to `EVENT_TYPES_BY_STUDY` and its name to `studyTypeLabel` in `LogsView.vue`.
6. Then add the type's own events, following the steps in the previous section.

### Study types that don't fit the participant model

The runtime assumes one participant moving through steps. A focus group has one facilitator and many attendees at the same time, so #2450 logs it differently: there is no runtime and no `STUDY_LOGGING` row. Instead, a `SESSION_EVENTS` policy lets only the facilitator or a study admin send `SESSION_STARTED` and `SESSION_ENDED`. These are verified against the live room and the scheduled session's status. Each scheduled session gets one log session, labelled `F-004` (facilitator of the fourth session) from the same counter as `P-` labels. If you add another role, follow the same pattern: a prefix for the role, and a number from the shared counter.

Logging focus group attendees is not designed yet. Agree the actor model with the maintainers before building it.

## Tests and local checks

Functions tests run on the emulators:

```bash
cd functions
FIRESTORE_EMULATOR_HOST=127.0.0.1:8081 FIREBASE_DATABASE_EMULATOR_HOST=127.0.0.1:9000 npm test -- logEvents focusGroupLogging
```

- `functions/tests/logEvents.spec.js` covers every type in `STUDY_LOGGING`.
- `functions/tests/focusGroupLogging.spec.js` covers focus group sessions and also needs the Realtime Database emulator.
- The emulator needs `LOG_ACTOR_HASH_SALT` in `functions/.env.local`; any test value works there.

Frontend: `npx vue-cli-service test:unit` covers the runtime, client, Logs view, participant timeline and producer views.

For every new type or event, test:

- allowed and denied roles, and that unknown study types stay denied;
- the consent gate (nothing accepted before consent);
- verification: a verified event is refused when the saved answer doesn't support it;
- rejected extra or invalid detail fields;
- that no stored log contains entered text.

**Deployed salt:** never change `LOG_ACTOR_HASH_SALT` on a deployed project. A different salt gives every returning participant a new session and a new label.

## Not implemented

- **Accessibility studies:** no logging and no Logs page yet.
- **Focus group attendees and observers:** only the facilitator's session start and end are logged.
- **Card sorting card moves:** only open, consent and submit are logged. Card and category names must never be logged; counts would be the safe next step.
- **AI emotion logging (GSoC M5 stretch):** not started.

## Related pages

- [GSoC 2026 proof of work - Justin Timothy](GSoC2026-JustinTimothy.md)
- [Logging reference in the repository](https://github.com/ruxailab/RUXAILAB/blob/develop/docs/logging-extension-guide.md)
- [Trusted ingestion PR #2295](https://github.com/ruxailab/RUXAILAB/pull/2295)
- [Log Explorer PR #2338](https://github.com/ruxailab/RUXAILAB/pull/2338)
- [Card sorting and focus group logging PR #2450](https://github.com/ruxailab/RUXAILAB/pull/2450)
- [Overview and export PR #2451](https://github.com/ruxailab/RUXAILAB/pull/2451)
