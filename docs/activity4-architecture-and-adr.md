# Activity 4: High-Level Architecture & Architecture Decision Record (ADR) - FitFlow Redesign

## 1. Overview
This document presents the complete system architecture for the **FitFlow Redesign**, illustrating system components, data flows, security mechanisms, scalability strategies, and the formal Architecture Decision Record (ADR).

---

## 2. System Architecture Diagram

```mermaid
graph TD
    %% Client Layer
    subgraph Client Layer
        MobileApp[React Native Mobile App - iOS & Android]
        WebApp[React Native for Web Client]
    end

    %% Gateway & Auth Layer
    subgraph Gateway & Security Layer
        APIGateway[API Gateway / Spring Cloud Gateway]
        AuthServer[Firebase Auth / OAuth2 JWT Provider]
    end

    %% Microservices Layer
    subgraph Microservices Layer
        CoreBackend[Spring Boot Core Service - User Profile & Workouts]
        SocialService[Spring Boot Social Service - Circles & Feeds]
        AIService[Python / FastAPI AI Microservice - Recommendation Engine & CV]
    end

    %% Data & Infrastructure Layer
    subgraph Data & Persistence Layer
        MongoDB[(MongoDB Atlas - User & Workout Data)]
        RedisCache[(Redis Cluster - Caching & Session Store)]
        S3Storage[(AWS S3 / Cloud Storage - Images & Assets)]
    end

    %% External Connections
    MobileApp --> APIGateway
    WebApp --> APIGateway
    APIGateway --> AuthServer
    APIGateway --> CoreBackend
    APIGateway --> SocialService
    APIGateway --> AIService

    CoreBackend --> MongoDB
    CoreBackend --> RedisCache
    SocialService --> MongoDB
    SocialService --> RedisCache
    AIService --> MongoDB
    AIService --> S3Storage
```

---

## 3. Data Flow Diagrams for Key Features

### 3.1 Feature 1: Personalized AI Workout Recommendation ("Daily Flow")
```mermaid
sequenceDiagram
    autonumber
    actor User as Mobile App (React Native)
    participant GW as API Gateway
    participant Core as Spring Boot Core API
    participant AI as Python AI Service
    participant DB as MongoDB

    User->>GW: GET /api/v1/workouts/daily-flow
    GW->>Core: Forward request with validated JWT
    Core->>DB: Fetch user profile, recent activity & fitness goals
    DB-->>Core: Return profile metadata
    Core->>AI: POST /ai/generate-plan (profile metadata)
    AI->>AI: Run ML Recommendation Model (TensorFlow)
    AI-->>Core: Return tailored workout plan JSON
    Core->>DB: Save recommended plan
    Core-->>GW: Return HTTP 200 (Workout Plan)
    GW-->>User: Render "Daily Flow" Recommendation Card
```

### 3.2 Feature 2: Camera-Based Nutrition Logging (Computer Vision)
```mermaid
sequenceDiagram
    autonumber
    actor User as Mobile App (React Native Camera)
    participant GW as API Gateway
    participant AI as Python AI Service (OpenCV/PyTorch)
    participant DB as MongoDB

    User->>GW: POST /api/v1/nutrition/recognize (Image File)
    GW->>AI: Stream image to AI Vision Service
    AI->>AI: Run Object Recognition & Food Classifier Model
    AI-->>GW: Return predicted food items + confidence score + estimated calories
    GW-->>User: Display food recognition result for user confirmation
    User->>GW: POST /api/v1/nutrition/log (Confirmed Meal)
    GW->>DB: Save meal entry to user daily journal
```

### 3.3 Feature 3: Private Social Circles & Activity Feed
```mermaid
sequenceDiagram
    autonumber
    actor User as Mobile App
    participant GW as API Gateway
    participant Social as Spring Boot Social Service
    participant Cache as Redis Cache
    participant DB as MongoDB

    User->>GW: POST /api/v1/social/circles/{id}/post (Workout Completed)
    GW->>Social: Create new circle post
    Social->>DB: Persist post document in MongoDB
    Social->>Cache: Invalidate & update Circle Feed Cache in Redis
    Social-->>GW: Return HTTP 201 Created
    GW-->>User: Update live feed via WebSockets
```

---

## 4. Architecture Decision Record (ADR)

### ADR-001: Selection of React Native, Spring Boot, MongoDB, and Python AI Microservice for FitFlow Redesign

* **Status:** Approved
* **Date:** 2026-09-16
* **Deciders:** FitFlow Redesign Product & Engineering Team

#### Context & Problem Statement
FitFlow experienced a significant decline in user retention (drop to 3.8 stars) due to generic workout recommendations, high friction in nutrition tracking, and lack of social accountability. The engineering team requires a modernized technology stack capable of supporting:
1. Fast cross-platform mobile delivery for iOS and Android.
2. Enterprise-grade, scalable API backend.
3. Flexible storage for dynamic health metrics and meal logs.
4. Dedicated AI microservice for recommendation algorithms and computer vision food recognition.

#### Decision
We decided to adopt:
- **Frontend:** React Native (TypeScript) with `react-native-reanimated`.
- **Backend Services:** Java Spring Boot for enterprise APIs and microservice architecture.
- **AI Microservice:** Python (FastAPI) leveraging PyTorch / TensorFlow Lite.
- **Database:** MongoDB Atlas (NoSQL) for high-performance schema flexibility.
- **Authentication:** Firebase Auth with JWT verification.

#### Consequences
* **Positive Consequences:**
  - High code reusability (>85%) across mobile platforms using React Native.
  - Decoupled AI microservice allows independent scaling of heavy ML compute workloads without degrading main API responsiveness.
  - MongoDB document model eliminates complex SQL migrations when adding new fitness attributes.
* **Negative Consequences:**
  - Managing a multi-language stack (Java, Python, TypeScript) increases operational complexity.
  - Requires maintaining proper contract definitions (OpenAPI/Swagger) across services.

---

## 5. Security & Scalability Considerations
- **Security:** OAuth2/JWT authentication, TLS 1.3 encryption for data in transit, AES-256 for data at rest in MongoDB Atlas, and strict GDPR compliance for anonymized health data.
- **Scalability:** Horizontal scaling of Spring Boot backend instances via Kubernetes/Docker; Redis caching layer for sub-10ms feed reads; decoupled async queuing for AI image processing tasks.
