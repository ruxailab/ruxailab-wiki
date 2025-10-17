---
title: Google Summer of Code 2025 – Transcription API
contributor: Basma Elhoseny
github: https://github.com/basmaelhoseny01
project_repo: https://github.com/ruxailab/transcription-api
organization: RUXAILAB
program_link: https://summerofcode.withgoogle.com/programs/2025/projects/aOHlFhUA
mentors:
  - Marc
  - Karine Pistili
date: 2025-09-04
---

# <img align="center" width="60px" src="https://en.opensuse.org/images/9/91/Gsocsun.png"> GSoC'25 — Transcription Tool for Usability Testing

This repository and its companion front-end integration are part of the **Google Summer of Code (GSoC) 2025** program with **RUXAI Lab**.  
The project focuses on building an **end-to-end Speech-to-Text (Transcription) Tool** — combining a scalable **FastAPI backend** with a **Vue-based RUXAILAB front-end integration** for managing audio transcription sessions.

---

## 🌐 Official GSoC Project Page
🔗 [Google Summer of Code 2025 — Transcription Tool for Usability Testing](https://summerofcode.withgoogle.com/programs/2025/projects/aOHlFhUA)

## 👩‍💻 Contributor

- **Basma Elhoseny**
  - **Role:** GSoC Contributor – Full-Stack (AI/Software Engineer)  
    **Education:** MSc Student in Data Analytics & Business Intelligence,  
    B.Sc. in Computer Engineering, **Cairo University (Class of 2024, Faculty of Engineering)**
  - [GitHub Profile](https://github.com/BasmaElhoseny01)
  - [LinkedIn Profile](https://www.linkedin.com/in/basmaelhoseny01/)

## 🧑‍🏫 Mentors

- [Karine Pistili](https://github.com/KarinePistili)
- [Marc](https://github.com/marcgc21)

## 🧩 Project Overview

The project was divided into **two main components**:

### 1. 🖥️ Backend — `transcription-api`

Repository: [ruxailab/transcription-api](https://github.com/ruxailab/transcription-api)  
Stack: **FastAPI**, **Python**, **Docker**, **Google Cloud Run**, **L4 GPU**

#### Core Responsibilities:

- Implemented the **speech-to-text API service** supporting multiple providers and models (OpenAI Whisper, etc.)
- Designed modular architecture with **provider/model selection**, **audio upload endpoints**, and **transcription session storage**
- Configured **environment variables** and **.env.example** for deployment reproducibility
- Deployed on **Google Cloud Run** with GPU support and regional configuration via Artifact Registry
- Set up internal **logging, monitoring, and health endpoints**
- Wrote detailed **deployment README** and workflow documentation

#### Links:

- 🔗 **Repository:** [transcription-api](https://github.com/ruxailab/transcription-api)
- ☁️ **Deployment:** Deployed via Google Cloud Run (GPU-enabled)
- 📄 **Backend README:** [View detailed setup](https://github.com/ruxailab/transcription-api#readme)

---

### 2. 💡 Frontend — Integration in RUXAILAB

Main Pull Request: [PR #992 – Transcription Tool Integration](https://github.com/ruxailab/RUXAILAB/pull/992)  
Stack: **Vue 3**, **Vuetify**, **JavaScript**, **Google Cloud Storage Integration**

#### Key Deliverables:

- Built a complete **Transcription Dashboard UI**
  - Upload and manage audio files
  - Select transcription provider & model
  - Display session analytics and metadata
  - Support for exporting results (PDF / CSV / JSON)
- Added **audio player** and **progress visualization**
- Integrated with the backend API for transcription creation and retrieval
- Followed componentized and responsive **Vuetify design patterns**
- Conducted internal **usability testing & UX validation**

---

## 🚀 Deployment

- **Backend:** Deployed using **Google Cloud Run** with GPU (L4)  
  → Automated build & deploy via Docker + Artifact Registry
- **Frontend:** Integrated into the main RUXAILAB web app and tested in staging environment

---

## 🗂️ Project Management

| Resource                          | Link                                                                                                                         |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 📊 **Project Board**              | [RUXAILAB GSoC Project Board](https://github.com/orgs/ruxailab/projects/8)                                                   |
| 📈 **Progress & Follow-Up Sheet** | [Google Sheet Tracker](https://docs.google.com/spreadsheets/d/1HA2vLJVuLwRmoyf-CYkFvIwXJUXrbbyQ9kxCkDbqpwU/edit?usp=sharing) |
| 🔄 **Frontend PR**                | [PR #992](https://github.com/ruxailab/RUXAILAB/pull/992)                                                                     |
| 🧠 **Backend Repo**               | [transcription-api](https://github.com/ruxailab/transcription-api)                                                           |

---

## 🧾 Documentation & Study Notes

Throughout the project, I created several internal guides and study resources to support the integration process:

- 🗃️ **Deployment Study Guide:** Cloud Run & GPU deployment configuration
- 🎙️ **Speech-to-Text Tools Survey:** Comparison between Whisper, Google Speech API, and Deepgram
- 🧩 **Vue & Vuetify Study Guide:** UI framework notes and reusable component patterns
- 🧪 **Testing Plan:** API tests, UX usability test logs, and manual QA notes

---

## 🏁 Outcome

The project successfully delivered a **fully working transcription pipeline**:

- Backend API deployed and containerized
- Front-end integration within RUXAILAB app
- Documented deployment pipeline, environment setup, and testing workflow
- Conducted UX testing and finalized end-user flow

---

## 🏆 GSoC Summary

| Item             | Description                                                |
| ---------------- | ---------------------------------------------------------- |
| **Organization** | RUXAI Lab                                                  |
| **Program**      | Google Summer of Code 2025                                 |
| **Contributor**  | Basma Elhoseny                                             |
| **Project**      | Transcription Tool (Speech-to-Text Pipeline & Integration) |
| **Main Outputs** | Backend API (FastAPI) + Frontend UI (Vue / Vuetify)        |
| **Duration**     | May – October 2025                                         |

---

### ✨ Acknowledgements

Special thanks to my mentors **Karine** and **Marc** for their continuous support and guidance throughout the GSoC journey.

---

## 📚 Useful Links

| Resource                  | Link                                                                                                                         |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 🧩 **Backend Repository** | [transcription-api](https://github.com/ruxailab/transcription-api)                                                           |
| 💻 **Frontend PR**        | [RUXAILAB #992](https://github.com/ruxailab/RUXAILAB/pull/992)                                                               |
| 📊 **Project Board**      | [RUXAILAB Project #8](https://github.com/orgs/ruxailab/projects/8)                                                           |
| 📈 **Progress Sheet**     | [Google Sheet Tracker](https://docs.google.com/spreadsheets/d/1HA2vLJVuLwRmoyf-CYkFvIwXJUXrbbyQ9kxCkDbqpwU/edit?usp=sharing) |

---

**Submitted as part of Google Summer of Code 2025 – Final Work Proof**  
© 2025 RUXAILab • Developed by Basma Elhoseny
