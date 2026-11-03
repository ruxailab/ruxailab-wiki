# GSoC 2026 — AI Tool for Heuristic Evaluation

## Contributor

- **Name:** Montse Ponsa Capell
- **Organization:** [Uramaki LAB](https://github.com/ruxailab)
- **GitHub:** [@mponsa12](https://github.com/mponsa12)
- **Email:** [mponsa12@gmail.com](mailto:mponsa12@gmail.com)

## Mentors' Info
- [Marc Gonzalez Capdevila](https://github.com/marcgc21)
- [Karine Pistili](https://github.com/KarinePistili)

## Project
**AI Tool for Heuristic Evaluation for RUXAILAB** (large, 350 hours). The project focuses on improving the heuristic evaluation workflow in RUXAILAB by enhancing usability and streamlining the evaluation process. It also integrates AI agents to automatically answer heuristic evaluation questions and generate AI-powered final reports.

- **Project proposal:** [AI Tool for Heuristic Evaluation — GSoC 2026](https://summerofcode.withgoogle.com/programs/2026/projects/AWtPHjCE)
- **Project source:** [RUXAILAB](https://github.com/ruxailab/RUXAILAB)

## Deliverables completed

### 1. Heuristic Evaluation (MS1)

Focused on improving the usability and user experience of the heuristic evaluation workflow.

- Redesigned the heuristic evaluation dashboard and improved result visualization.
- Enhanced question forms, response handling and navigation.
- Improved the evaluation interface to provide a more intuitive and consistent user experience.

### 2. Use AI Agents (MS2)

Focused on integrating AI agents to automate and improve heuristic evaluations.

- Developed a reusable AI agent module with configuration, management and support for multiple AI providers.
- Integrated AI agents to automatically answer heuristic evaluation questions.
- Added a community section for discovering public AI agents.
- Implemented asynchronous evaluation processing with real-time progress tracking.
- Added pause, resume, and retry functionality without losing evaluation progress.
- Improved evaluation navigation, completion and result management.
- Added support for traditional, detailed, and weighted evaluation modes.

### 3. Additional Platform Improvements

Contributions to the usability and maintainability of RUXAILAB.

- Improved menu organization, navigation, and UI consistency.
- Fixed navigation issues and enhanced user feedback notifications.
- Refactored storage management with dynamic resolution and separate modules for each studio.


## Deliverables not completed, and why

**MS4 — AI-Powered PDF Report Generation**

Milestone 4, which focused on generating and exporting AI-powered heuristic evaluation reports in PDF format, was not completed.

This was mainly because Milestone 3 required more development time than initially anticipated to implement and refine the heuristic evaluation workflow. Additionally, the ISO required to update the website was not available, which caused further delays.

As a result, PDF report generation remains pending and is planned as future work.


## Pull requests

The following pull requests summarize the main contributions made to RUXAILAB, organized by functionality.

### Heuristic Evaluation Workflow

Improvements to the heuristic evaluation process, including evaluation execution, response handling, and result visualization.

- [#2431 — Improve heuristic AI evaluation workflow](https://github.com/ruxailab/RUXAILAB/pull/2431)
- [#2407 — Fix heuristic evaluation response flow](https://github.com/ruxailab/RUXAILAB/pull/2407)
- [#2177 — Improve current answer interface using Stitch ideas](https://github.com/ruxailab/RUXAILAB/pull/2177)

### AI Agent Integration

Development and integration of reusable AI agents to automate heuristic evaluations.

- [#2277 — Implement AI agents for heuristic evaluations](https://github.com/ruxailab/RUXAILAB/pull/2277)
- [#2238 — Add reusable AI agents module](https://github.com/ruxailab/RUXAILAB/pull/2238)

### UI/UX Improvements

Enhancements to the interface, navigation, and overall user experience across RUXAILAB.

- [#2154 — Refactor menu naming and update routes](https://github.com/ruxailab/RUXAILAB/pull/2154)
- [#2125 — Update heuristic evaluation dashboard styling](https://github.com/ruxailab/RUXAILAB/pull/2125)
- [#2107 — Improve comment actions and unify global toast handling](https://github.com/ruxailab/RUXAILAB/pull/2107)
- [#2106 — Fix navigation link to cooperators from reports](https://github.com/ruxailab/RUXAILAB/pull/2106)

### Storage and Architecture

Improvements to the organization and management of storage modules across RUXAILAB studios.

- [#2129 — Create a new storage module for each studio](https://github.com/ruxailab/RUXAILAB/pull/2129)
- [#2114 — Replace hardcoded storage module with dynamic calculation](https://github.com/ruxailab/RUXAILAB/pull/2114)


## Additional materials
- [First Iteration Stitch designs](https://stitch.withgoogle.com/projects/12061720715149914209)
- [Second Iteration Stitch designs](https://stitch.withgoogle.com/projects/14887834714452941830)


## Future work

1. Implement the generation and export of AI-powered heuristic evaluation reports in PDF format, including evaluation results, detected usability issues, and improvement recommendations.
2. Continue improving AI agent accuracy and consistency across different websites, heuristic evaluation criteria, and study modes.
3. Further enhance the heuristic evaluation workflow based on user feedback, focusing on usability, performance, and the reliability of asynchronous evaluations.

## Conclusion

The project delivered significant improvements to the heuristic evaluation workflow in RUXAILAB, including a redesigned user interface, reusable AI agents, and automated heuristic evaluations. Researchers can configure and execute AI-powered evaluations, track their progress, manage responses, and review results through an improved interface.

Additional contributions enhanced navigation, storage architecture, and overall usability across the platform. The generation of AI-powered PDF reports remains future work.
