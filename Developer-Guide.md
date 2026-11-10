# RUXAILAB Developer Guide

This guide is for contributors developing the RUXAILAB application in the
[main code repository](https://github.com/ruxailab/RUXAILAB). It complements the
repository's [README](https://github.com/ruxailab/RUXAILAB/blob/develop/README.md)
and [contribution guidelines](https://github.com/ruxailab/RUXAILAB/blob/develop/CONTRIBUTING.md)
with a map of the codebase and common development workflows.

## Prerequisites

- Node.js 24 for local development.
- Node.js 24 for the Firebase Cloud Functions project.
- npm and Git.
- A Firebase project, or the Firebase Emulator Suite for local development.

Some optional integrations require separate services. Their URLs and setup
requirements are described in the main repository's README.

## Set up the workspace

Clone the code repository and install dependencies for the frontend and
Cloud Functions separately:

```bash
git clone https://github.com/ruxailab/RUXAILAB.git
cd RUXAILAB
npm ci
cd functions
npm ci
cd ..
```

Create the frontend environment file and add the configuration needed for your
setup:

```bash
cp .env.example .env
```

The frontend reads its Firebase, emulator, localization, and integration
settings from the root environment files. Cloud Functions have separate
settings, loaded from `functions/.env` and, when selected by the command,
another environment file such as `functions/.env.develop`. Use
`functions/.env.example` as the template for the variables you need. Keep
credentials and other private values out of commits.

Start the frontend development server:

```bash
npm run serve
```

If the frontend is configured to use Firebase emulators, start the needed
emulators as well. Ports and emulator options are configured in the root
`firebase.json` and `.env.example`. The Docker Compose setup is another option;
it exposes the app at `http://localhost:8080` and the Emulator UI at
`http://localhost:4000`.

## Codebase map

| Path | Responsibility |
| ---- | -------------- |
| `src/main.js` | Creates the Vue app and installs the router, Vuex store, Vuetify, i18n, and shared plugins. |
| `src/app/` | Application shell, global layouts, plugins, Firebase setup, router, and app-level services. |
| `src/router/modules/` | Shared route groups, including public and administrative routes. |
| `src/ux/` | Feature modules for `CardSorting`, `FocusGroup`, `Heuristic`, `UserTest`, and `accessibility`. |
| `src/shared/` | Shared components, controllers, composables, models, services, store modules, utilities, and views. |
| `src/store/` | Vuex store and its modules. |
| `src/ai/` | AI-related functionality such as study generation, transcription, and sentiment analysis. |
| `functions/index.js` | Firebase Cloud Functions entry point. |
| `functions/src/` | Server-side code organized into features, HTTP handlers, triggers, scheduled tasks, repositories, shared code, and utilities. |
| `tests/unit/` | Frontend unit tests. |
| `tests/rules/` | Firebase security-rules tests. |
| `functions/tests/` | Cloud Functions tests. |
| `firestore.rules`, `database.rules.json`, `storage.rules` | Firebase security rules for their respective services. |

Study-method-specific screens, routes, state, and logic generally belong in
that method's `src/ux/<Method>/` module. Reuse shared code from `src/shared/`
when it is genuinely common to multiple features. When adding a study method,
follow the [study-method implementation guide](https://github.com/ruxailab/RUXAILAB/blob/develop/docs/adding-a-study-method.md)
and the [activity-logging guide](logging) where applicable.

## Common development commands

Run commands from the repository root unless noted otherwise.

| Command | What it checks or starts |
| ------- | ------------------------ |
| `npm run serve` | Frontend development server. |
| `npm test` | Frontend unit tests. |
| `npm run test:rules` | Security-rules tests using Firebase emulators. |
| `npm run lint` | ESLint for frontend source in `src/`. |
| `npm run lint:fix` | Automatically fixes supported frontend lint issues. |
| `npm run build:dev` | Development build. |
| `npm run build:prod` | Production build. |
| `npm --prefix functions run serve:dev` | Cloud Functions emulator using the development environment configuration. |
| `npm --prefix functions test` | Cloud Functions tests. |
| `npm --prefix functions run lint` | ESLint for Cloud Functions. |

Run the relevant checks for the files you changed. Changes to Firebase access
rules should include the corresponding rules tests; changes to a Cloud
Function should include its tests and lint check.

## Implementation notes

### Routes and access control

Application routes are assembled in `src/app/router/index.js` from shared
route modules and the feature routers under `src/ux/`. Preserve the route
authorization metadata and access checks when adding or changing routes.
Study-specific access rules are not interchangeable with global user-role
checks; consult the existing route patterns and add tests for access changes.

### Firebase and data access

The client uses Firebase services configured under `src/app/plugins/firebase/`.
Server-side operations live in Cloud Functions. Keep frontend and server
configuration separate, and update the applicable Firestore, Realtime Database,
or Storage rules when a change alters data access. Prefer testing rule changes
with the Firebase Emulator Suite rather than a live project.

### Localization and commits

Follow the existing locale-file patterns when adding user-facing strings. The
pre-commit hook runs `i18n-diff-guard.mjs`, `npm run test`, and `lint-staged`;
the latter applies the configured lint and formatting checks to staged
frontend files.

## Contribution workflow

The main repository's contribution guide has the complete workflow. In brief:

1. Branch from `develop` and create a focused feature or fix branch.
2. Follow the patterns in the relevant feature module and keep changes scoped.
3. Add or update tests and documentation affected by the change.
4. Run the relevant checks before committing.
5. Open a pull request targeting `develop` with a clear description and any
   related issue.

For the system structure and methodology references, see the
[architecture overview](Architecture) and
[study methodologies](Study-Methodologies). For module-specific developer
documentation, see the [Focus Group guide](focusgroups),
[Focus Group analysis guide](analysis), and
[study activity logging guide](logging).
