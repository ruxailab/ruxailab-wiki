# <img align="center" width="60px" src="https://en.opensuse.org/images/9/91/Gsocsun.png"> GSoC 2025 - Final Work Report: UI Layout Optimization for RUXAILAB and Migrating the Codebase to Vue 3

## Contributor Info

<div container>
<table>
<tr>
<td width="600px">
&#8226; Name: Sahitya Chandra <br />
&#8226; Organization: <a href="https://github.com/ruxailab" target="_blank">Uramaki LAB</a><br />
&#8226; Email: <a href="mailto:sahityajb@gmail.com" target="_blank">sahityajb@gmail.com</a><br />
&#8226; GitHub: <a href="https://github.com/sahitya-chandra" target="_blank">sahitya-chandra</a><br />
&#8226; LinkedIn: <a href="https://www.linkedin.com/in/sahitya-chandra75/" target="_blank">Sahitya Chandra</a><br />
&#8226; X: <a href="https://x.com/sahitya_twt" target="_blank">sahitya_twt</a><br />
<td>
<a href="https://github.com/sahitya-chandra"><img src="https://github.com/sahitya-chandra.png" height="250px" width="250px;" alt="Sahitya Chandra"/></a>
</td>
</tr>
</table>
</div>

## Mentors' Info

- **Mentor:** [Marc Gonzalez Capdevila](https://github.com/marcgc21)
- **Assisting Mentor:** Leticia Carvalho Ramos

## Project Details

### Project Title
UI Layout Optimization for RUXAILAB and Migrating the Codebase to Vue 3

### GSoC Project Page
- [GSoC 2025 with Uramaki LAB](https://summerofcode.withgoogle.com/programs/2025/projects/iTnW9V5g)

### Project Proposal
- [Project Proposal](https://docs.google.com/document/d/1gOuTJ2VdnZASMVJo1a8-Z_o9IgnqWcQ8xeNKqbKJjcE/edit?usp=sharing)

### Project Repository
- [RUXAILAB Main Repository](https://github.com/ruxailab/RUXAILAB)

### Objectives
The primary objectives of my GSoC 2025 project with Uramaki LAB were:
1. **UI Layout Optimization**: Redesign and optimize the user interface of the RUXAILAB platform to enhance usability, accessibility, and responsiveness, ensuring a seamless experience for researchers and participants.
2. **Vue 3 Migration**: Migrate the existing RUXAILAB codebase from Vue 2 to Vue 3 to leverage modern features, improve performance, and ensure long-term maintainability.
3. **Feature Enhancements**: Implement new features for unmoderated usability testing and heuristic evaluation to expand the platform’s capabilities.

### Project Description
RUXAILAB is an open-source platform designed to facilitate usability testing and user experience research. My project focused on improving the platform by revamping its UI and migrating its codebase from Vue 2 to Vue 3. The UI optimization involved redesigning layouts to improve navigation, usability, accessibility (WCAG compliance), and responsiveness across devices. The migration to Vue 3 ensured the codebase could leverage modern Vue features like the Composition API, better TypeScript support, and improved performance.

Beyond the initial goals, I implemented end-to-end features for unmoderated usability testing and heuristic evaluation, adding functionalities such as task-based testing, restrict participant during analytics calculation, enhanced filtering, and Firebase storage integration for user uploads. These enhancements aimed to make the platform more robust and user-friendly for conducting usability studies.

### Project Structure
- **Design Phase**: Created wireframes and mockups for redesigned UI components, focusing on accessibility and responsive design.
- **Development Phase**: Implemented new UI layouts, fixed bugs, and added features using Vue.js, Vuetify, and Firebase.
- **Migration Phase**: Upgraded the codebase from Vue 2 to Vue 3, refactoring components, updating dependencies, and ensuring compatibility.
- **Feature Implementation**: Developed new features for unmoderated usability testing and heuristic evaluation, including task management and storage usage tracking.
- **Testing and Refinement**: Conducted testing to ensure functionality, accessibility, and performance, iterating based on community feedback.

## Work Summary

### 1. Vue 3 Migration
The migration of the RUXAILAB codebase from Vue 2 to Vue 3 was a critical deliverable, enabling the platform to leverage modern Vue features and ensure long-term maintainability. This process involved a systematic approach to upgrading dependencies, refactoring components, and resolving compatibility issues while preserving existing functionality. The migration was conducted using the `@vue/compat` build to facilitate a smooth transition, with incremental updates to align with Vue 3 standards.

**Key Tasks and Achievements**:
- **Dependency Upgrades**: Updated core libraries to their Vue 3-compatible versions, including `vue-router` to v4, `vuetify` to v3, `vuex` to v4, and `vue-i18n` to v11. Replaced `vue-template-compiler` with `@vue/compiler-sfc` to support Vue 3’s single-file component compilation.
- **Codebase Refactoring**: Transitioned components to the Composition API, replacing Options API where feasible. Refactored lifecycle methods and reactivity usage to align with Vue 3’s reactive system. Updated component initialization to use `createApp`, `app.use`, and `app.mount`.
- **Compatibility and Error Resolution**: Addressed runtime errors and compile-time warnings flagged by `@vue/compat`. Ensured compatibility with existing features like user authentication, test creation, and task management.
- **Code Quality Improvements**: Removed deprecated Vue 2 features (e.g., `>>>` syntax) and reduced npm vulnerabilities by updating or replacing outdated packages. Refactored components to adhere to Vuetify 3 standards, enhancing maintainability.
- **Tooling Enhancements**: Introduced `eslint-plugin-vuetify` to enforce Vuetify 3 best practices. Created `eslint.config.mjs` to support Vue 3 and Composition API linting, and updated `eslint` to a compatible version.
- **Challenges Overcome**: Managed complex dependency conflicts, particularly with Vuetify 3’s styling system. Ensured backward compatibility for legacy components during the transition. Optimized the migration workflow to minimize downtime and maintain feature parity.

**Key PRs**:
- [PR #839](https://github.com/ruxailab/RUXAILAB/pull/839): Completed the migration of the RUXAILAB codebase to Vue 3, including dependency upgrades and Composition API adoption.

### 2. UI Layout Optimization
The UI layout optimization was a cornerstone of the project, aimed at enhancing usability, accessibility, and responsiveness across the RUXAILAB platform. This involved a comprehensive redesign of the entire UI of RUXAILAB, ensuring a seamless experience for researchers and participants. The redesign adhered to WCAG accessibility standards and incorporated modern, responsive layouts using Vuetify 3, improving navigation and data clarity.

**Key Tasks and Achievements**:
- **Authentication Pages**: Revamped Sign In, Sign Up, and Forgot Password views with modern, accessible designs.
- **Study Creation Flow**: Overhauled the multi-step study creation process, introducing a new Accessibility test category and a simplified flow using a stepper.
- **Dashboard and Admin Views**: Redesigned the Admin view with a complete new Dashboard view to a clean, modern layout with improved data grouping.
- **Report View Enhancements**: Upgraded the Report View for usability tests, adding user identification (full name and email or "Unknown" for anonymous users), test status (Completed or Pending), and admin actions like direct user deletion from the report table.
- **Analytics Views**:
  - **General Analytics**: Improved layout with intuitive visualizations of user participation and test outcomes, including user-level test summaries.
  - **Individual Analytics**: Introduced a tabular breakdown of user test data, detailing user origin (invited vs. anonymous) and task insights (average task time, completed vs. skipped tasks) via popup modals.
  - **SUS and NASA-TLX Analytics**: Refactored System Usability Scale (SUS) score logic to accept only valid 10-length inputs, with reusable chart components. Added NASA-TLX analytics with task filtering for workload-based insights, presented in both chart and table views.
- **Edit Test View**: Redesigned the entire UI layout of edit test views for Unmoderated Usability Test and Heuristic Evaluation.
- **Settings & Co-operator View**: Refactored both of these views with new and user-centric layouts.
- **Answer View**: Revamped the entire heuristic and user test view for a better and effortless user experience while answering the study.
- **Reusable Wrappers & Components**: Created reusable page wrappers for maintaining style consistency across the application.
- **Loader Redesign**: Created a new loader using the updated RUXAILAB logo, with improved alignments for a polished look across devices.
- **Challenges Overcome**: Balanced aesthetic improvements with functional enhancements, ensuring accessibility compliance. Addressed complex state management issues during the study creation flow redesign. Iterated designs based on community feedback to optimize user experience.

**Key PRs**:
- [PR #948](https://github.com/ruxailab/RUXAILAB/pull/948): Major UI layout optimizations and feature enhancements, including redesigned authentication, study creation, and analytics views.
- [PR #963](https://github.com/ruxailab/RUXAILAB/pull/963): Post-midterm UI optimizations, refining dashboard and report views.
- [PR #983](https://github.com/ruxailab/RUXAILAB/pull/983): Created loader with new RUXAILAB logo.
- [PR #988](https://github.com/ruxailab/RUXAILAB/pull/988): Completed next-session card on the dashboard with enhanced visuals and accessibility.

### 3. Feature Enhancements
In addition to the proposed goals, I implemented end-to-end features for unmoderated usability testing and heuristic evaluation:
- **Unmoderated Usability Testing**: Added support for manual and automatic test types, hide user functionality, improved task navigation, and fixed issues with task answer updates.
- **Heuristic Evaluation**: Enhanced heuristic evaluation workflows, fixing bugs and improving usability.
- **Firebase Storage Integration**: Implemented storage usage calculation for user tests, stored in Firestore for real-time updates.
- **Internationalization**: Improved i18n strings for better multilingual support.

**Key PRs**:
- [PR #950](https://github.com/ruxailab/RUXAILAB/pull/950): Added MANUAL & AUTOMATIC test types in list and filter.
- [PR #952](https://github.com/ruxailab/RUXAILAB/pull/952): Fixed NASA-TLX answer object updates.
- [PR #979](https://github.com/ruxailab/RUXAILAB/pull/979): Heuristic evaluation fixes.
- [PR #981](https://github.com/ruxailab/RUXAILAB/pull/981): Fixed image upload to storage during answering.
- [PR #995](https://github.com/ruxailab/RUXAILAB/pull/995): Fixed internationalization strings (open).
- [PR #1001](https://github.com/ruxailab/RUXAILAB/pull/1001): Firebase storage usage calculation.

### 4. Bug Fixes and Maintenance
I addressed various bugs and performed maintenance tasks to improve the platform’s stability:
- Fixed initialization errors in UserTestView.
- Improved task navigation and consent checkbox layouts.
- Refactored filters to support study type-based filtering.

**Key PRs**:
- [PR #871](https://github.com/ruxailab/RUXAILAB/pull/871): Fixed initialization error tooltip in UserTestView.
- [PR #886](https://github.com/ruxailab/RUXAILAB/pull/886): Ensured text fields are empty after task completion.
- [PR #932](https://github.com/ruxailab/RUXAILAB/pull/932): Fixed task clicking and consent checkbox alignment.
- [PR #935](https://github.com/ruxailab/RUXAILAB/pull/935): Fixed cooperator view for moderated tests.
- [PR #949](https://github.com/ruxailab/RUXAILAB/pull/949): Refactored filter to use study type.
- [PR #957](https://github.com/ruxailab/RUXAILAB/pull/957): Added null value checks.

### 5. Community Contributions
Beyond coding, I actively engaged with the RUXAILAB community:
- Helped other contributors set up the project locally.
- Reviewed PRs and provided feedback.

## Deliverables

### Completed Deliverables
- **Vue 3 Migration**: Successfully migrated the RUXAILAB codebase to Vue 3, ensuring compatibility and performance improvements.
- **UI Layout Optimization**: Redesigned key components (dashboard, next-session card, loader, authentication, and analytics views) with improved accessibility and responsiveness.
- **New Features**: Implemented unmoderated usability testing and heuristic evaluation features, including task management and filtering.
- **Bug Fixes**: Resolved issues in task navigation, internationalization, and initialization errors.

### Incomplete Deliverables
- **Light/Dark Mode**: Currently not needed by the Org.

## Pull Requests

| S.No | Title | Link | Status | Created | Merged |
|------|-------|------|--------|---------|--------|
| 1 | Migration of RUXAILAB codebase to Vue 3 (Completed) | [#839](https://github.com/ruxailab/RUXAILAB/pull/839) | Merged | 2025-05-01 | 2025-05-26 |
| 2 | Fix: Initialization error tooltip in UserTestView | [#871](https://github.com/ruxailab/RUXAILAB/pull/871) | Merged | 2025-05-17 | 2025-05-18 |
| 3 | Fix: Text fields empty after task completion | [#886](https://github.com/ruxailab/RUXAILAB/pull/886) | Merged | 2025-05-19 | 2025-05-19 |
| 4 | Rebase develop on vue3-migration branch | [#908](https://github.com/ruxailab/RUXAILAB/pull/908) | Merged | 2025-05-26 | 2025-05-26 |
| 5 | Fix: Clicking of tasks and consent checkbox horizontal | [#932](https://github.com/ruxailab/RUXAILAB/pull/932) | Merged | 2025-07-01 | 2025-07-01 |
| 6 | Fix: Cooperator view of moderated test | [#935](https://github.com/ruxailab/RUXAILAB/pull/935) | Merged | 2025-07-04 | 2025-07-04 |
| 7 | Rebase latest commits | [#936](https://github.com/ruxailab/RUXAILAB/pull/936) | Merged | 2025-07-04 | 2025-07-04 |
| 8 | Major UI layout optimizations and feature enhancements | [#948](https://github.com/ruxailab/RUXAILAB/pull/948) | Merged | 2025-07-15 | 2025-07-16 |
| 9 | Refactor: Modified filter to filter by study type | [#949](https://github.com/ruxailab/RUXAILAB/pull/949) | Merged | 2025-07-17 | 2025-07-17 |
| 10 | Fix: Added MANUAL & AUTOMATIC testType in list and filter | [#950](https://github.com/ruxailab/RUXAILAB/pull/950) | Merged | 2025-07-17 | 2025-07-17 |
| 11 | Fix: NASA-TLX answer object update | [#952](https://github.com/ruxailab/RUXAILAB/pull/952) | Merged | 2025-07-22 | 2025-07-22 |
| 12 | Chore: Removed deprecated imports and >>> usage | [#953](https://github.com/ruxailab/RUXAILAB/pull/953) | Merged | 2025-07-24 | 2025-07-31 |
| 13 | Chore: Small null value check | [#957](https://github.com/ruxailab/RUXAILAB/pull/957) | Merged | 2025-08-01 | 2025-08-04 |
| 14 | UI layout optimizations and feature enhancements (post-midterm) | [#963](https://github.com/ruxailab/RUXAILAB/pull/963) | Merged | 2025-08-07 | 2025-08-07 |
| 15 | Fix: Improved TemplateInfoDialog in DashboardView and ProfileView | [#964](https://github.com/ruxailab/RUXAILAB/pull/964) | Closed | 2025-08-07 | None |
| 16 | Fix: Heuristics fixes | [#979](https://github.com/ruxailab/RUXAILAB/pull/979) | Merged | 2025-09-15 | 2025-09-15 |
| 17 | Fix: Image upload to storage while answering | [#981](https://github.com/ruxailab/RUXAILAB/pull/981) | Merged | 2025-09-22 | 2025-09-22 |
| 18 | Redesigned loader using new RUXAILAB logo and fixed alignments | [#982](https://github.com/ruxailab/RUXAILAB/pull/982) | Closed | 2025-09-22 | None |
| 19 | Created loader with new RUXAILAB logo | [#983](https://github.com/ruxailab/RUXAILAB/pull/983) | Merged | 2025-09-25 | 2025-09-25 |
| 20 | Feat: Completed next-session card on dashboard | [#988](https://github.com/ruxailab/RUXAILAB/pull/988) | Merged | 2025-09-30 | 2025-10-03 |
| 21 | Fix: Internationalization strings | [#995](https://github.com/ruxailab/RUXAILAB/pull/995) | Merged | 2025-10-06 | 2025-10-17 |
| 22 | Chore: Removed debug logs | [#1000](https://github.com/ruxailab/RUXAILAB/pull/1000) | Merged | 2025-10-08 | 2025-10-13 |
| 23 | Feat: Firebase storage usage calculation | [#1001](https://github.com/ruxailab/RUXAILAB/pull/1001) | Merged | 2025-10-14 | 2025-10-14 |

## Additional Materials
- Figma Designs(created pre GSoC): [Link](https://www.figma.com/design/RTqzPVGMfWuJZMwzqzc6Yc/UI-Layout-for-RUXAILAB?node-id=0-1&t=69M0BjmHgF7LjyTd-1)


## Future Work
- **Add Tests**: I am planning to implement unit and integrated tests for core functionality.
- **Enhance Unmoderated Testing**: Add advanced features like real-time participant feedback and analytics.  
- **Improve Heuristic Evaluation**: Expand heuristic evaluation templates and integrate automated scoring.  
- **Optimize Performance**: Further optimize Vue 3 components for faster rendering and lower resource usage.  
- **Community Contributions**: Continue mentoring new contributors and reviewing PRs to support RUXAILAB’s growth.  

## Conclusion
Participating in GSoC 2025 with RUXAILAB has been a transformative experience. I successfully migrated the codebase to Vue 3, optimized the UI for better usability and accessibility, and implemented new features for unmoderated usability testing and heuristic evaluation. These contributions have enhanced the platform’s functionality and user experience, making it more robust for its users and contributors.

I am deeply grateful to my mentors, Marc Gonzalez Capdevila and Leticia Carvalho Ramos, and the RUXAILAB community for their guidance and support. This project has strengthened my skills in Vue.js, TypeScript, Firebase, and open-source collaboration. I plan to continue contributing to RUXAILAB, refining features, and mentoring new contributors to ensure the platform’s continued success.