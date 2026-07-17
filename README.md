# 💳 AiEnabled.PaymentPlatForm

> **A modern, high-throughput, and intelligent microservices-based payment processing architecture utilizing AI-driven fraud detection and advanced data analytics.**

---

## 🌐 Architecture Overview

This production-ready payment ecosystem is engineered for high scalability, fault tolerance, and independent service deployment. It bridges robust core transaction flows with real-time AI and predictive batch analytics.

### 🛠️ Core Technology Stack

| Component | Technologies |
| :--- | :--- |
| **Gateway & APIs** | ![NodeJS](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white) ![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white) |
| **Data Storage** | ![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white) |
| **Data Science & AI** | ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white) ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white) |
| **Infrastructure** | ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) ![Azure](https://img.shields.io/badge/Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white) |

---

## ⚙️ Microservices Topology

### 🚪 1. API Gateway
* **Purpose:** Single entry point exposing routing, secure request validation, logging, and rate-limiting.
* **Tech Stack:** Node.js + Express / Fastify / NestJS
* **Endpoints:**
  * `POST /api/payments` — Process new transactions
  * `GET /api/payments/:id` — Query transaction status
  * `POST /api/auth/login` — Account authentication
  * `POST /api/chat` — Connect to the AI assistant

### 👤 2. User Service
* **Purpose:** Manages active user accounts, customer profiles, payment preferences, and identity state.
* **Tech Stack:** Node.js + Express + SQL Server (ORM: TypeORM / Sequelize)

### 💰 3. Payment Service
* **Purpose:** Processes commands and coordinates transactions with payment networks (Stripe / PayPal / Adyen).
* **Tech Stack:** Node.js + Express + SQL Server transaction schemas

### 🚨 4. Fraud Service
* **Purpose:** Uses AI-driven decision systems to block high-risk transactions.
* **Tech Stack:** Node.js + OpenAI / Azure OpenAI endpoints
* **Outputs:**
  * `riskScore` — Dynamic 0-100 risk analysis rating
  * `status` — Real-time decision (`approved` / `review` / `declined`)

### 📈 5. Analytics Service
* **Purpose:** Scheduled or real-time batch processing pipeline detecting long-term payment fraud trends and performance logs.
* **Tech Stack:** Python + pandas

### 🤖 6. AI Assistant Service
* **Purpose:** An intelligent LLM chat helper translating confusing payment errors and transaction data into simple, user-friendly natural language explanations.
* **Tech Stack:** Node.js API calling LLM prompts

---

## 🎨 System Architecture Flow

```mermaid
graph TD
    Client[Client Browser/App] -->|HTTPS| Gateway[API Gateway]
    Gateway -->|Auth / Fetch Profile| UserService[User Service]
    Gateway -->|Execute Intent| PaymentService[Payment Service]
    Gateway -->|Support Chat| AIAssistant[AI Assistant Service]
    
    PaymentService -->|Verify Trust| FraudService[Fraud Service - LLM]
    PaymentService -->|Persist State| SQL[(SQL Server Database)]
    
    SQL -.->|Batch Export / Events| AnalyticsService[Analytics Service - Python & Pandas]
    
    style Gateway fill:#339933,stroke:#fff,stroke-width:2px,color:#fff
    style PaymentService fill:#007ACC,stroke:#fff,stroke-width:2px,color:#fff
    style FraudService fill:#CC2927,stroke:#fff,stroke-width:2px,color:#fff
    style AIAssistant fill:#412991,stroke:#fff,stroke-width:2px,color:#fff
    style AnalyticsService fill:#150458,stroke:#fff,stroke-width:2px,color:#fff
    style SQL fill:#444,stroke:#fff,stroke-dasharray: 5 5,color:#fff
