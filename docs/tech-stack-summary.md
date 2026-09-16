# Tech Stack Summary - FitFlow Redesign

## 1. Overview
This document outlines the selected technology stack for the **FitFlow Redesign** project, addressing key pain points identified during human-centered design research (user retention drop, high friction in nutrition/workout logging, lack of social accountability).

## 2. Selected Technology Stack
* **Frontend:** React Native (Cross-platform iOS & Android mobile application with On-Device ML via TensorFlow Lite)
* **Backend:** Spring Boot (Java RESTful Web APIs & Native AI Recommendation Engine)
* **Database:** MongoDB (NoSQL document store for flexible user data, workout logs, and nutrition records)
* **Authentication:** Firebase Auth / OAuth2 with JWT tokens

## 3. Rationale & Justification
- **React Native:** Allows rapid cross-platform deployment with native performance, rich UI animation support, and on-device machine learning (TensorFlow Lite) for computer vision tasks.
- **Spring Boot:** Offers robust enterprise-grade backend stability, high throughput, easy dependency injection, scalable REST API structures, and native Java execution of AI workout and nutrition recommendation algorithms.
- **MongoDB:** Flexible schema design accommodates changing fitness data structures (adaptive workout plans, varying nutrition logs) seamlessly.
