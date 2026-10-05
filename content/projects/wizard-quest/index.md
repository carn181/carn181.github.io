+++
title = "Wizard Quest"
date = 2025-02-01T00:00:00Z
period = "Feb 2025"
award = "1st Place in the Game Track at UGAHacks"
summary = "A Pokémon-GO inspired Augmented Reality and Computer Vision web platform that gamifies real-world exploration events, backed by FastAPI & Postgres."
tags = ["Python", "FastAPI", "Postgres", "AR/CV", "UGAHacks"]
+++

### The Concept

Imagine Pokémon-GO, but designed for real-world campus exploration and live event scavenger hunts. **Wizard Quest** was conceived and built during a 36-hour hackathon sprint at **UGAHacks**, where our team set out to combine interactive Augmented Reality (AR) and Computer Vision (CV) into an engaging web application.

[github.com/carn181/ugahacks-11](https://github.com/carn181/ugahacks-11) · [Devpost submission](https://devpost.com/software/wizard-quest) · [Live demo](https://wizard-quest-uga.vercel.app)

[![Wizard Quest demo video](https://img.youtube.com/vi/nheFrOx770I/0.jpg)](https://www.youtube.com/watch?v=nheFrOx770I)

---

### Tech stack

| Layer | Technologies |
|---|---|
| Backend | Python, FastAPI, PostgreSQL/PostGIS, SQLAlchemy |
| Frontend | Next.js, React, TypeScript, Tailwind CSS, Framer Motion |
| AR/CV | AR.js, Three.js, WebXR, computer vision hand tracking |
| Maps | Leaflet |
| Real-time | Socket.io |
| DevOps | Git, Docker, Vercel |

---

### How It Works

1. **Interactive AR/CV Layer:** Players navigate physical locations while the camera interface overlays digital interactive quest objects, using computer vision to detect physical landmarks and validate puzzle completions.
2. **High-Performance Backend:** Built with **Python**, **FastAPI**, and **PostgreSQL** to handle concurrent player check-ins, real-time leaderboard updates, and spatial location queries without lag.
3. **Gamified Quests:** Players solve puzzles, collect virtual items, and complete location-based challenges with immediate feedback.

---

### Hackathon Outcome & Leadership

As technical lead for a team of 3 engineers:
- I architected the FastAPI backend and database schema to guarantee zero-downtime performance during live demos.
- Coordinated git workflows, API contracts, and feature priorities under tight 36-hour constraints.
- **Result:** Wizard Quest won **1st Place in the Game Track at UGAHacks**.
