# 1️⃣ What is System Design (Really)?

System design is the discipline of **designing software systems that continue to work correctly as load, users, data, and failures increase**.

---

### ❌ It is NOT:
- Choosing frameworks
- Writing business logic
- UI design

### ✅ It IS:
- How components interact
- How data flows
- How systems fail
- How systems recover
- How systems scale

---

#### **Mental Model**
Think in terms of:

```
Clients → APIs → Services → Databases → Caches → Queues
```

---

#### **System Design Answers:**
- What happens when traffic spikes?
- What breaks first?
- How do we scale safely?
- How do we measure performance?

---

# 2️⃣ Core Metrics You MUST Know (Non-Negotiable)

These metrics are the language of system design.

## 2.1 **Throughput**

**Definition:**  
Throughput = how much work your system completes per unit time.

**Examples:**
- Requests per second
- Messages per minute
- Files uploaded per hour

**Example:**  
If your API handles 500 requests per second:  
➡️ **Your throughput = 500 RPS**

**Key Insight:**  
- Throughput answers: _“How much can we process?”_  
- But **NOT**: _“How fast does one request complete?”_ (that’s *latency*)

---

## 2.2 **Latency**

**Definition:**  
Latency = time taken for a single request to complete.

**Measured in:**
- milliseconds (ms)
- seconds

**Example:**  
User sends request → Response arrives in 120ms  
➡️ **Latency = 120ms**

**Why latency matters more than you think:**  
Users feel:
- <100ms → instant
- 100–300ms → fast
- 300–1000ms → slow
- 1s → broken

**Key Insight:**  
You can have:
- High throughput
- Terrible latency

_Example: A batch system processing millions of jobs slowly._

---

## 2.3 **QPS (Queries Per Second)**

**Definition:**  
QPS = number of requests hitting your system per second.

**Relationship:**  
QPS ≈ Throughput (for APIs)

But:
- QPS focuses on **incoming load**
- Throughput focuses on **successful processing**

**Example:**
- Incoming QPS: 1,000
- Processed: 800
- Failed: 200

_Your system is overloaded._

---

## 2.4 **Availability**

**Definition:**  
Availability = percentage of time your system is usable.

**Measured as:**  
`Availability = Uptime / Total Time`

**Common SLOs:**
| Availability | Downtime / Year   |
| ------------ | ---------------- |
| 99%          | ~3.6 days        |
| 99.9%        | ~8.7 hours       |
| 99.99%       | ~52 minutes      |

**Key Insight:**  
High availability requires:
- Redundancy
- Health checks
- Failover
- No single point of failure

---

# 3️⃣ How These Metrics Interact (CRITICAL)

You **cannot maximize everything at once**.

**Tradeoffs**
- Increasing throughput → may increase latency
- Reducing latency → may reduce throughput
- Increasing availability → increases cost & complexity

_System design is controlled compromise._

---

# 4️⃣ PRACTICAL FOUNDATION: MINI SOCIAL API

You will build something that grows across the curriculum.

### What are we building?
A Mini Social API with:
- Users
- Posts
- Likes (later)
- Comments (later)

*Today: foundation only*

---

## 4.1 **Architecture (Day 1 version)**

```
Client
  ↓
Node.js API
  ↓
PostgreSQL
```
- Single service.
- Single database.
- Simple on purpose.

---

## 4.2 **Why Docker from Day 1?**

Because real systems are **reproducible**.

Docker gives you:
- Same environment everywhere
- Isolation
- Predictability

---

# 5️⃣ IMPLEMENTATION (STEP-BY-STEP)

## 5.1 **Project Structure**
```
mini-social/
├── docker-compose.yml
├── api/
│   ├── Dockerfile
│   ├── package.json
│   └── index.js
```

---

## 5.2 **docker-compose.yml**
```yaml
version: "3.8"

services:
  api:
    build: ./api
    ports:
      - "3000:3000"
    depends_on:
      - db
    environment:
      DATABASE_URL: postgres://postgres:postgres@db:5432/social

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: social
    ports:
      - "5432:5432"
```

---

## 5.3 **API Dockerfile**
```dockerfile
FROM node:18

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

CMD ["node", "index.js"]
```

---

## 5.4 **package.json**
```json
{
  "name": "mini-social-api",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.19.0",
    "pg": "^8.11.3"
  }
}
```

---

## 5.5 **index.js (Minimal API)**
```js
const express = require("express");
const { Pool } = require("pg");

const app = express();
app.use(express.json());

const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
});

app.get("/health", async (_, res) => {
  res.json({ status: "ok" });
});

app.post("/users", async (req, res) => {
  const { email } = req.body;
  const result = await pool.query(
    "INSERT INTO users(email) VALUES($1) RETURNING *",
    [email]
  );
  res.json(result.rows[0]);
});

app.get("/users", async (_, res) => {
  const result = await pool.query("SELECT * FROM users");
  res.json(result.rows);
});

app.listen(3000, () => {
  console.log("API running on port 3000");
});
```

---

# 6️⃣ Database Schema (Day 1 Minimal)
```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email TEXT UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT now()
);
```

---

# 7️⃣ Connect Concepts to Reality (IMPORTANT)

**Throughput:**  
Each request hits Node + DB  
_DB will be the bottleneck first_

**Latency:**  
Query time + network + serialization

**QPS:**  
Try load testing:  
100 users → 100 QPS

**Availability:**  
If DB crashes → system down  
_Single point of failure (intentional for Day 1)_

---

# 8️⃣ Day 1 Thinking Exercises (DO THESE)

**What happens if:**
- 1,000 users sign up at once?
- What breaks first?
  - Node?
  - Postgres?

**How would latency change if:**
- DB is on another machine?

**How would you improve availability?**

_(These will be answered in Days 2–5.)_

---

# 9️⃣ What You Should Understand by End of Day 1

You should now be able to:
- Explain system design in one sentence
- Define throughput, latency, QPS, availability
- Identify bottlenecks in a simple architecture
- Run a real backend system locally using Docker
- Understand why this design will not scale

That last point is **intentional**.

---

## 🔜 What Day 2 Will Fix

Day 2 introduces:
- Stateless services
- Horizontal scaling
- JWT auth
- Removing single-instance limitations
