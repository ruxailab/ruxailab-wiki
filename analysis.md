# Focus Group analysis — developer guide

This page documents the current post-session analysis implementation and how to extend it. It does not describe a general-purpose or trained machine-learning model. For the overall Focus Group data/session architecture, see [focusgroups.md](focusgroups).

## What runs, and when

Analysis is an explicit facilitator action on a finished session. The default pipeline runs server-side in Firebase Functions and does not require a third-party AI key. Optional LLM synthesis is a separate action, only available after the standard analysis has been generated.

```text
finished session in answers/{answersDocId}.sessions[sessionId]
    └─ runFocusGroupAnalysis (authenticated facilitator callable)
         ├─ flatten participant chat messages
         ├─ analyze each topic: phrases, extractive summary, wording similarity, stance cues
         ├─ suggest cross-response themes
         └─ persist under sessions[sessionId].analysis

optional: synthesizeFocusGroupAnalysis
    └─ sends bounded analysis summaries to the server-configured OpenRouter model
```

Primary implementation files:

- `functions/src/https/focusGroupAnalysis.js` — callable handler, access checks, participant selection, persistence.
- `functions/src/features/focusGroupAnalysis/flattenSession.js` — message normalization and grouping by topic and participant.
- `keywordExtractor.js`, `themeExtractor.js`, `summarizer.js`, `textVectorize.js`, `consensusAnalyzer.js` — dependency-free analysis stages.
- `functions/src/https/focusGroupSynthesis.js` — optional model-backed synthesis.
- `src/ux/FocusGroup/views/FocusGroupAnalyticsView.vue` and `src/ux/FocusGroup/components/analytics/` — facilitator dashboard.
- `src/ux/FocusGroup/utils/*Report.js` — report-specific formatting and table data.

See the [analysis implementation](https://github.com/ruxailab/RUXAILAB/tree/develop/functions/src/features/focusGroupAnalysis), [callable handlers](https://github.com/ruxailab/RUXAILAB/tree/develop/functions/src/https), [analytics view](https://github.com/ruxailab/RUXAILAB/blob/develop/src/ux/FocusGroup/views/FocusGroupAnalyticsView.vue), and [WP3 PR #2418](https://github.com/ruxailab/RUXAILAB/pull/2418).

## Default, non-LLM pipeline

The callable reads the canonical study and answer documents; it does not trust a client-provided answer document mapping. It rejects unauthenticated requests, non-facilitators, mismatched answer documents, and missing studies/sessions. It derives participant IDs from the persisted session roster and excludes non-participant roles before processing chat messages.

For each topic with participant messages, the pipeline returns:

- **Key phrases:** concise candidate phrases ranked from participants' literal responses. These are suggestions for review, not finalized themes.
- **Suggested themes:** cross-response groupings with supporting response references. The facilitator chooses whether to adopt them into the separate theme board.
- **Extractive summary:** selected original participant sentences; it does not claim to generate a paraphrase.
- **Participant wording similarity:** a lexical overlap score calculated from text. It indicates shared wording only; it is not an agreement, consensus, sentiment, or response-quality score.
- **Possible shared/contrasting views:** cautious heuristic stance cues grouped by aspect and accompanied by the original supporting quotes. These are tentative review leads, not definitive sentiment labels or a semantic judgment of agreement.

The standard pipeline is deterministic JavaScript text processing; it makes no model/API call. It may miss paraphrases, context, sarcasm, negation outside its cue patterns, multilingual nuance, or a meaningful finding phrased only once. Facilitators should inspect the original responses before drawing research conclusions.

## Metrics shown to facilitators

- **Participant message share** is each participant's share of recorded participant chat messages for the session. It is not a measure of contribution quality or spoken participation.
- **Chat coverage by topic** counts participants with at least one recorded chat response for a topic and identifies participants with no recorded chat response. Missing chat is not evidence that someone did not speak.
- **Possible shared/contrasting views** presents quote-backed, tentative stance patterns where the text contains explicit cues.

These are intentionally distinct from a claim that the system has measured consensus. Audio/video capture, transcripts, and spoken-turn coverage are not currently inputs to this analytics pipeline.

## Optional OpenRouter synthesis

The optional synthesis callable receives a bounded context derived from the saved topic summaries, keywords, and wording-similarity notes. It is not the default analysis and should not be described as such. The system prompt instructs the model not to infer agreement from wording similarity or invent quotes/causes. The user reviews the result before saving it.

Server configuration uses:

```dotenv
CHAT_BUILDER_OPENROUTER_API_KEY=
CHAT_BUILDER_OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
FOCUS_GROUP_ANALYSIS_OPENROUTER_MODEL=
```

The analysis-specific model can fall back to `CHAT_BUILDER_OPENROUTER_STUDY_MODEL` when unset. Keep keys in the server/functions environment only—never in a `VUE_APP_*` variable, browser bundle, screenshot, or committed `.env` file. Add safe, redacted server diagnostics when investigating provider failures; distinguish missing/invalid credentials from model access, quota, and request errors without logging the key or participant text.

## Persistence and reporting

The standard result is persisted at `answers/{answersDocId}.sessions.{sessionId}.analysis`, alongside the session it describes. Optional synthesis is saved separately under that session's `analysis.deepAnalysis`. The answer review's manually curated theme board remains in the answer document's `themes` array; generated suggestions do not replace it automatically.

The PDF report includes the reviewed session context, participant/theme material, supported analysis findings, and chat-coverage information. If changing analysis fields or display labels, update both the interactive analytics view and the PDF/report utilities so the exported report remains consistent. Test theme inclusion and page wrapping with realistic long content.

## Extending and testing analysis

1. Keep transformations pure in `functions/src/features/focusGroupAnalysis/` where possible and add focused unit tests in `functions/tests/`.
2. Add role/ownership and persistence tests around callable changes in `functions/tests/focusGroupAnalysis.spec.js`.
3. Preserve participant boundaries and topic attribution; test blank messages, observer/facilitator exclusion, missing topics, and duplicate/short text.
4. For every metric, document exactly what it measures and what it does not. Do not rename lexical similarity as consensus.
5. Keep generated suggestions separate from facilitator-approved themes, and retain evidence references/quotes for findings that need review.
6. Never include raw API credentials in client code or logs. Avoid sending participant content to a model unless the facilitator invokes the optional synthesis and the deployment's privacy configuration permits it.

From `functions/`, use `npm test -- --runInBand` and `npm run lint`; from the app root, use the project test/lint/build scripts and add a report test if a PDF-facing field changes.

## Not implemented

- **Audio sentiment bridge and `SentimentTimeline`:** proposal stretch work remains follow-up; the current analyzer consumes text chat only. See [issue #2143](https://github.com/ruxailab/RUXAILAB/issues/2143).
- **Stored full-session or per-topic recordings:** LiveKit provides the call transport, not persistent recording. Recording/egress, consent, storage, retention, and playback need a separate implementation. See [issue #2205](https://github.com/ruxailab/RUXAILAB/issues/2205).
- **Semantic consensus detection:** lexical overlap and explicit cue heuristics are not semantic understanding. The UI avoids claiming that they establish participant agreement.

## Related pages

- [Focus Groups in RUXAILAB](focusgroups)
- [GSoC 2026 proof of work](GSoC2026-Mohith)
