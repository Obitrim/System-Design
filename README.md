# System Design

This project documents my journey in learning System Design concepts and building robust, reliable, maintainable, and scalable applications.

---

## Curriculum Overview

By following this curriculum, you'll be prepared to step into senior engineering roles with strong focus on production-ready systems—beyond just theory.

**Legend:**

- 🎯 **Concept Focus**
- 🧠 **What You Must Understand**
- 🛠 **What You Must Implement**
- 💻 **Sample Project Stack:** _Node.js, PostgreSQL, Redis, Docker, Kafka, AWS-style architecture_

---

## 📆 12-Week System Design Curriculum (5 Days/Week)

### **Stack Used Throughout**

- **Backend:** Node.js (Express or NestJS)
- **Database:** PostgreSQL
- **Cache:** Redis
- **Queue:** Kafka _(or RabbitMQ)_
- **Infrastructure:** Docker
- **Monitoring:** Prometheus + Grafana
- **Cloud Concepts:** AWS-style (EC2, S3, ALB, etc.)

---

## 🔥 PHASE 1 — Core Foundations (Weeks 1–4)

<details>
<summary><strong>WEEK 1 – Scalability & Architecture Basics</strong></summary>

| Day   | Concept                        | You Must Know                          | Practical Task                                     | Sample Project          |
| ----- | ------------------------------ | -------------------------------------- | -------------------------------------------------- | ----------------------- |
| Day 1 | What is System Design?         | Throughput, latency, availability, QPS | Install Docker, set up Node + Postgres             | Start "Mini Social API" |
| Day 2 | Vertical vs Horizontal Scaling | Stateless services                     | Convert API to stateless                           | JWT auth                |
| Day 3 | Load Estimation                | Capacity planning                      | Estimate users, traffic, storage                   |                         |
| Day 4 | Monolith Architecture          | Pros/Cons                              | Build monolithic REST API                          |                         |
| Day 5 | Reverse Proxy & Load Balancer  | L4 vs L7                               | Add Nginx in front of app, run multiple containers |                         |

</details>

<details>
<summary><strong>WEEK 2 – Databases Deep Dive</strong></summary>

| Day   | Concept            | You Must Know           | Practical Task                   |
| ----- | ------------------ | ----------------------- | -------------------------------- |
| Day 1 | SQL Indexing       | B-tree, composite index | Add indexes & benchmark queries  |
| Day 2 | Transactions       | ACID, isolation levels  | Simulate race conditions         |
| Day 3 | Query Optimization | EXPLAIN, slow queries   | Optimize feed query              |
| Day 4 | Replication        | Read replicas           | Simulate read scaling            |
| Day 5 | NoSQL              | CAP theorem basics      | Compare Mongo vs Postgres design |

**✅ Project Feature:** Add Posts, Likes, Comments with optimized queries

</details>

<details>
<summary><strong>WEEK 3 – Caching & Performance</strong></summary>

| Day   | Concept            | You Must Know             | Practical Task                  |
| ----- | ------------------ | ------------------------- | ------------------------------- |
| Day 1 | Caching Strategies | Cache aside/write-through | Add Redis caching to feed       |
| Day 2 | Cache Invalidation | TTL/manual invalidation   | Implement invalidation logic    |
| Day 3 | CDN                | Static asset caching      | Serve images via CDN simulation |
| Day 4 | Rate Limiting      | Token bucket              | Implement API rate limiting     |
| Day 5 | Benchmarking       | Load testing basics       | Use k6 or Artillery             |

**✅ Project now handles 10k+ simulated users**

</details>

<details>
<summary><strong>WEEK 4 – API Design & Security</strong></summary>

| Day   | Concept             | You Must Know           | Practical Task                    |
| ----- | ------------------- | ----------------------- | --------------------------------- |
| Day 1 | REST Best Practices | Idempotency, pagination | Convert feed to cursor pagination |
| Day 2 | Auth                | JWT vs sessions         | Implement access & refresh tokens |
| Day 3 | OAuth               | OAuth2 flow             | Add Google login                  |
| Day 4 | RBAC                | Role-based access       | Add admin role                    |
| Day 5 | API Gateway         | Gateway patterns        | Create simple gateway service     |

</details>

---

## 🚀 PHASE 2 — Distributed Systems (Weeks 5–8)

<details>
<summary><strong>WEEK 5 – Messaging & Event Driven Systems</strong></summary>

| Day   | Concept                   | You Must Know         | Practical Task               |
| ----- | ------------------------- | --------------------- | ---------------------------- |
| Day 1 | Message Queues            | Async processing      | Install Kafka                |
| Day 2 | Producers/Consumers       | Delivery guarantees   | Publish post-created event   |
| Day 3 | Event-Driven Architecture | Decoupling services   | Create notification service  |
| Day 4 | Dead Letter Queues        | Failure handling      | Add retry logic              |
| Day 5 | Idempotency               | Exactly-once illusion | Prevent duplicate processing |

**✅ Split system into:**

- API service
- Notification service
- Analytics service

</details>

<details>
<summary><strong>WEEK 6 – Consistency & Distributed Data</strong></summary>

| Day   | Concept              | You Must Know               | Practical Task              |
| ----- | -------------------- | --------------------------- | --------------------------- |
| Day 1 | CAP Theorem          | Trade-offs                  | Simulate service outage     |
| Day 2 | Eventual Consistency | Read models                 | Build async read model      |
| Day 3 | CQRS                 | Command vs Query separation | Separate write/read DB      |
| Day 4 | Saga Pattern         | Distributed transactions    | Implement payment workflow  |
| Day 5 | Two Phase Commit     | Why to avoid                | Simulate failed transaction |

</details>

<details>
<summary><strong>WEEK 7 – Microservices Architecture</strong></summary>

| Day   | Concept                  | You Must Know        | Practical Task                |
| ----- | ------------------------ | -------------------- | ----------------------------- |
| Day 1 | Monolith → Microservices | Tradeoffs            | Break project into 3 services |
| Day 2 | Service Communication    | REST vs async        | Replace REST with events      |
| Day 3 | Service Discovery        | Basic understanding  | Simulate registry             |
| Day 4 | Circuit Breaker          | Fault isolation      | Add circuit breaker logic     |
| Day 5 | API Aggregation          | Backend for frontend | Build BFF layer               |

</details>

<details>
<summary><strong>WEEK 8 – Sharding & Scaling Databases</strong></summary>

| Day   | Concept            | You Must Know     | Practical Task               |
| ----- | ------------------ | ----------------- | ---------------------------- |
| Day 1 | Database Sharding  | Range vs hash     | Simulate sharded DB          |
| Day 2 | Consistent Hashing | Load distribution | Implement hash logic         |
| Day 3 | Rebalancing        | Data migration    | Move shard data              |
| Day 4 | Distributed Locks  | Redis locks       | Implement locking system     |
| Day 5 | Leader Election    | Raft basics       | Simulate simple leader logic |

</details>

---

## 🛡 PHASE 3 — Production Readiness (Weeks 9–10)

<details>
<summary><strong>WEEK 9 – Reliability & Observability</strong></summary>

| Day   | Concept         | You Must Know       | Practical Task       |
| ----- | --------------- | ------------------- | -------------------- |
| Day 1 | Fault Tolerance | Redundancy          | Run multi-node setup |
| Day 2 | Monitoring      | Metrics, logs       | Add Prometheus       |
| Day 3 | Tracing         | Distributed tracing | Add OpenTelemetry    |
| Day 4 | SLA/SLO         | Reliability math    | Define SLAs          |
| Day 5 | Chaos Testing   | Failure simulation  | Kill containers      |

</details>

<details>
<summary><strong>WEEK 10 – Cloud & Infrastructure</strong></summary>

| Day   | Concept             | You Must Know        | Practical Task             |
| ----- | ------------------- | -------------------- | -------------------------- |
| Day 1 | Docker Deep Dive    | Container networking | Optimize Dockerfiles       |
| Day 2 | CI/CD Pipelines     |                      | Setup GitHub Actions       |
| Day 3 | Cloud Architecture  | AWS-style infra      | Design AWS diagram         |
| Day 4 | Object Storage      | S3 design            | Implement file upload      |
| Day 5 | Deployment Strategy | Blue/Green           | Simulate deployment switch |

</details>

---

## 🧠 PHASE 4 — Interview & Advanced Design (Weeks 11–12)

<details>
<summary><strong>WEEK 11 – Design Famous Systems</strong></summary>

Design a full system from scratch each day:

| Day   | System           |
| ----- | ---------------- |
| Day 1 | URL Shortener    |
| Day 2 | Chat System      |
| Day 3 | Twitter Feed     |
| Day 4 | Payment System   |
| Day 5 | Ride-Hailing App |

</details>

<details>
<summary><strong>WEEK 12 – Senior Level Topics</strong></summary>

| Day   | Concept                           |
| ----- | --------------------------------- |
| Day 1 | Distributed Consensus             |
| Day 2 | Global Systems (multi-region)     |
| Day 3 | Data Privacy & Compliance         |
| Day 4 | Cost Optimization                 |
| Day 5 | Full Capstone Architecture Review |

</details>

---

## 🏗 Final Capstone Project

**Build:** _Scalable SaaS Platform_

**Features:**

- Auth
- RBAC
- Microservices
- Redis caching
- Kafka events
- Sharded DB
- File uploads
- Monitoring
- CI/CD
- Docker deployment

---

## 📚 Core Books You Must Read

- _Designing Data-Intensive Applications_
- _System Design Interview – An Insider's Guide_
- _Clean Architecture_

---

## ⚡ Career Growth Alignment

By completing this curriculum, you will:

- Move toward senior engineer level
- Strengthen your backend skills
- Gain a deep understanding of architecture

**Outcome:**  
You’ll reach Senior Backend level, be ready for FAANG-style system design interviews, and be capable of designing real SaaS architectures.
