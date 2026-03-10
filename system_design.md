# 🏗️ System Design — Roadmap & Interview Questions

> A comprehensive quick-reference guide covering System Design topics for SDE interviews, based on the TakeUForward roadmap.

---

## 1. Basics

### Q1. What is System Design?

The process of defining a system's architecture, components, modules, interfaces, and data flow to satisfy specified requirements. Interviews test your ability to design **scalable, reliable, and maintainable** systems.

**Approach:** Requirements → Estimation → High-level design → Deep dive → Trade-offs → Bottlenecks.

---

### Q2. Horizontal vs. Vertical Scaling

| Feature    | Vertical (Scale Up) | Horizontal (Scale Out)                    |
| ---------- | ------------------- | ----------------------------------------- |
| How        | Add more CPU/RAM    | Add more machines                         |
| Limit      | Hardware ceiling    | Theoretically unlimited                   |
| Complexity | Simple              | Needs load balancing, distributed systems |
| Downtime   | Often required      | Zero downtime possible                    |
| Cost       | Expensive at scale  | Cost-effective                            |

---

### Q3. What is Capacity Estimation?

Estimating resources (servers, storage, bandwidth) needed for a system.

**Key metrics:** QPS (Queries Per Second), storage needs, bandwidth, memory.
**Approach:** Estimate DAU → peak traffic (2-5x average) → storage growth over time.

---

### Q4. What is HTTP?

**Hypertext Transfer Protocol** — application-layer protocol for web communication.

- **Stateless** (each request independent)
- Methods: GET, POST, PUT, DELETE, PATCH
- Status codes: 2xx (success), 3xx (redirect), 4xx (client error), 5xx (server error)
- **HTTPS** = HTTP + TLS encryption

---

### Q5. What is the Internet TCP/IP Stack?

The 4-layer model that powers the internet:

| Layer          | Function                 | Protocols            |
| -------------- | ------------------------ | -------------------- |
| Application    | User-facing services     | HTTP, DNS, FTP, SMTP |
| Transport      | End-to-end communication | TCP, UDP             |
| Internet       | Routing & addressing     | IP, ICMP             |
| Network Access | Physical transmission    | Ethernet, Wi-Fi      |

---

### Q6. What Happens When You Enter Google.com?

1. **DNS Lookup:** Browser → DNS resolver → Root → TLD → Authoritative → IP address
2. **TCP Connection:** 3-way handshake with Google's server
3. **TLS Handshake:** Establish encrypted connection (HTTPS)
4. **HTTP Request:** Browser sends GET request
5. **Server Processing:** Google processes request, queries databases
6. **HTTP Response:** Server returns HTML/CSS/JS
7. **Rendering:** Browser parses and renders the page

---

### Q7. What are Relational Databases?

Store data in **tables** with rows and columns, related via keys. Use SQL. Follow ACID properties.

**Examples:** MySQL, PostgreSQL, Oracle, SQL Server.
**When to use:** Structured data, complex queries, strong consistency needed.

---

### Q8. What are Database Indexes?

Data structures (typically B+ Trees) that speed up data retrieval at the cost of slower writes and extra storage.

**Types:** Clustered (one per table, reorders data), Non-clustered (separate structure), Composite (multi-column).

---

### Q9. What are NoSQL Databases?

Non-relational databases for unstructured/semi-structured data, designed for scalability.

| Type              | Structure              | Example          |
| ----------------- | ---------------------- | ---------------- |
| **Document**      | JSON-like documents    | MongoDB          |
| **Key-Value**     | Simple key-value pairs | Redis, DynamoDB  |
| **Column-family** | Column-oriented        | Cassandra, HBase |
| **Graph**         | Nodes and edges        | Neo4j            |

---

### Q10. What is a Cache?

An in-memory data store for frequently accessed data, reducing database load.

**Cache strategies:** Cache-aside (lazy), Write-through, Write-back, Write-around.
**Eviction policies:** LRU, LFU, FIFO, TTL-based.

---

### Q11. What is Thrashing?

When a system spends excessive time swapping pages between memory and disk, causing severe performance degradation. In system design context, it refers to cache or resource thrashing when too many requests compete for limited resources.

---

### Q12. What are Threads?

Lightweight units of execution within a process. Share memory space with other threads in the same process.

**Thread vs Process:** Threads share memory (faster communication, less isolation). Processes have separate memory (safer, heavier).

**Thread Pool:** Pre-created threads ready to handle requests → avoids creation overhead.

---

## 2. Load Balancing

### Q13. What is Load Balancing?

Distributing incoming traffic across multiple servers to ensure no single server is overwhelmed.

**Algorithms:**
| Algorithm | How |
|-----------|-----|
| **Round Robin** | Cycle through servers sequentially |
| **Weighted Round Robin** | More traffic to stronger servers |
| **Least Connections** | Send to server with fewest active connections |
| **IP Hash** | Hash client IP → consistent server |
| **Random** | Random server selection |

**Types:** L4 (transport layer, TCP/UDP) vs L7 (application layer, HTTP).

---

### Q14. What is Consistent Hashing?

A hashing technique that minimizes redistribution when servers are added/removed.

**How:** Servers and keys placed on a virtual ring. Each key maps to the next server clockwise.
**Adding a server:** Only keys between the new server and its predecessor are remapped.
**Virtual nodes:** Each server gets multiple positions on the ring for even distribution.

**Used in:** DynamoDB, Cassandra, CDNs.

---

### Q15. What is Sharding?

Splitting a database horizontally across multiple servers (shards).

**Strategies:** Range-based, Hash-based, Directory-based.
**Benefits:** Scalability, performance, fault isolation.
**Challenges:** Cross-shard queries, rebalancing, joins across shards.

---

## 3. DataStores

### Q16. What are Bloom Filters?

A **space-efficient probabilistic data structure** that tells you if an element is _possibly_ in a set or _definitely not_.

- **False positives:** Possible (says "maybe yes" when it's actually no)
- **False negatives:** Never (if it says "no", it's definitely no)
- Uses multiple hash functions and a bit array
- **Use cases:** Cache lookups, spam filters, database query optimization

---

### Q17. What is Data Replication?

Copying data across multiple servers for **reliability, availability, and performance**.

| Type              | Description                                                                 |
| ----------------- | --------------------------------------------------------------------------- |
| **Synchronous**   | Write confirmed only after all replicas updated (consistent but slow)       |
| **Asynchronous**  | Write confirmed immediately; replicas updated later (fast but may be stale) |
| **Master-Slave**  | One master handles writes; slaves handle reads                              |
| **Master-Master** | Multiple masters handle reads and writes                                    |

---

### Q18. How are NoSQL Databases Optimized?

- **LSM Trees + SSTables:** Write-optimized storage (Cassandra, RocksDB)
- **Compaction:** Merge sorted files to reduce read amplification
- **Bloom Filters:** Skip unnecessary disk reads
- **Memtables:** In-memory buffer before flushing to disk
- **Consistent Hashing:** Distribute data evenly across nodes

---

### Q19. What are Location-based Databases?

Databases optimized for geospatial data.

**Techniques:** Geohashing (encode lat/long into string), Quadtrees (divide space into quadrants), R-trees (rectangle-based indexing).

**Use cases:** Uber (nearby drivers), Yelp (nearby restaurants), Google Maps.

---

### Q20. Database Migrations

The process of changing a database schema or moving data between systems.

**Best practices:** Version control migrations, backward-compatible changes, blue-green deployments, test thoroughly, have rollback plans.

---

## 4. Consistency vs. Availability

### Q21. What is Data Consistency?

All nodes see the same data at the same time.

**CAP Theorem:** A distributed system can guarantee at most 2 of 3:

- **Consistency:** All reads return the latest write
- **Availability:** Every request gets a response
- **Partition Tolerance:** System works despite network partitions

In practice, network partitions happen, so you choose **CP** (consistent) or **AP** (available).

---

### Q22. Data Consistency Levels

| Level                | Description                                        |
| -------------------- | -------------------------------------------------- |
| **Strong**           | Reads always return latest write (linearizable)    |
| **Eventual**         | Reads may return stale data temporarily; converges |
| **Causal**           | Preserves cause-effect ordering                    |
| **Read-your-writes** | User always sees their own writes                  |

---

### Q23. Transaction Isolation Levels

| Level            | Dirty Read | Non-Repeatable | Phantom |
| ---------------- | ---------- | -------------- | ------- |
| Read Uncommitted | ✅         | ✅             | ✅      |
| Read Committed   | ❌         | ✅             | ✅      |
| Repeatable Read  | ❌         | ❌             | ✅      |
| Serializable     | ❌         | ❌             | ❌      |

---

## 5. Message Queues

### Q24. What is a Message Queue?

An asynchronous communication mechanism where producers send messages and consumers process them independently.

**Benefits:** Decoupling, buffering, load leveling, fault tolerance.
**Examples:** RabbitMQ, Apache Kafka, Amazon SQS, Redis Streams.

---

### Q25. What is the Publisher-Subscriber Model?

**Pub/Sub** pattern where publishers send messages to topics and subscribers receive messages from topics they've subscribed to.

**Pub/Sub vs Queue:** In pub/sub, all subscribers get every message. In queues, each message goes to one consumer.
**Examples:** Kafka topics, Redis Pub/Sub, Google Pub/Sub.

---

### Q26. What are Event-Driven Systems?

Architecture where components communicate through events (state changes). Producers emit events; consumers react.

**Patterns:** Event sourcing (store all events), CQRS (separate read/write models), Saga (distributed transactions).
**Benefits:** Loose coupling, scalability, real-time processing.

---

### Q27. Database as a Message Queue

Using database tables as a message queue (outbox pattern).

**How:** Write to a "messages" table → background worker polls and processes.
**Pros:** Transactional consistency (write data + message atomically).
**Cons:** Polling latency, not designed for high throughput.

---

## 6. DevOps Concepts

### Q28. What is a Single Point of Failure (SPOF)?

A component whose failure brings down the entire system.

**Examples:** Single database, single load balancer, single DNS server.
**Solutions:** Redundancy, replication, failover, distributed architecture.

---

### Q29. What are Containers?

Lightweight, isolated environments for running applications with their dependencies.

**Docker:** Package app + dependencies into a container image.
**Kubernetes (K8s):** Orchestrates containers — scaling, deployment, health checks.

**Containers vs VMs:** Containers share the OS kernel (lighter, faster); VMs have full OS (heavier, more isolated).

---

### Q30. What is Service Discovery and Heartbeats?

- **Service Discovery:** How services find each other in a distributed system (e.g., Consul, etcd, ZooKeeper).
- **Heartbeats:** Periodic signals sent to indicate a service is alive. If heartbeats stop → service marked as dead → failover triggered.

---

### Q31. How to Avoid Cascading Failures?

When one service failure causes others to fail.

**Solutions:**

- **Circuit Breaker:** Stop calling a failing service; return fallback
- **Bulkhead:** Isolate resources per service
- **Timeouts:** Don't wait indefinitely
- **Retries with backoff:** Exponential backoff + jitter
- **Rate limiting:** Prevent overload
- **Graceful degradation:** Return partial results instead of error

---

### Q32. Anomaly Detection in Distributed Systems

Detecting unusual behavior (latency spikes, error rate increases, resource exhaustion).

**Techniques:** Statistical methods (Z-score), ML-based detection, threshold alerts, log analysis.
**Tools:** Prometheus, Grafana, Datadog, ELK Stack.

---

### Q33. Distributed Rate Limiting

Controlling request rates across multiple servers.

**Algorithms:** Token bucket, Leaky bucket, Fixed/Sliding window counter.
**Challenges:** Synchronizing counters across nodes → use Redis or similar shared store.

---

## 7. Caching

### Q34. What is Distributed Caching?

Cache spread across multiple nodes for scalability and fault tolerance.

**Examples:** Redis Cluster, Memcached.
**Consistency:** Use consistent hashing to distribute keys.

---

### Q35. What are Content Delivery Networks (CDNs)?

Geographically distributed servers caching static content close to users.

**How:** User → nearest CDN edge server → cache hit (fast) or origin pull.
**Benefits:** Lower latency, reduced origin load, DDoS protection.
**Examples:** CloudFlare, AWS CloudFront, Akamai.

---

### Q36. Write Policies

| Policy            | How                                        | Trade-off                  |
| ----------------- | ------------------------------------------ | -------------------------- |
| **Write-Through** | Write to cache AND database simultaneously | Consistent but slow        |
| **Write-Back**    | Write to cache first; sync to DB later     | Fast but risk of data loss |
| **Write-Around**  | Write to DB only; cache on read miss       | Avoids cache pollution     |

---

### Q37. Replacement Policies

What to evict when cache is full:

| Policy                          | Evicts                         |
| ------------------------------- | ------------------------------ |
| **LRU** (Least Recently Used)   | Least recently accessed item   |
| **LFU** (Least Frequently Used) | Least frequently accessed item |
| **FIFO**                        | Oldest item                    |
| **Random**                      | Random item                    |

---

## 8. Microservices

### Q38. Microservices vs. Monoliths

| Feature        | Monolith                   | Microservices                   |
| -------------- | -------------------------- | ------------------------------- |
| **Deployment** | Deploy everything together | Deploy services independently   |
| **Scaling**    | Scale everything           | Scale individual services       |
| **Technology** | Single tech stack          | Polyglot                        |
| **Complexity** | Simple initially           | Complex (networking, debugging) |
| **Failure**    | One bug can crash all      | Isolated failures               |

---

### Q39. How Monoliths are Migrated

**Strangler Fig Pattern:** Gradually replace monolith pieces with microservices while the monolith continues running.

**Steps:** Identify bounded contexts → extract one service at a time → route traffic → decommission old code.

---

## 9. API Gateways

### Q40. How are APIs Designed?

- **RESTful:** Resource-based URLs, HTTP methods, stateless (most common)
- **GraphQL:** Client specifies exact data needed
- **gRPC:** Fast binary protocol using Protocol Buffers

**Best practices:** Versioning (v1/v2), pagination, rate limiting, proper status codes, idempotency.

---

### Q41. What are Asynchronous APIs?

APIs where the client doesn't wait for the result immediately.

**Patterns:** Webhooks (server calls back), Polling (client checks periodically), WebSockets (persistent bidirectional connection), Server-Sent Events (server pushes).

---

## 10. Authentication Mechanisms

### Q42. OAuth

Open standard for **delegated authorization**. Lets apps access user data without exposing passwords.

**OAuth 2.0 Flow:** User → App redirects to Auth Server → User logs in → Auth Server returns authorization code → App exchanges code for access token → App uses token to access resources.

**Roles:** Resource Owner (user), Client (app), Authorization Server, Resource Server.

---

### Q43. Token-Based Authentication

Client authenticates once; server issues a **token** (e.g., JWT) used for subsequent requests.

**JWT (JSON Web Token):** Header.Payload.Signature — self-contained, stateless.
**Refresh Tokens:** Long-lived token to get new access tokens without re-login.

---

### Q44. Access Control Lists and Rule Engines

- **ACL:** List mapping users/roles to permissions for specific resources.
- **RBAC:** Role-Based Access Control (User → Role → Permissions).
- **ABAC:** Attribute-Based Access Control (rules based on attributes like time, location).
- **Rule Engines:** Evaluate business rules dynamically to make authorization decisions.

---

## 11. System Design Tradeoffs

### Q45. Pull vs. Push

|          | Pull                      | Push                           |
| -------- | ------------------------- | ------------------------------ |
| How      | Client requests data      | Server sends data              |
| Latency  | Higher (polling interval) | Lower (real-time)              |
| Example  | RSS feeds, polling APIs   | WebSockets, push notifications |
| Use when | Low update frequency      | Real-time needs                |

---

### Q46. Memory vs. Latency

More memory (caching) = lower latency but higher cost. Trade off based on access patterns and budget.

---

### Q47. Throughput vs. Latency

- **Throughput:** Number of requests processed per unit time.
- **Latency:** Time to process a single request.
- Optimizing one often hurts the other (batching increases throughput but increases latency).

---

### Q48. Consistency vs. Availability

**CAP Theorem trade-off.** Pick CP (banking) or AP (social media) based on requirements.

---

### Q49. Latency vs. Accuracy

- **Real-time** → accept approximate results (recommendations, search suggestions)
- **Batch processing** → exact results but slower (analytics, reports)

---

### Q50. SQL vs. NoSQL Databases

| SQL                         | NoSQL                       |
| --------------------------- | --------------------------- |
| Structured, schema-enforced | Flexible schema             |
| ACID                        | BASE (eventual consistency) |
| Vertical scaling            | Horizontal scaling          |
| Complex queries (JOINs)     | Simple queries              |
| Banking, ERP                | Real-time apps, big data    |

---

## 12. Practice Problems

Design each system considering scalability, reliability, and performance:

| #   | Problem                                                                 |
| --- | ----------------------------------------------------------------------- |
| 1   | **Live-Streaming App** — Real-time video encoding, CDN, chat            |
| 2   | **Instagram** — Photo uploads, feeds, stories, notifications            |
| 3   | **Tinder** — Location-based matching, real-time messaging               |
| 4   | **WhatsApp** — End-to-end encrypted messaging, group chat, media        |
| 5   | **TikTok** — Short video uploads, recommendation engine, CDN            |
| 6   | **Online Coding Judge (Part 1)** — Code submission, sandboxed execution |
| 7   | **Online Coding Judge (Part 2)** — Scaling, result caching, queue       |
| 8   | **UPI Payments** — Secure transactions, bank integration, idempotency   |
| 9   | **IRCTC** — High traffic booking, seat inventory, queuing               |
| 10  | **Netflix Video Pipeline** — Video ingestion, transcoding, CDN          |
| 11  | **DoorDash** — Real-time delivery, driver matching, ETA                 |
| 12  | **Amazon Online Shop** — Product catalog, cart, orders, payments        |
| 13  | **Google Maps** — Geospatial data, routing, real-time traffic           |
| 14  | **Gmail** — Email storage, search, spam filtering, attachments          |
| 15  | **Chess Website** — Real-time game state, matchmaking, WebSockets       |
| 16  | **Uber** — Ride matching, surge pricing, real-time tracking             |
| 17  | **Google Docs** — Real-time collaboration, OT/CRDT, versioning          |

---

## 13. Additional Resources

- [InterviewReady Course](https://interviewready.io/) — Comprehensive system design course
- [System Design Primer (GitHub)](https://github.com/donnemartin/system-design-primer) — Community resource
- **"Designing Data-Intensive Applications"** by Martin Kleppmann — Gold standard book

---

> 📖 **Source:** [TakeUForward — Complete System Design Roadmap](https://takeuforward.org/system-design/complete-system-design-roadmap-with-videos-for-sdes)
