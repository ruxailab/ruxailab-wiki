# Src Folder Structure

This page explains how the `src` directory is organized in RUXAILAB and where to add new code.

## First-Level Overview

```text
src/
├── main.js
├── ai/
├── app/
├── assets/
├── composables/
├── controllers/
├── features/
├── router/
├── shared/
├── store/
├── ux/
└── views/
```

## First-Level Folder Guide

### `main.js`
Entry point of the Vue app. This is where app bootstrapping starts.

### `ai/`
AI-related modules (for example, transcription and audio sentiment workflows).

### `app/`
Application shell and global app wiring.

### `assets/`
Static resources used by the app (images, JSON data, and templates).

### `composables/`
Global reusable Vue composables (shared hooks/logic).

### `controllers/`
App-level controllers used to coordinate business logic.

### `features/`
Feature-first organization for domain-specific functionality.
Use this location for code specific to one product feature.

### `router/`
Route definitions and navigation setup.

### `shared/`
Cross-cutting reusable code used by multiple features.

### `store/`
Vuex store root and modular store units.

### `ux/`
UX testing domains and flows (Accessibility, Card Sorting, Heuristic evaluation, User Test).

### `views/`
Top-level view pages and route-facing UI screens.

## Where to Add New Code

- If code is specific to one domain, add it under `features/<domain>/`.
- If code is reusable across domains, add it under `shared/`.
- If code belongs to UX methods and test flows, use `ux/`.
- If you are adding global bootstrapping/config, use `app/` or `main.js`.

## Suggested Conventions

- Keep each feature self-contained.
- Move repeated logic into `shared/` or `composables/`.
- Keep routing modular in `router/modules/`.
- Prefer small, focused files per responsibility.

---

If this structure evolves, update this page together with the related refactor so contributors always have an accurate map.
