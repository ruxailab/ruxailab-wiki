---
title: Google Summer of Code 2024 – Sentiment Analysis for Moderated Usability Tests (Audio)
contributor: Basma Elhoseny
github: https://github.com/BasmaElhoseny01
project_repo:
  - https://github.com/ruxailab/sentiment-analysis-api
  - https://github.com/ruxailab/RUXAILAB
organization: RUXAILAB
program_link: https://summerofcode.withgoogle.com/programs/2024/projects/V469U9cf
mentors:
  - Karine Pistili
  - Marc
  - Vinícius Cavalcanti
date: 2024-08-17
---

# <img align="center" width="60px" src="https://en.opensuse.org/images/9/91/Gsocsun.png"> GSoC'24 — Sentiment Analysis for Moderated Usability Tests (Audio)

This project introduces **audio-based sentiment analysis** for moderated usability tests within the RUXAILAB ecosystem. The goal is to enrich usability evaluation by combining **speech transcription** and **sentiment classification**, allowing moderators to better understand users’ emotional responses during test sessions.

---

## 🌐 Official GSoC Project Page

🔗 [Data Extraction for Sentiment Analysis from Usability Tests](https://summerofcode.withgoogle.com/programs/2024/projects/V469U9cf)

---

## 👩‍💻 Contributor

- **Basma Elhoseny**
  - **Role:** GSoC Contributor – Student Developer
  - [GitHub Profile](https://github.com/BasmaElhoseny01)

---

## 🧑‍🏫 Mentors

- [Karine Pistili](https://github.com/KarinePistili)
- [Marc](https://github.com/marcgc21)
- [Vinícius Cavalcanti](https://github.com/hvini)

---

## 🧩 Project Overview

The project focuses on extending RUXAILAB with **Sentiment Analysis for Moderated Usability Tests**, specifically targeting **audio-based evaluations**.

It enables moderators and researchers to:

- Analyze **emotional sentiment** (Positive, Neutral, Negative) from user speech.
- Associate sentiment results with **specific audio regions**.
- Combine **transcriptions and sentiment insights** to better understand user experience during usability tests.

The solution integrates directly with the **Sentiment Analysis API**, developed as part of GSoC 2024.

---

## 🏗️ Architecture Overview

The solution is composed of two tightly integrated parts:

---

### 1. 🧠 Backend — `sentiment-analysis-api`

Repository: [ruxailab/sentiment-analysis-api](https://github.com/ruxailab/sentiment-analysis-api)  
Stack: **Python**, **Flask**, **Whisper**, **RoBERTa**, **PyTorch**, **Docker**

#### Core Features:

- Audio extraction from video and audio files.
- Speech transcription using **Whisper**.
- Sentiment classification using **RoBERTa**.
- Timestamp-based sentiment analysis per audio segment.
- REST API with full documentation and test coverage.
- Docker and Docker Compose support.

---

### 2. 💡 Frontend Integration — `RUXAILAB`

Repository: [ruxailab/RUXAILAB](https://github.com/ruxailab/RUXAILAB)  
Stack: **Vue.js**, **Vuetify**, **JavaScript**, **Firebase**, **WaveSurfer.js**

#### Key Deliverables:

- **Audio Sentiment Tab** integrated into moderated test answers.
- Interactive **audio waveform visualization** with region-based sentiment analysis.
- Playback controls (speed and volume).
- Display of transcriptions mapped to sentiment per audio region.
- Improved Firestore querying with multi-condition support.

---

## 🛠️ Main Contributions

- 🎙️ Implementation of **Sentiment Analysis for Moderated Usability Tests (Audio)**.
- 🧩 Integration with the **Sentiment Analysis API**.
- 🗂️ Creation of new models, controllers, views, and UI components.
- 🔎 Improved Firestore querying via reusable multi-condition queries.
- 🎨 Enhanced UX for moderators through intuitive audio visualization.

---

## 🔧 Technologies & Tools

- **Frontend:** JavaScript, Vue.js, Vuetify, Firebase, WaveSurfer.js  
- **Backend:** Python, Flask, Whisper, RoBERTa, PyTorch  
- **DevOps:** Docker, Docker Compose  

---

## 🔄 Pull Requests

The following pull requests were created as part of the GSoC period:

- 🔗 **[Sentiment Analysis integration into RUXAILAB #533](https://github.com/ruxailab/RUXAILAB/pull/533)**

---

## 🏁 Outcome

The project successfully delivered a **complete audio sentiment analysis workflow**, allowing RUXAILAB to support deeper emotional insights during moderated usability tests.

### Key Results:

- ✅ Audio region-based sentiment analysis.
- ✅ Seamless backend–frontend integration.
- ✅ Improved moderator experience with rich visual feedback.
- ✅ Scalable architecture for future sentiment-related features.

---

## 🏆 GSoC Summary

| Item             | Description                                                     |
| ---------------- | --------------------------------------------------------------- |
| **Organization** | RUXAILAB                                                        |
| **Program**      | Google Summer of Code 2024                                      |
| **Contributor**  | Basma Elhoseny                                                  |
| **Project**      | Sentiment Analysis for Moderated Usability Tests (Audio)       |
| **Technologies** | Python, Vue.js, Firebase, Whisper, RoBERTa, Docker              |
| **Topics**       | Sentiment Analysis, UX Research, Audio Processing, AI          |
| **Duration**     | May – August 2024                                               |

---

### ✨ Acknowledgements

Special thanks to mentors **Karine Pistili**, **Marc**, and **Vinícius Cavalcanti** for their guidance, feedback, and continuous support throughout the GSoC journey.

---

**Submitted as part of Google Summer of Code 2024 – Final Work Proof**  
© 2024 RUXAILAB • Developed by Basma Elhoseny
