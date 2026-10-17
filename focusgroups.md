# Focus Groups in RUXAILAB — developer guide

This guide maps the Focus Group feature to the existing RUXAILAB architecture. It is intended for contributors extending the feature; for analysis algorithms and their interpretation limits, see [analysis.md](analysis).

## Architecture at a glance

The feature lives primarily in `src/ux/FocusGroup/`, following the app's per-study-method organization. Shared services remain in their existing shared modules rather than being copied into Focus Group code.

| Area | Main code |
| --- | --- |
| Study models | `models/FocusGroupStudy.js`, `DiscussionTopic.js`, `FocusGroupConfig.js`, `Stimulus.js` |
| Answer/theme models | `models/FocusGroupStudyAnswer.js`, `Theme.js` |
| Data access | `controllers/FocusGroupController.js` |
| State and callable functions | `store/FocusGroup.js` |
| Routes and role/capability checks | `router.js`, shared `studyAccessPolicy` |
| Study manager and guide editor | `views/ManagerView.vue`, `views/EditFocusGroupView.vue`, `components/DiscussionGuideEditor.vue`, `components/SessionConfigEditor.vue` |
| Live session | `views/FocusGroupSessionView.vue`, `composables/useFocusGroupSession.js`, `components/session/` |
| Post-session review and themes | `views/FocusGroupAnswerView.vue`, `components/ThematicEditor.vue` |
| Analytics and report | `views/FocusGroupAnalyticsView.vue`, `components/analytics/`, `utils/*Report.js` |

Useful entry points in the source repository: [FocusGroup module](https://github.com/ruxailab/RUXAILAB/tree/develop/src/ux/FocusGroup), [analysis Cloud Functions](https://github.com/ruxailab/RUXAILAB/tree/develop/functions/src/features/focusGroupAnalysis), and [function handlers](https://github.com/ruxailab/RUXAILAB/tree/develop/functions/src/https).

## Data ownership and lifecycle

- A study is stored in Firestore's `tests/{studyId}` collection. `FocusGroupStudy` serializes its ordered `discussionGuide`, session `config`, and `stimuli` alongside the inherited study fields.
- A study's answer document lives in `answers/{answersDocId}`. `FocusGroupStudyAnswer` stores completed sessions in a `sessions` map keyed by `sessionId`, plus the facilitator-managed `themes` array.
- During a live session, shared state is synchronized through Firebase Realtime Database under `focusGroupSessions/{roomId}`. Scheduled sessions use an isolated room ID; the legacy room uses the study ID. Presence, topic position, messages, consent decisions, notes, prompts, timer, stimuli state, and breakout state are live-session data.
- Private facilitator/observer backroom messages use a separate top-level `focusGroupBackroom/{roomId}` path. Keeping this separate is important: RTDB read permissions cascade down from a parent, so placing private data below a participant-readable session node would not provide the intended isolation.
- When a session ends, the session view/store writes the completed session snapshot to the answer document. Post-session answer review reads the sessions and themes back from that document.
- The in-session video call uses the shared LiveKit video-call integration. A live call is not a recording: this feature does not currently persist a full-session or per-topic recording.

## Session roles and access control

The feature reuses RUXAILAB's access levels: facilitator/admin (`0`), participant (`1`), and observer (`3`). Display role labels are localized and should not be used as authorization values. RTDB rules and the app's study-capability policy enforce what a role may read or change. Analysis and optional synthesis callables independently require an authenticated facilitator and verify that the answer document belongs to the requested study.

When adding routes or data paths:

1. Add the correct study capability to the route and navigation policy; client-side hiding is not an access check.
2. Add/adjust Firestore or RTDB rules for the exact path and role. Keep private observer/facilitator data out of participant-readable RTDB ancestors.
3. Validate authorization again in every callable or trusted server boundary.
4. Add tests for both allowed and denied roles, including direct URL/callable access.

## Extending the module

- Add study configuration fields to `FocusGroupConfig`, including serialization and a default that preserves existing studies.
- Add guide-topic behavior to `DiscussionTopic` and the guide editor; preserve stable topic IDs because discussions and analysis refer to those IDs.
- Add session-time synchronized state through `useFocusGroupSession`. Keep writes scoped to the correct room ID, handle disconnects, unsubscribe listeners on unmount, and consider whether the state belongs in the public session tree or the private backroom tree.
- Add persisted answer fields through `FocusGroupStudyAnswer` and `FocusGroupController`; update review rendering and PDF export if the field should appear after the session.
- Keep manually curated themes separate from generated suggestions. Suggestions should not silently overwrite facilitator decisions.
- Put reusable video-call behavior in `src/shared/components/videoCall/`; Focus Group should configure and consume the shared integration rather than fork the media transport.

## Tests and local checks

Relevant tests are in `tests/unit/`, `functions/tests/`, and the Firebase rules test configuration. From the application root, the standard commands include:

```sh
npm test -- --runInBand
npm run lint
npm run build-prod
```

For Cloud Functions, run the functions package's tests and lint from `functions/`:

```sh
npm test -- --runInBand
npm run lint
```

If a change touches role boundaries or database paths, also run the repository's emulator-backed rules tests (`npm run test:rules`) and add focused allow/deny cases. Use the repository's current setup guide for Firebase emulator configuration; never put real credentials in documentation or test fixtures.

## Related work

- [GSoC 2026 proof of work](GSoC2026-Mohith)
- [Focus Group analysis guide](analysis)
- [Core module pull request](https://github.com/ruxailab/RUXAILAB/pull/2146)
- [Guide/models/store pull request](https://github.com/ruxailab/RUXAILAB/pull/2147)
- [Live session pull request](https://github.com/ruxailab/RUXAILAB/pull/2188)
- [Post-session review and themes](https://github.com/ruxailab/RUXAILAB/pull/2368)
- [Post-session analysis and report](https://github.com/ruxailab/RUXAILAB/pull/2418)
