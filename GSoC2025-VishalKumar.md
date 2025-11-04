# GSoC 2025 — Final Work Report

> AI-Powered Accessibility Evaluation in Ruxailab
>
> Last updated: 2025-11-04

---

## At a glance

| Category | Details |
|---|---|
| Contributor | Vishal Kumar ([@saltykheera](https://github.com/saltykheera)) |
| Email | N/A |
| Organization | URAMAKI LAB ([ruxailab](https://github.com/ruxailab)) |
| Project | AI-Powered Accessibility Evaluation in Ruxailab |
| Program Page | https://summerofcode.withgoogle.com/programs/2025/organizations/uramaki-lab |
| Proposal | https://docs.google.com/document/d/e/2PACX-1vSR2hrXOH9RfvwxAV863VpcSCTR0UnLLn_6OwaXJzYu8GEZqc506wuevT0qfMuSPq9hDIrzZCOawuMC/pub |
| Avatar | ![avatar](https://avatars.githubusercontent.com/u/142778969?v=4) |

### Quick links

- Main repositories
  - RUXAILAB (app): https://github.com/ruxailab/RUXAILAB
  - Accessibility testing backend (automatic): https://github.com/ruxailab/accessiblity-testing-backend
  - AI accessibility API: https://github.com/ruxailab/ai-accessibility-api
- PR/Commits authored by @saltykheera
  - RUXAILAB: https://github.com/ruxailab/RUXAILAB/commits/organization-feature-accessibility/?author=saltykheera
  - Backend: https://github.com/ruxailab/accessiblity-testing-backend/commits/main/?author=saltykheera
  - AI API: https://github.com/ruxailab/ai-accessibility-api/commits/main/?author=saltykheera

---

## People

| Role | Name |
|---|---|
| Contributor | Vishal Kumar |
| Primary Mentor | Marc Gonzalez Capdevila |
| Assisting Mentor(s) | Sebastian Jitaru |

---

## Project overview

Web accessibility evaluation is often fragmented, manual, and inconsistent. Evaluators need a unified, repeatable way to find, document, and share WCAG-compliant issues across web applications.

This project delivers an integrated toolkit with three complementary modes:

1. Manual Audit Assistant — guided checklists, keyboard/ARIA inspection helpers, and in-browser annotations for human reviewers.
2. Automated Scanner — crawls pages, runs rule-based checks against WCAG success criteria, and flags common violations.
3. AI-Assisted Reviewer — prioritizes issues, suggests fixes, and generates human-readable explanations and code examples.

Common features include page analysis, issue grouping, collaborative sharing, and exportable reports (PDF/Markdown/CSV). The implementation follows WCAG guidelines as the source of rules and maps detected issues to specific success criteria for traceability.

---

## Objectives

- [x] Manual Accessibility Testing tool
- [x] Automated Accessibility Testing tool
- [x] AI‑Assisted accessibility testing tool

---

## Phases and delivery

| Phase | Summary |
|---|---|
| Design | User-centered design for three modes (Manual, Automated, AI‑Assisted). Vuetify prototypes, UI/UX flows, WCAG mapping, specs, and acceptance criteria. |
| Development | Modular, testable architecture; analysis engine; collaboration/summary services; report generation; API contracts; CI/CD; automated tests; incremental integrations. |
| Feature & Release | Stabilized user-facing features (sharing, RBAC, annotations, exports); thorough QA and accessibility testing; staged rollouts; usability iterations. |

---

## Work components

### 1) Manual Accessibility Tool

| Item | Details |
|---|---|
| Scope | Manual testing workflow, WCAG-configurable modules, collaborative review |
| Status | Delivered |
| Key PRs | See below |

Key tasks and achievements:
- Implemented and integrated a manual accessibility testing model into the study workflow.
- Seamless integration with the existing study creation and configuration flow.
- Configurable test module with WCAG conformance levels (A, AA, AAA).
- Testing/preview UI with notes, image attachments, and manual annotations mapped to WCAG success criteria.
- Tabular review of answers and test results.
- Collaborative workflows to invite participants.
- Aggregation and categorization of responses for comparison and analysis.
- Role-based permissions (admin/evaluator/guest) with appropriate restrictions.

PRs:
- #937 Accessibility Testing Tool (Manual/Automatic) — https://github.com/ruxailab/RUXAILAB/pull/937
- #956 fix: config not saving in Firestore — https://github.com/ruxailab/RUXAILAB/pull/956
- #965 add: new flow for accessibility tests — https://github.com/ruxailab/RUXAILAB/pull/965
- #966 enhanced: cooperative view for manual accessibility — https://github.com/ruxailab/RUXAILAB/pull/966
- #969 added: dashboard consistency across tests (MANUAL, AUTOMATIC) — https://github.com/ruxailab/RUXAILAB/pull/969
- #973 See PR — https://github.com/ruxailab/RUXAILAB/pull/973
- #977 chore: routes, pre-implemented config, page wrapper layout — https://github.com/ruxailab/RUXAILAB/pull/977

Challenges overcome:
- Refactored project structure for clarity and scalability; adapted manual tool to new workflow across API, UI, and configuration layers.

---

### 2) Automatic Accessibility Testing Tool

| Item | Details |
|---|---|
| Scope | Express.js backend + pa11y scanner; frontend integration & reports |
| Status | Delivered |
| Key Links | Commits in app/backend below |

Key tasks and achievements:
- Backend (Express.js) providing REST endpoints for accessibility scans.
- Integrated pa11y to run automated WCAG checks and normalize results.
- API accepts URLs, queues scans, and returns structured results by WCAG principles and success criteria.
- Frontend module to submit URLs, monitor progress/status, and display grouped findings with recommendations.
- Persistence of scan results, report page with stats and exports (CSV/JSON/Markdown).
- Collaboration: invite reviewers; role-based access control.
- Robust client-server communication with error handling, retries, and progress feedback.

Commits by author:
- RUXAILAB app: https://github.com/ruxailab/RUXAILAB/commits/organization-feature-accessibility/?author=saltykheera
- Backend: https://github.com/ruxailab/accessiblity-testing-backend/commits/main/?author=saltykheera

Challenges overcome:
- Ensured web‑worker/browser compatibility across Linux, macOS, and Windows by handling platform-specific Chrome executable paths.

---

### 3) AI Assistant Tool

| Item | Details |
|---|---|
| Scope | Flask + Selenium analyzers; ML for links; BLIP for image alt; collaborative frontend |
| Status | Delivered |
| Key Links | Commits in app/API below |

Key tasks and achievements:
- Backend: Flask REST API + Selenium analyzers for color contrast, keyboard/link navigation, and image alt attributes.
- Anchor Text Classifier: TF‑IDF → Logistic Regression pipeline; utilities for single/batch predictions; simple retraining via `training_data.csv`.
- Image Alt/Captioning: Pretrained BLIP (Salesforce) captioner; CPU/GPU inference support; helpers for URL/file/batch.
- Frontend: Unified input for URL/HTML, users select test types; results tracked in global store; collaborative viewer and report generator.

Commits by author:
- RUXAILAB app: https://github.com/ruxailab/RUXAILAB/commits/organization-feature-accessibility/?author=saltykheera
- AI API: https://github.com/ruxailab/ai-accessibility-api/commits/main/?author=saltykheera

Challenges overcome:
- Data/model constraints (noisy labels, class imbalance, large pretrained models); automation fragility (Selenium/pa11y, JS-rendered content, cross-platform browser issues); delivering reliable WCAG-mapped suggestions within packaging/CI/CD/batching/latency limits.

---

## Deliverables

| Deliverable | Link |
|---|---|
| AI Accessibility API — Commits delivered | https://github.com/ruxailab/ai-accessibility-api/commits/main/?author=saltykheera |
| Main App (RUXAILAB) — Feature work | https://github.com/ruxailab/RUXAILAB/commits/organization-feature-accessibility/?author=saltykheera |
| Automatic Testing Backend — Feature work | https://github.com/ruxailab/accessiblity-testing-backend/commits/main/?author=saltykheera |

---

## Additional materials

| Type | URL |
|---|---|
| Figma / Design | N/A |
| Blog post | N/A |
| Demo / Video | N/A |

---

## Conclusion

This project unified manual, automated, and AI-assisted accessibility evaluation into a cohesive toolkit mapped directly to WCAG. I learned to balance UX, performance, and explainability while integrating rule-based checks with ML-driven suggestions. Collaborating with mentors on architecture, CI/CD, and cross-platform browser automation sharpened my engineering discipline and product sense. I’m grateful to Marc Gonzalez Capdevila and Sebastian Jitaru for their guidance and to the URAMAKI LAB community for the trust and support throughout GSoC.

---

## Appendix

- Organization GitHub: https://github.com/ruxailab
- GSoC Org Page: https://summerofcode.withgoogle.com/programs/2025/organizations/uramaki-lab
- Proposal (public): https://docs.google.com/document/d/e/2PACX-1vSR2hrXOH9RfvwxAV863VpcSCTR0UnLLn_6OwaXJzYu8GEZqc506wuevT0qfMuSPq9hDIrzZCOawuMC/pub
