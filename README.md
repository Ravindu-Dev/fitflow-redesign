# FitFlow Redesign Project 🏋️‍♂️📱

A human-centered redesign of the **FitFlow** fitness tracking application, addressing user retention, engagement, and tracking friction through AI-driven workout recommendations, smart nutrition logging, and privacy-focused social circles.

---

## 📌 Project Overview
FitFlow is a health-tech platform designed to empower users on their fitness journey. This repository contains the full monorepo structure for the redesigned FitFlow mobile client, backend microservices, AI engine, and technical documentation.

---

## 🛠️ Technology Stack
- **Mobile Frontend:** React Native (iOS & Android)
- **Backend Service:** Java Spring Boot (RESTful API & Microservices)
- **Database:** MongoDB (NoSQL Document Store)
- **AI Microservice:** Python (FastAPI, TensorFlow Lite, Computer Vision)
- **Authentication:** Firebase Auth & JWT

---

## 📁 Repository Structure
```
fitflow-redesign/
├── frontend/        # React Native mobile application
├── backend/         # Spring Boot backend API service
├── ai-service/      # Python AI & Computer Vision microservice
└── docs/            # Project documentation, comparison matrices & architecture
    ├── tech-stack-summary.md
    ├── comparison-matrix.md
    └── architecture-diagram.md
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

## 🔒 Branch Protection Guidelines
To ensure code quality and maintain repository integrity, follow the branch protection rules outlined in the setup documentation when pushing to GitHub:
1. Require a Pull Request (PR) before merging into `main`.
2. Require at least 1 approving review.
3. Require status checks (CI/CD pipeline build & tests) to pass before merging.
4. Restrict direct pushes to the `main` branch.
