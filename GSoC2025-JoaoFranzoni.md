# <img align="center" width="60px" src="https://en.opensuse.org/images/9/91/Gsocsun.png"> GSoC 2025 - Final Work Report: Improving User Testing with Eye Tracking, Sentiment Analysis & Pre/Post Tasks

## Contributor Info

- **Name:** João Franzoni  
- **Organization:** [RUXAILAB](https://github.com/ruxailab)  
- **Email:** [joaofranzoni0@gmail.com](mailto:joaofranzoni0@gmail.com)  
- **GitHub:** [joaofranzoni](https://github.com/joaofranzoni)  
- **Country:** Brazil

## Mentors' Info

- **Mentor:** [Marc Gonzalez Capdevila](https://github.com/marcgc21)  
- **Mentor:** [Julio Manoel](https://github.com/JulioManoel)

## Project Details

### Project Title
Improving User Testing with Eye Tracking, Sentiment Analysis & Pre/Post Tasks

### GSoC Project Page
- [GSoC 2025 with RUXAILAB](https://summerofcode.withgoogle.com/programs/2025/projects/KrpA8CbI)

### Project Summary
This project enhanced RUXAILAB, an open-source platform for usability evaluation, by integrating three major components:

1. **Eye Tracking** – Affordable, webcam-based gaze tracking for real-time attention visualization (heatmaps, gaze paths).  
2. **Sentiment Analysis** – Multimodal detection using facial expression recognition and NLP to infer user emotions during tests.  
3. **Pre/Post-Test Tasks** – Configurable forms for evaluating usability (SUS, NASA-TLX) and cognitive load, before and after experiments.

These integrations allow richer, data-driven usability testing with combined qualitative and quantitative insights. The system was built using a modular, API-first, and user-centered approach, including support for real-time analytics and integration with RUXAILAB workflows.

### Project Technologies
- **Programming:** Python, JavaScript  
- **Frameworks:** Flask, Vue.js, Vuetify  
- **Machine Learning:** PyTorch  
- **Deployment & DevOps:** Docker, Firebase  
- **Topics:** Machine Learning, Eye Tracking, Sentiment Analysis, UX Research, HCI, Usability Testing  

---

## Work Summary

### 1. Eye Tracking Module
Developed a full eye-tracking system with:

- Real-time iris detection and gaze estimation  
- Heatmaps and gaze path overlays on test interfaces  
- Calibration interface as standalone and integrated with RUXAILAB  
- Streaming gaze data to analytics dashboards  
- **Key PRs:**
  - [Eye Tracking Module - Full Capture, Calibration & Real-Time Visualization Integration #951](https://github.com/ruxailab/RUXAILAB/pull/951)  
  - [Eye-Tracking Calibration Interface – Standalone & RUXAILAB Integration #82](https://github.com/ruxailab/web-eye-tracker-front/pull/82)  
  - [Update and Simplification of Gaze Tracking Prediction Pipeline #41](https://github.com/ruxailab/eye-tracker-api/pull/41)

---

### 2. Sentiment Analysis Integration
- Facial sentiment detection using ML models deployed via API  
- Integrated with RUXAILAB to capture user emotions during tasks  
- Optimized pipelines to reduce latency and improve accuracy  
- **Key PRs:**
  - [Facial Sentiment Analysis Integration and Visualization #1007](https://github.com/ruxailab/RUXAILAB/pull/1007)  
  - [Facial Sentiment Optimization and RuxaiLab Integration #1](https://github.com/ruxailab/facial-sentiment-analysis-api/pull/1)  
  - [Fix Audio Sentiment Analysis to the new structure of tests and enhance UX #1005](https://github.com/ruxailab/RUXAILAB/pull/1005)

---

### 3. Pre/Post-Test Task Forms
- Implemented customizable forms for SUS, NASA-TLX  
- Enabled integration with session analytics

---

### 4. Docker & Backend Improvements
- Standardized API endpoints for batch predictions and gaze tracking  
- Simplified deployment via Docker for reproducibility  
- Optimized data pipelines for eye tracking and sentiment analysis  

---

### 5. Contributions & Commits
- **Total PRs submitted:** 6 major PRs for core functionalities  
- **Commits on main RUXAILAB repository:** +866 commits  
- **Notable Work:** End-to-end integration of new modules, API-first architecture, and real-time analytics

---

## Pull Requests Summary

| PR Title | Repository | Link |
|----------|-----------|------|
| [GSOC-25] Facial Sentiment Analysis Integration and Visualization | RUXAILAB | [#1007](https://github.com/ruxailab/RUXAILAB/pull/1007) |
| [GSOC-25] Fix Audio Sentiment Analysis & Enhance UX | RUXAILAB | [#1005](https://github.com/ruxailab/RUXAILAB/pull/1005) |
| [GSOC-25] Eye Tracking Module - Full Capture, Calibration & Real-Time Visualization Integration | RUXAILAB | [#951](https://github.com/ruxailab/RUXAILAB/pull/951) |
| [GSOC-25] Eye-Tracking Calibration Interface – Standalone & RUXAILAB Integration | Web Eye Tracker Front | [#82](https://github.com/ruxailab/web-eye-tracker-front/pull/82) |
| [GSOC-25] Update and Simplification of Gaze Tracking Prediction Pipeline | Eye Tracker API | [#41](https://github.com/ruxailab/eye-tracker-api/pull/41) |
| [GSOC-25] Facial Sentiment Optimization and RuxaiLab Integration | Facial Sentiment Analysis API | [#1](https://github.com/ruxailab/facial-sentiment-analysis-api/pull/1) |

## Repositories Summary

| Repository | Link |
|-----------|------|
| RUXAILAB | [RUXAILAB ](https://github.com/ruxailab/RUXAILAB) |
| Web-eye-tracker-front | [web-eye-tracker-front](https://github.com/ruxailab/web-eye-tracker-front) |
| Eye-tracker-api | [eye-tracker-api](https://github.com/ruxailab/eye-tracker-api) |
| Facial-sentiment-analysis-api | [facial-sentiment-analysis-api](https://github.com/ruxailab/facial-sentiment-analysis-api) |

---

## Results & Achievements
- Complete integration of eye tracking and sentiment analysis into RUXAILAB  
- Real-time visualization of gaze and emotional metrics  
- Modular and scalable architecture enabling future feature additions  
- Open-source contributions with +866 commits to RUXAILAB  

---

## Future Work
- Additional metrics for cognitive load  
- Enhanced AI models for sentiment analysis and gaze prediction   
- Enhanced Methods of analysis with Facial, Eyes and Audio data gathered

---

## Conclusion

My GSoC 2025 project was an incredible journey and a complete success. Over the past months, I had the opportunity to work on something that challenged me in every possible way, integrating multiple AI models, each designed for a different purpose and type of media, and turning all of that into structured, meaningful data for UX analysis. Making eye tracking, sentiment analysis, and pre/post-test tasks work together in harmony was not only technically demanding but also deeply rewarding.  

Throughout this process, I grew a lot as a developer. I learned how to deal with complex architectures, connect different repositories and APIs, and find creative solutions when things didn’t go as planned. More than just coding, this experience taught me how to be patient, persistent, and collaborative — skills that I’ll carry for the rest of my career.  

I’m also really thankful for the RUXAILAB community. Working with contributors from so many different countries and cultures was inspiring and made me realize how powerful open source collaboration can be. And of course, I want to thank my mentors, Marc, Julio and Karine, who were my light when I felt lost or stuck. Their guidance and trust made all the difference, without them, this project would not have been the success it became.
