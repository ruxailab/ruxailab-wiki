# GSoC 2026 — Focus Group Management and Analysis Module

## Contributor

- **Name:** M. Mohith
- **GitHub:** [@mohi-devhub](https://github.com/mohi-devhub)
- **Email:** [achumohith14@gmail.com](mailto:achumohith14@gmail.com)

## Project

**Focus Group Management and Analysis Module for RUXAILAB** (medium, 175 hours; mentors: Marc and Karine). The project adds a moderated, multi-participant focus-group workflow to RUXAILAB, from study setup and live sessions through post-session review and analysis.

- **Project proposal:** [Focus Group Management and Analysis Module — GSoC 2026](https://summerofcode.withgoogle.com/programs/2026/projects/4HOKx20I)
- **Project source:** [RUXAILAB](https://github.com/ruxailab/RUXAILAB)

## Deliverables completed

The original proposal marked WP1 and WP2 as the core commitment and WP3 as stretch work. The delivered work is summarized against those work packages below.

### WP1 — Foundation and session configuration

- Registered Focus Group as a creatable study type and integrated it with the Inquiry category, routing, store, and study navigation.
- Added Focus Group study, discussion-topic, configuration, stimulus, answer, and theme models, plus the data-access/controller layer.
- Built the manager experience and discussion-guide editor for objectives, ordered topics, prompts, time estimates, and session options.

### WP2 — Live session and thematic structuring

- Built facilitator-led live sessions with participant presence, topic progression, prompts, participant chat, consent and waiting-room options, observer notes, timers, and stimulus presentation.
- Added LiveKit-powered calls and breakout rooms, facilitator/observer backroom chat, staff room access, and participation indicators.
- Persisted completed session discussions and notes for post-session review; added a facilitator-managed theme board that groups response excerpts. NLP suggestions remain distinct until a facilitator accepts them.

### WP3 — Analysis, analytics, and reporting (stretch)

- Added a server-side, facilitator-authorized, dependency-free text-analysis pipeline for participant chat: key-phrase extraction, suggested themes, extractive topic summaries, and lexical wording-similarity scores.
- Added cautious, quote-backed stance cues for possible shared or contrasting views. These are review prompts, not definitive sentiment or agreement labels. Lexical similarity is explicitly not presented as agreement.
- Added analytics for participant message share and per-topic chat coverage, including gaps in recorded chat responses. The UI explains that chat coverage does not measure spoken participation.
- Added an optional, server-side OpenRouter synthesis action, with provider credentials kept out of the browser, and a PDF report containing the reviewable analysis and facilitator-created themes.
- Added English/Spanish interface strings and unit coverage for the analysis and reporting utilities.

## Deliverables not completed or limited

- **Recording and storage of the live meeting video/audio:** the app supports live calls, but does not capture and persist full-session or per-topic recordings. LiveKit call transport alone does not create stored recordings; this requires a recording/egress and storage lifecycle. The related request remains tracked in [issue #2205](https://github.com/ruxailab/RUXAILAB/issues/2205).
- **Audio transcription and sentiment timeline:** the proposed integration with the separate `sentiment-analysis-api` and a per-participant `SentimentTimeline` were not delivered. The current analytics pipeline analyzes recorded participant chat text, not audio or transcripts. This follow-up is tracked in [issue #2143](https://github.com/ruxailab/RUXAILAB/issues/2143).

## Pull requests

All Focus Group pull requests opened for this project are listed here. PRs #2217 and #2311 were superseded by the later merged PRs noted below.

### Core module and post-session workflow

- [#2146 — Add Focus Group as a creatable study type](https://github.com/ruxailab/RUXAILAB/pull/2146) — merged
- [#2147 — Discussion guide editor, models, controller, and store](https://github.com/ruxailab/RUXAILAB/pull/2147) — merged
- [#2176 — Migrate manager view to dashboard layout](https://github.com/ruxailab/RUXAILAB/pull/2176) — merged
- [#2188 — Live session view with facilitated discussion](https://github.com/ruxailab/RUXAILAB/pull/2188) — merged
- [#2207 — Session feature selection, consent form, and no-toolbar layout](https://github.com/ruxailab/RUXAILAB/pull/2207) — merged
- [#2217 — Initial live video-call PR](https://github.com/ruxailab/RUXAILAB/pull/2217) — closed/superseded by [#2218](https://github.com/ruxailab/RUXAILAB/pull/2218)
- [#2218 — Live session video call](https://github.com/ruxailab/RUXAILAB/pull/2218) — merged
- [#2229 — Facilitator-driven prompts and session layout](https://github.com/ruxailab/RUXAILAB/pull/2229) — merged
- [#2263 — Per-topic timer and observer notes](https://github.com/ruxailab/RUXAILAB/pull/2263) — merged
- [#2288 — Stimulus upload and live presentation](https://github.com/ruxailab/RUXAILAB/pull/2288) — merged
- [#2289 — Live participation tracker](https://github.com/ruxailab/RUXAILAB/pull/2289) — merged
- [#2311 — Initial breakout-room PR](https://github.com/ruxailab/RUXAILAB/pull/2311) — closed/superseded by [#2317](https://github.com/ruxailab/RUXAILAB/pull/2317)
- [#2317 — Breakout rooms with per-group video and chat](https://github.com/ruxailab/RUXAILAB/pull/2317) — merged
- [#2318 — Private facilitator/observer backroom chat](https://github.com/ruxailab/RUXAILAB/pull/2318) — merged
- [#2330 — Staff access to breakout rooms and facilitator call](https://github.com/ruxailab/RUXAILAB/pull/2330) — merged
- [#2331 — Staff, participants, and per-session live rooms](https://github.com/ruxailab/RUXAILAB/pull/2331) — merged
- [#2368 — Post-session answer review and thematic structuring](https://github.com/ruxailab/RUXAILAB/pull/2368) — merged
- [#2381 — Session invites, privacy, and review-flow fixes](https://github.com/ruxailab/RUXAILAB/pull/2381) — merged
- [#2386 — Guided sessions and invite routing](https://github.com/ruxailab/RUXAILAB/pull/2386) — merged
- [#2398 — Session collaboration UI polish](https://github.com/ruxailab/RUXAILAB/pull/2398) — merged

### WP3 analysis and reporting

- [#2418 — Implement post-session analysis](https://github.com/ruxailab/RUXAILAB/pull/2418) — merged

## Related project issues

- **Foundation and session flow:** [#2134](https://github.com/ruxailab/RUXAILAB/issues/2134) data models; [#2135](https://github.com/ruxailab/RUXAILAB/issues/2135) creation wiring; [#2136](https://github.com/ruxailab/RUXAILAB/issues/2136) manager and guide editor; [#2137](https://github.com/ruxailab/RUXAILAB/issues/2137) live session.
- **Capture and analysis:** [#2138](https://github.com/ruxailab/RUXAILAB/issues/2138) multi-participant capture; [#2139](https://github.com/ruxailab/RUXAILAB/issues/2139) answer persistence; [#2140](https://github.com/ruxailab/RUXAILAB/issues/2140) manual themes; [#2141](https://github.com/ruxailab/RUXAILAB/issues/2141) i18n and tests; [#2142](https://github.com/ruxailab/RUXAILAB/issues/2142) keyword/theme extraction; [#2143](https://github.com/ruxailab/RUXAILAB/issues/2143) summaries, consensus, and sentiment bridge; [#2144](https://github.com/ruxailab/RUXAILAB/issues/2144) polish and review; [#2145](https://github.com/ruxailab/RUXAILAB/issues/2145) analytics and PDF.
- **Session extensions:** [#2201](https://github.com/ruxailab/RUXAILAB/issues/2201) no-toolbar layout; [#2202](https://github.com/ruxailab/RUXAILAB/issues/2202) consent; [#2203](https://github.com/ruxailab/RUXAILAB/issues/2203) feature selection; [#2204](https://github.com/ruxailab/RUXAILAB/issues/2204) backroom chat; [#2205](https://github.com/ruxailab/RUXAILAB/issues/2205) session recording (not delivered); [#2206](https://github.com/ruxailab/RUXAILAB/issues/2206) video call and topic timer; [#2226](https://github.com/ruxailab/RUXAILAB/issues/2226) participation tracker; [#2227](https://github.com/ruxailab/RUXAILAB/issues/2227) breakout rooms; [#2228](https://github.com/ruxailab/RUXAILAB/issues/2228) stimulus presentation.

## Additional materials

- [Focus Group module developer guide](focusgroups)
- [Focus Group analysis developer guide](analysis)
- [Focus Group wireframes in Figma](https://www.figma.com/design/iXzEv5cVO84JO8SMhwWXRB/Wireframes-for-Focus-Groups?node-id=0-1&t=EFlyK0xn02ZcsjDh-1)

## Future work

1. Add consent-aware LiveKit recording/egress, secure storage, per-topic markers or segments, retention controls, and playback in the answer review. Keep recording distinct from the live call itself.
2. Integrate the existing transcription/sentiment service behind an explicit researcher action, then visualize timestamped results with clear provenance and limitations.
3. Continue validating the keyword, theme, summary, and stance heuristics against varied real sessions; improve multilingual behavior and expose supporting excerpts so facilitators can verify suggestions.

## Conclusion

The project delivered the core Focus Group workflow and a substantial portion of the proposed WP3 stretch: researchers can configure and run structured group sessions, review and thematically organize responses, inspect facilitator-oriented text analytics, and export a report. The implementation keeps researcher judgment central and labels the limits of text-derived measures. Recording-backed audio analysis remains future work rather than being represented as complete.
