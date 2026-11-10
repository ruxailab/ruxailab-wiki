<div align="center">
  <h1>Welcome to RUXAILAB</h1>
  <p>An open-source platform for user research, usability testing, and accessibility evaluation.</p>
</div>

## About

RUXAILAB helps researchers plan studies, collect participant feedback, and
analyze usability and user experience. The application includes Card Sorting,
Focus Group, Heuristic Evaluation, and User Testing modules. An accessibility
module is also under development; its study category is currently marked as
coming soon.

The application is built with Vue 3 and Vuetify and uses Firebase
Authentication, Cloud Firestore, Realtime Database, Cloud Storage, and Cloud
Functions. Optional integrations provide services such as eye tracking,
transcription, sentiment analysis, PDF generation, and video calls.

## Explore the documentation

- [Developer Guide](Developer-Guide) — setup, project layout, and common commands.
- [Architecture](Architecture) — application, Firebase, and access-control diagrams.
- [Study methodologies](Study-Methodologies) — method selection and workflows.
- [Focus Group developer guide](focusgroups)
- [Focus Group analysis guide](analysis)
- [Study activity logging guide](logging)

## Run RUXAILAB locally

### Prerequisites

- Node.js `>=22.22.1` for the main application.
- npm and Git.
- A Firebase project, or the Firebase Emulator Suite.
- Python 3.11.8 is listed in the contribution guide; Cloud Functions use Node.js 24.

### Install and configure

```bash
git clone https://github.com/ruxailab/RUXAILAB.git
cd RUXAILAB
npm install
cp .env.example .env
```

Set the Firebase and other environment values required for your setup in
`.env`. For local emulator development, configure the emulator flags and ports
in `.env` using `.env.example`, then start the configured Firebase emulators
from the repository root:

```bash
firebase emulators:start
```

Start the application:

```bash
npm run serve
```

The development server prints the local application URL. Do not commit `.env`
files, API keys, or private credentials.

For the Docker-based emulator setup, see the
[contribution guide](https://github.com/ruxailab/RUXAILAB/blob/develop/CONTRIBUTING.md);
it exposes the app at `http://localhost:8080` and Firebase Emulator UI at
`http://localhost:4000`.

### Cloud Functions

Cloud Functions are a separate npm project and require Node.js 24. If you are
working on them, install their dependencies and configure their environment
separately:

```bash
cd functions
npm install
cp .env.example .env
```

Use `functions/.env.example` for server-side configuration. Never put server
secrets in frontend `VUE_APP_*` variables.

## Useful checks

Run from the repository root:

| Command | Purpose |
| ------- | ------- |
| `npm test` | Run frontend unit tests. |
| `npm run test:rules` | Run Firebase security-rules tests with emulators. |
| `npm run lint` | Lint frontend source. |
| `npm run build:dev` | Create a development build. |
| `npm run build:prod` | Create a production build. |
| `npm --prefix functions test` | Run Cloud Functions tests. |
| `npm --prefix functions run lint` | Lint Cloud Functions. |

Use the relevant checks for the code you change. Avoid deploying to a shared
Firebase project unless you have verified the active project and have
authorization to deploy.

## Contribute and get help

Read the [contribution guidelines](https://github.com/ruxailab/RUXAILAB/blob/develop/CONTRIBUTING.md)
before opening a pull request.

- [Report a bug](https://github.com/ruxailab/RUXAILAB/issues/new?template=bug.yml)
- [Request a feature](https://github.com/ruxailab/RUXAILAB/issues/new?template=feature.yml)
- [Ask a question in GitHub Discussions](https://github.com/ruxailab/RUXAILAB/discussions)
- [RUXAILAB Discord](https://discord.com/channels/1209902463239593984/1209902463713288293)

RUXAILAB is distributed under the [MIT License](https://github.com/ruxailab/RUXAILAB/blob/develop/LICENSE).
