---
title: "Google Summer of Code 2025 - Disgitbot: GitHub-Discord Integration Platform"
contributor: Tianqin Meng
github: https://github.com/tqmsh
project_repo: https://github.com/ruxailab/disgitbot
organization: RUXAILAB
program_link: https://summerofcode.withgoogle.com/programs/2025/projects/gZbjuWuX
mentors:
  - Marc Gonzalez Capdevila
  - Karine Pistili Rodrigues
  - Julio Manoel
---

# GSoC 2025 - Disgitbot: GitHub-Discord Integration Platform

**Repository:** [disgitbot](https://github.com/ruxailab/disgitbot)  
**Try the bot:** [RUXAILAB Discord Server](https://discord.gg/VAxzZxVV)  
**Student:** Tianqin Meng ([@tqmsh](https://github.com/tqmsh))  
**Organization:** Uramaki LAB  
**Project:** [Integration of GitHub Actions with Discord Role Management](https://summerofcode.withgoogle.com/programs/2025/projects/gZbjuWuX)

## Project Objectives

The Disgitbot project creates a comprehensive Discord bot that integrates GitHub activity with Discord communities. The main goals were to:

- Provide real-time GitHub contribution notifications in Discord
- Automate role assignment based on contribution metrics  
- Enable AI-powered PR review and labeling
- Create analytics dashboards for community engagement
- Streamline development workflows through intelligent automation

## Project Description

Disgitbot transforms Discord servers into live GitHub activity dashboards. Users make pull requests and automatically get roles. The bot tracks every PR, issue, and commit across repositories, updating Discord roles automatically and using AI to label and review PRs.

**The Problem**: Managing GitHub contributions across Discord communities is messy. People manually assign roles, forget to label PRs, and lose track of who's contributing what. Teams waste time on administrative tasks instead of building software.

**The Solution**: Disgitbot automates everything. It tracks your GitHub activity, updates Discord roles automatically, uses AI to label and review PRs, and shows real-time analytics.

## Project Structure

The project consists of two main components:

### Discord Bot (`disgitbot`)
- **Repository:** [ruxailab/disgitbot](https://github.com/ruxailab/disgitbot)
- **Tech Stack:** Python, Discord.py, Google Cloud Run, GitHub API
- **Deployment:** [Discord Bot Setup Guide](https://github.com/ruxailab/disgitbot/blob/main/discord_bot/README.md)

### Core Features
1. **Contribution Tracking** - Real-time GitHub activity monitoring
2. **Smart Role Assignment** - Automatic role updates based on contribution levels
3. **AI Code Review** - Google Gemini API integration for PR analysis
4. **Consistent Labeling** - Automated PR labeling system
5. **Live Metrics** - Real-time repository statistics in Discord channels
6. **Analytics Dashboard** - Contributor activity visualization and leaderboards

## How It Works

Your Discord server becomes a live dashboard of your GitHub activity. Make a pull request, get a role. Open 50 PRs, get a better role. The bot watches everything and updates your community automatically.

AI analyzes every PR and assigns labels and reviewers. No more guessing what category a change belongs to or who should review it.

## Six Major Features

### Contribution Tracking
Run `/show-stats` to see your GitHub activity. The bot tracks every PR, issue, and commit across all repositories. Daily updates through GitHub Actions keep everything current.

### Smart Role Assignment
First PR gets you "🌸 1+ PRs". Hit 51 PRs and become "🌹 51+ PRs". The system recalculates nightly and updates everyone's roles automatically. Top three contributors get special medals.

### AI Code Review
Google's Gemini AI reads your PR title, description, and code changes. It predicts the right labels and assigns reviewers from your top contributors. No more manual categorization.

### Consistent Labeling
The bot learns your repository's label structure and applies them consistently. Every PR gets properly categorized without human intervention.

### Live Metrics
Discord voice channels show real-time stats: "Stars: 1,234", "Forks: 567", "Contributors: 89". All your repositories combined into one dashboard.

### Analytics Dashboard
Charts show contributor activity over time. Compare team performance, spot trends, and see who's leading in different categories. Daily, weekly, monthly, and all-time leaderboards.

## How We Built It

**Data Pipeline**: GitHub Actions runs daily to collect repository data, process contributions, and update Discord. Handles rate limits and scales to hundreds of repositories.

**AI Layer**: Gemini API analyzes code changes and makes labeling decisions. Gets smarter over time by learning your repository patterns.

**Cloud Infrastructure**: Google Cloud Run with pay-per-request billing. Throttles resources during low activity, keeping costs low.

## Results

After deployment, teams would see faster PR reviews, higher contributor engagement, better project visibility, and less time spent on admin tasks.

## Try It Yourself

**Demo**: [RUXAILAB Discord Server](https://discord.gg/VAxzZxVV)  
**Code**: [GitHub Repository](https://github.com/ruxailab/disgitbot)  
**Deploy**: [Setup Guide](https://github.com/ruxailab/disgitbot/blob/main/discord_bot/README.md)

Everything is open source and ready to use.

## What's Next

The architecture supports easy extensions: project management integrations, advanced AI analysis, custom dashboards, and CI/CD pipeline connections.

This project shows how AI can solve real developer problems beyond just generating code. It automates the boring stuff so teams can focus on building great software.

Thanks to the RUXAILAB mentors and GSoC 2025 program for making this possible.

## Pull Requests

This is a separate repository with no direct pull requests to the main RUXAILAB organization. All development work was completed within the [disgitbot repository](https://github.com/ruxailab/disgitbot).

## Deliverables

### Completed Features
- Discord bot with OAuth GitHub account linking
- Automated role assignment system (Novice to Expert levels)  
- AI-powered PR review using Google Gemini API
- Real-time analytics and live metrics display
- Contribution tracking with daily GitHub Actions workflows
- Hall of Fame visualization system
- Repository metrics tracking (stars, forks, contributors)
- Cloud deployment on Google Cloud Run

### Implementation Details
- **Data Pipeline:** GitHub Actions runs daily to collect repository data and update Discord
- **AI Layer:** Gemini API analyzes code changes and makes labeling decisions  
- **Cloud Infrastructure:** Google Cloud Run with pay-per-request billing
- **Database:** Firestore for storing contribution data and analytics

## Additional Materials Created During GSoC

- **Project Documentation:** [Complete README](https://github.com/ruxailab/disgitbot/blob/main/README.md)
- **Setup Guide:** [Discord Bot Deployment Guide](https://github.com/ruxailab/disgitbot/blob/main/discord_bot/README.md)
- **Implementation Diagrams:** Mermaid diagrams showing system architecture
- **Timeline & Tasks:** Detailed project timeline with completed milestones
- **Gallery:** Screenshots demonstrating all implemented features
- **Live Demo:** [RUXAILAB Discord Server](https://discord.gg/VAxzZxVV)

**Submitted as part of Google Summer of Code 2025 – Final Work Proof**  
© 2025 RUXAILab • Developed by Tianqin Meng