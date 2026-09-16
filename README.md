# FitFlow Redesign Project 🏋️‍♂️📱

A human-centered redesign of the **FitFlow** fitness tracking application, addressing user retention, engagement, and tracking friction through AI-driven workout recommendations, smart nutrition logging, and privacy-focused social circles.

---

## 📌 Project Overview & Lab Exercise 05 Complete Coverage

This repository serves as the official monorepo and documentation hub for **IT3060 - Human Computer Interaction (Lab Exercise 05)**. It contains the complete deliverables for all 5 activities:

1. **[Activity 1: Frontend Framework Comparison](docs/activity1-frontend-comparison.md)** — In-depth evaluation of React Native, Flutter, Kotlin Multiplatform, and SwiftUI.
2. **[Activity 2: Backend, Database & Auth Comparison](docs/activity2-backend-database-auth.md)** — Comparative analysis of Spring Boot, Node.js, FastAPI, MongoDB, PostgreSQL, and Firebase Auth.
3. **[Activity 3: Weighted Decision Matrix](docs/activity3-weighted-decision-matrix.md)** — Comprehensive decision matrix with criterion weights tailored for FitFlow.
4. **[Activity 4: System Architecture & ADR](docs/activity4-architecture-and-adr.md)** — High-level Mermaid diagrams, feature data flows, and formal Architecture Decision Record (ADR-001).
5. **[Activity 5: GitHub Repository Setup & Governance](README.md)** — Repository setup, folder structure, `.gitignore`, and branch protection guidelines.

---

## 🛠️ Selected Technology Stack
- **Mobile Frontend:** React Native (iOS & Android) with `react-native-reanimated`
- **Core Backend Service:** Java Spring Boot (REST API Microservices)
- **AI Microservice:** Python (FastAPI, PyTorch / TensorFlow Lite, OpenCV)
- **Database:** MongoDB Atlas (NoSQL Document Store)
- **Authentication:** Firebase Auth & JWT

---

## 📁 Repository Structure
```
fitflow-redesign/
├── frontend/                               # React Native mobile application codebase
├── backend/                                # Spring Boot backend API service codebase
├── ai-service/                             # Python AI & Computer Vision microservice codebase
└── docs/                                   # Lab Exercise 05 Documentation Suite
    ├── activity1-frontend-comparison.md    # Activity 1: Frontend analysis & selection
    ├── activity2-backend-database-auth.md  # Activity 2: Backend, DB & Auth analysis
    ├── activity3-weighted-decision-matrix.md# Activity 3: Weighted decision matrix
    ├── activity4-architecture-and-adr.md   # Activity 4: Architecture diagram & ADR-001
    ├── tech-stack-summary.md               # Executive Tech Stack Summary
    ├── comparison-matrix.md                # Quick Matrix Reference
    └── architecture-diagram.md             # System Diagram Overview
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v18+) & npm/yarn
- Java Development Kit (JDK 17+)
- Python (v3.10+)
- MongoDB (Local instance or MongoDB Atlas URI)
- Git

### Installation & Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/<your-username>/fitflow-redesign.git
   cd fitflow-redesign
   ```

2. **Frontend Setup (React Native)**
   ```bash
   cd frontend
   npm install
   npx react-native run-android # or run-ios
   ```

3. **Backend Setup (Spring Boot)**
   ```bash
   cd ../backend
   ./mvnw clean install  # or ./gradlew build
   ./mvnw spring-boot:run
   ```

4. **AI Microservice Setup (Python)**
   ```bash
   cd ../ai-service
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   uvicorn main:app --reload
   ```

---

## 🔒 Branch Protection Guidelines (Activity 5)
To ensure code quality and maintain repository integrity on GitHub:
1. Navigate to **Settings** > **Branches** > **Add branch protection rule**.
2. Set **Branch name pattern** to `main`.
3. Enable **Require a pull request before merging** (Minimum 1 approval).
4. Enable **Require status checks to pass before merging**.
5. Enable **Do not allow bypassing the above settings**.
