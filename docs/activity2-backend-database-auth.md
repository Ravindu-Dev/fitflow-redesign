# Activity 2: Backend, Database, and Authentication Comparison - FitFlow Redesign

## 1. Overview
This document evaluates candidate backend frameworks, database management systems, and authentication/authorization solutions to support the **FitFlow Redesign** architecture.

---

## 2. Backend Framework Comparison

| Framework | Language | Performance & Concurrency | Scalability | AI/ML Integration | Dev Speed | Security & Ecosystem | Recommendation Status |
|---|---|---|---|---|---|---|---|
| **Spring Boot** | Java | Very High (Multithreading/Virtual Threads) | Enterprise High | Moderate (via REST to AI Microservice) | High | Excellent (Spring Security, Enterprise standards) | **Selected for Core API** |
| **Node.js / NestJS** | TypeScript | High (Event Loop / Async I/O) | High | Good (JS/Python IPC) | Very High | Good | Alternative |
| **FastAPI** | Python | High (Asynchronous ASGI) | High | Outstanding (Native PyTorch/TensorFlow/OpenCV) | Very High | Good | **Selected for AI Microservice** |
| **Go (Gin/Fiber)** | Go | Extremely High (Goroutines) | Extremely High | Low (Requires Cgo/External) | High | Strong | Overkill for mid-sized team |

---

## 3. Database System Comparison

| Database | Model Type | Schema Flexibility | Health & Nutrition Data Query Performance | Real-time Capabilities | GDPR/HIPAA Security Controls | Selection |
|---|---|---|---|---|---|---|
| **MongoDB** | NoSQL Document | High (Dynamic workout plans & flexible nutrition logs) | Excellent (Indexing JSON documents) | Change Streams support | Role-based access, Client-side Field Level Encryption | **Selected Primary DB** |
| **PostgreSQL** | Relational SQL | Low (Rigid relational tables) | High (Complex join queries) | Logical Replication / Listen-Notify | Robust encryption & audit logs | Alternative |
| **Firebase Firestore** | NoSQL Document | High | Moderate (Query limitations on arrays/nested fields) | Native real-time listeners | GCP IAM compliance | Selected for Social/Feeds |
| **Amazon DynamoDB** | NoSQL Key-Value | High | High (Single-digit ms latency) | DynamoDB Streams | AWS KMS encryption | High cost for complex queries | Rejected |

---

## 4. Authentication & Authorization Comparison

| Solution | Auth Protocol Support | Security & Compliance (GDPR/HIPAA) | Real-time & Social Auth | Cost / Pricing | Maintenance Effort | Selection |
|---|---|---|---|---|---|---|
| **Firebase Auth** | OAuth2, OIDC, Social Login, Phone Auth | Compliant (SOC 2, ISO 27001, GDPR) | Native integration with Firebase SDKs | Generous free tier, Pay-as-you-go | Low (Managed Service) | **Selected Primary Auth** |
| **AWS Cognito** | OAuth2, SAML 2.0, OIDC | HIPAA Eligible, GDPR Compliant | AWS SDK integration | Low pay-per-MAU | Moderate (Complex setup) | Alternative |
| **Auth0** | OAuth2, OIDC, Enterprise SSO | HIPAA & GDPR Compliant | Broad SDK support | Expensive at scale | Very Low | Rejected due to cost |
| **Supabase Auth** | OAuth2, Magic Links | GDPR Compliant | Postgres Row-Level Security | Low | Low | Alternative |

---

## 5. Security & Compliance Analysis
- **GDPR & CCPA Compliance:**
  - Mandatory user consent tracking and anonymized health data storage.
  - Right to be forgotten (cascading deletion of user profiles and telemetry records in MongoDB).
  - Encrypted telemetry transmission over HTTPS/TLS 1.3 and WSS (Secure WebSockets).
- **Data Encryption:**
  - Encryption in transit (TLS 1.3).
  - Encryption at rest using AES-256 for MongoDB Atlas document stores.

---

## 6. Recommended Technology Combination
- **Core Backend Service:** **Spring Boot** (Java 17+) for enterprise business logic, user management, and transactional integrity.
- **AI Microservice:** **Python / FastAPI** for serving machine learning models (personalized workout generation and computer vision food recognition).
- **Primary Database:** **MongoDB Atlas** for storing unstructured workout routines, nutrition logs, and user profile metadata.
- **Authentication:** **Firebase Auth** with JWT verification on the Spring Boot backend gateway.
