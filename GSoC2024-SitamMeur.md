---
title: Google Summer of Code 2024 – Eye Tracking Algorithm Optimization Based on Low-Resolution Cameras
contributor: Sitam Meur
github: https://github.com/sitammeur
linkedin: https://www.linkedin.com/in/sitammeur/
project_repo: 
    - https://github.com/ruxailab/eye-tracker-api
    - https://github.com/ruxailab/web-eye-tracker-front
organization: RUXAILAB
program_link: https://summerofcode.withgoogle.com/archive/2024/projects/lEPzZg7S
mentors:
  - Vinicius
  - Marc
  - Karine Pistili
date: 2024-11-11
---

# <img align="center" width="60px" src="https://en.opensuse.org/images/9/91/Gsocsun.png"> GSoC'24 — Eye Tracking Algorithm Optimization Based on Low-Resolution Cameras

This project aims to improve eye-tracking algorithms by exploring new techniques, optimizing existing parameters, and integrating JavaScript enhancements for seamless front-end integration. The main goal is to achieve real-time eye-tracking capabilities. Once the optimization process is complete, the algorithms will be carefully integrated into the project for usability testing, ensuring compatibility and smooth operation within the existing system's framework.

---

## 🌐 Official GSoC Project Page

🔗 [Google Summer of Code 2024 — Web Eye Tracker Project](https://summerofcode.withgoogle.com/archive/2024/projects/lEPzZg7S)

---

## 👨‍💻 Contributor

- **Sitam Meur**
  - **Role:** GSoC Contributor – Student Developer  
    **Education:** Bachelor of Technology in Computer Science, Meghnad Saha Institute of Technology, Kolkata
  - [GitHub Profile](https://github.com/sitamgithub-MSIT)
  - [LinkedIn Profile](https://www.linkedin.com/in/sitammeur/)

---

## 🧑‍🏫 Mentors

- [Vinicius](https://github.com/hvini)
- [Marc](https://github.com/marcgc21)
- [Karine Pistili](https://github.com/KarinePistili)

---

## 🧩 Project Overview

The **Web Eye Tracker** project aims to create an accessible, open-source, and browser-compatible eye tracking tool capable of operating on low-resolution cameras.  
The system enables **gaze tracking, calibration, model selection, and real-time visualization**, enhancing usability testing and research capabilities across diverse devices.

The project was developed in **two major components**:

---

### 1. 🖥️ Backend — `eye-tracker-api`

Repository: [ruxailab/eye-tracker-api](https://github.com/ruxailab/eye-tracker-api)  
Stack: **Flask**, **Python**, **Docker**, **Streamlit**, **Google Cloud Run**

#### Core Responsibilities:

- Implemented multiple **regression models** for gaze prediction:
  - Linear, Ridge, Lasso, Elastic Net, Bayesian Ridge, and SGD Regressor.
- Integrated **model selection and calibration endpoints** for flexible experimentation.
- Built **data preprocessing**, **model persistence**, and **evaluation metric pipelines** (MAE, RMSE, R²).
- Developed a **Streamlit-based visualization tool** for analyzing raw calibration data, metrics, and regression outputs.
- Implemented **logging, testing, and configuration management**.
- **Containerized** the service using Docker for easy deployment on Google Cloud Run.

#### Links:

- 🔗 **Repository:** [eye-tracker-api](https://github.com/ruxailab/eye-tracker-api)
- 🧠 **Commits:** [View all commits by Sitam Meur](https://github.com/ruxailab/eye-tracker-api/commits?author=sitammeur)

---

### 2. 💡 Frontend — `web-eye-tracker-front`

Repository: [ruxailab/web-eye-tracker-front](https://github.com/ruxailab/web-eye-tracker-front)  
Stack: **Vue.js**, **Vuetify**, **TensorFlowJS**, **JavaScript**, **Firebase**

#### Key Deliverables:

- Implemented the **front-end dashboard** to:
  - Manage calibration and gaze prediction sessions.
  - Enable **model selection** and **real-time gaze visualization**.
  - Display regression outputs and metrics dynamically.
- Integrated **TensorFlowJS** for in-browser ML inference.
- Connected front-end with backend via REST API endpoints.
- Improved UI/UX for accessibility and real-time feedback.
- Conducted internal **testing and usability validation** using low-resolution webcams.

#### Links:

- 🔗 **Repository:** [web-eye-tracker-front](https://github.com/ruxailab/web-eye-tracker-front)
- 🧠 **Commits:** [View all commits by Sitam Meur](https://github.com/ruxailab/web-eye-tracker-front/commits?author=sitammeur)

---

## 🗂️ Project Management

| Resource                | Link                                                                                                                               |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 📊 **Project Proposal** | [RUXAILAB GSoC Project Proposal](https://docs.google.com/document/d/1sEEQAt7eaARyVBDsjxo6yLLMRb4i3L66x66YBskdCv4/edit?usp=sharing) |
| 📈 **Progress Sheet**   | [GSoC Progress & Work Log](https://docs.google.com/document/d/1RjCnGjYYgPKvFUrN8hSjPX29aayWr6eEopeCN3QZwEQ/edit?usp=sharing)       |
| 🔄 **Backend PR**       | [PR #26](https://github.com/ruxailab/eye-tracker-api/pull/26)                                                                      |
| 🧠 **Frontend Commits** | [web-eye-tracker-front commits](https://github.com/ruxailab/web-eye-tracker-front/commits?author=sitammeur)                        |

---

## 📚 Documentation & Research Notes

Throughout the project, several technical notes and internal guides were created:

- 🧩 **Model Comparison Report:** Regression, Ensemble, and Neural architectures
- ⚙️ **Hyperparameter Optimization Notes:** Grid Search, Cross-validation, and Bayesian tuning
- 🎛️ **Calibration Study:** Analysis of manual calibration limitations and ML-based improvements
- 🧪 **Testing Notes:** Model performance analysis, overfitting mitigation, and validation logs

---

## 🏁 Outcome

The project successfully delivered a **fully integrated web eye-tracking system**, with modular backend APIs and interactive front-end visualizations.

### Key Achievements:

- ✅ Complete end-to-end integration between backend and frontend.
- ✅ Flexible model selection & evaluation system.
- ✅ Streamlit visualization for calibration and results analysis.
- ✅ Performance testing with real camera input.

---

## 🧠 Technical Highlights

- Addressed **overfitting** in the Y-coordinate regression model via regularization and validation techniques.
- Designed a **modular model interface** allowing seamless switching between multiple regressors.
- Implemented **TensorFlowJS model integration** for live browser inference.
- Conducted **comparative analysis** between traditional regressors and advanced models (MLP, CNN, Mediapipe).
- Proposed **future enhancements** for deep learning–based calibration and head-pose correction.

---

## 🏆 GSoC Summary

| Item             | Description                                                                               |
| ---------------- | ----------------------------------------------------------------------------------------- |
| **Organization** | RUXAILAB                                                                                  |
| **Program**      | Google Summer of Code 2024                                                                |
| **Contributor**  | Sitam Meur                                                                                |
| **Project**      | Eye Tracking Algorithm Optimization Based on Low-Resolution Cameras                       |
| **Technologies** | Python, Javascript, Flask, Vue.js, Scikit-learn, Firebase, Streamlit, Tensorflow.js       |
| **Topics**       | Front-end, Javascript, Eye Tracking, Algorithm Optimization, Artificial Intelligence (AI) |
| **Duration**     | May – August 2024                                                                         |

---

### ✨ Acknowledgements

Special thanks to mentors **Vinicius**, **Marc**, and **Karine Pistili** for their invaluable support and continuous guidance throughout the GSoC journey.

---

## 📚 Useful Links

| Resource                   | Link                                                                                                                               |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 🧩 **Backend Repository**  | [eye-tracker-api](https://github.com/ruxailab/eye-tracker-api)                                                                     |
| 💻 **Frontend Repository** | [web-eye-tracker-front](https://github.com/ruxailab/web-eye-tracker-front)                                                         |
| 📄 **Final PR**            | [#26](https://github.com/ruxailab/eye-tracker-api/pull/26)                                                                         |
| 📊 **Project Proposal**    | [RUXAILAB GSoC Project Proposal](https://docs.google.com/document/d/1sEEQAt7eaARyVBDsjxo6yLLMRb4i3L66x66YBskdCv4/edit?usp=sharing) |
| 📈 **Progress Sheet**      | [GSoC Progress & Work Log](https://docs.google.com/document/d/1RjCnGjYYgPKvFUrN8hSjPX29aayWr6eEopeCN3QZwEQ/edit?usp=sharing)       |

---

**Submitted as part of Google Summer of Code 2024 – Final Work Proof**  
© 2024 RUXAILAB • Developed by Sitam Meur
