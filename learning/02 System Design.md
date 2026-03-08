### The SaaS System Design Organizer

**1. Core Application Services (The "What")**

* Project Management Tool (Jira)
* Chat Application (Real-time)
* URL Shortening Service (TinyURL)
* Job Scheduler (Cron + distributed jobs)
* Live Dashboard for Project Metrics

**2. Real-Time & Collaboration (The "How we work together")**

* Real-Time Collaboration Tool (Confluence)
* Collaboration Sync (CRDT-based)
* Live Co-Editing Presence System
* High-Availability WebSockets System
* Real-Time Presence & Heartbeats

**3. Search, Content & Data (The "Information Retrieval")**

* Search System for Knowledge Base / Scalable Content Indexer
* Permission-Aware Search / Issue Ticket Search Engine
* Search Ranking with Access Control
* Distributed File Store System (attachments)
* Tagging Service
* Top Confluence Feed System

**4. Distributed Infrastructure & Scaling (The "Heavy Lifting")**

* API Gateway / Load Balancer + Failover for APIs
* Rate Limiter Service / Global Rate Limiting / Scalable API Throttling
* Distributed Cache & Cache Invalidation System
* Database Sharding Strategy (by user/tenant)
* Multi-Region Failover System

**5. Events, Queues & Asynchronous Processing (The "Pipes")**

* Scalable Notification System / Push Notifications
* Distributed Messaging System (Pub/Sub)
* Distributed Queue Service
* Consistent Event Stream for Changes
* Big Data Pipeline for Event Processing

**6. Ops, Reliability & Multi-Tenancy (The "Enterprise Grade")**

* Tenant Isolation Systems / Multi-Tenant Billing & Quotas / Multi-Tenant Metrics
* Scalable Auth & Authorization (OAuth/SSO)
* Audit Logging System / Logging and Monitoring System
* Distributed Transactions / Eventual Consistency / Distributed Locks
* Data Backup + DR / Project Snapshot + Rollback
* Feature Flags System / A/B Feature Rollout

---

### The Interview Room: Deep Dive into Questions 1-5

Let's treat this like a real Amazon loop. I'll play both the interviewer pushing for depth and the candidate providing the architectural breakdown. We will anchor these designs heavily in AWS infrastructure and robust monitoring, treating these not just as concepts, but as systems ready for production.

#### 1. Design a Project Management Tool like Jira

**The Deep Dive:** The core challenge of Jira isn't just storing text; it's managing highly customizable workflows, complex relational data (epics, tasks, sub-tasks), and ensuring consistency when multiple people edit a ticket.

* **Data Model & Storage:** A NoSQL database is tempting for flexible schemas, but Jira requires strict relational integrity (Issue A blocks Issue B) and ACID properties for state changes. We'd use a robust RDBMS like **Amazon Aurora (PostgreSQL)**. To handle custom fields per tenant (a common SaaS challenge), we implement an Entity-Attribute-Value (EAV) model or leverage Postgres's native `JSONB` columns for tenant-specific custom attributes while keeping core fields (Status, Assignee) strongly typed.
* **Workflow Engine:** How do we handle custom transitions (e.g., "To Do" -> "In Progress")? We implement a State Machine pattern. The database stores the allowable transition matrix for a specific project's workflow. When a user moves a ticket, a backend service validates the requested state change against this matrix before committing.
* **Concurrency:** If two people edit a ticket at the same time, we use **Optimistic Locking**. We add a `version_number` to the ticket row. When an update is sent, it includes the version the user was looking at. If the DB version has incremented in the meantime, the second user's request fails with a 409 Conflict, prompting them to refresh.

#### 2. Design a Real-Time Collaboration Tool (like Confluence)

**The Deep Dive:** This is all about handling concurrent typing without locking the entire document.

* **Conflict Resolution (CRDTs vs. OT):** We will use **CRDTs (Conflict-free Replicated Data Types)**. Unlike Operational Transformation (OT) which requires a central server to sequence operations, CRDTs assign unique, fractional mathematical indices to every character. If I type 'A' at index 0.5 and you type 'B' at index 0.6, the order is mathematically guaranteed regardless of which order the server receives the packets.
* **Connection Management:** Clients maintain persistent **WebSocket** connections to a fleet of real-time servers. Since WebSockets are stateful, we use an API Gateway that routes connections.
* **State Broadcasting:** When a user types, the CRDT operations are sent via WebSocket to the server, which publishes the event to a Pub/Sub system (like **Amazon ElastiCache with Redis Pub/Sub**). Other real-time servers subscribe to this channel and push the updates down to all other clients currently viewing that specific document ID.

#### 3. Design a Scalable Notification System

**The Deep Dive:** You've dealt with pipeline validation and dead-letter queues before; this system requires exactly that kind of rigor to ensure we don't spam users or drop alerts.

* **Decoupled Architecture:** We use a fan-out pattern. An upstream service (like the Jira workflow engine) fires an event: `TicketAssigned`. This drops into an **Amazon SNS** topic.
* **Queueing & Preferences:** SNS fans out to multiple **SQS** queues (e.g., one for Email, one for In-App, one for SMS). Before sending, a Notification Processor Lambda picks up the SQS message and checks the user's preferences in a fast NoSQL store (DynamoDB). If the user muted email notifications for that project, the message is gracefully dropped.
* **Deduplication & Rate Limiting:** To prevent alert fatigue, we use Redis. Before sending a notification, we check a Redis key `user:{id}:ticket:{id}:recent`. If it exists, we throttle. We also leverage SQS FIFO queues with MessageDeduplicationIds to ensure that if the upstream system retries a failure, the user doesn't get two identical emails.

#### 4. Design a Search System for Knowledge Base (Permission-Aware)

**The Deep Dive:** Standard search is easy (Inverted Index). *Permission-aware* search is incredibly hard because permissions change frequently, and you can't leak the existence of a private document in search results.

* **Search Engine:** We use **Amazon OpenSearch (Elasticsearch)**. Documents are parsed, tokenized, and stored in an inverted index.
* **The Permission Problem:** We use **Query-Time Filtering** via Bitsets. Every document in OpenSearch is tagged with an Access Control List (ACL) ID. When a user queries "deployment plans", the search service first calls an Auth Service to get a list of all group IDs and ACLs the user belongs to.
* **The Execution:** The search query is appended with a massive `FILTER` clause: `MATCH("deployment plans") AND ACL_ID IN (user_acl_list)`. Elasticsearch handles this efficiently by caching the bitsets of these ACL filters.
* **Data Pipeline:** When a document's permissions change, a change-data-capture (CDC) event streams via Kafka/Kinesis to immediately update the document's ACL array in OpenSearch, ensuring near-real-time security compliance.

#### 5. Design an API Gateway

**The Deep Dive:** The gateway is the front door. It must be blazingly fast and highly resilient.

* **Core Responsibilities:** Routing (L7 load balancing), SSL termination, Auth offloading, and Rate Limiting.
* **Auth Offloading:** Instead of every microservice validating JWTs, the Gateway validates the signature of the incoming JWT using a cached public key. It then parses the user ID and tenant ID, appending them as HTTP headers (e.g., `X-User-Id`) before routing to the internal services.
* **Rate Limiting:** We implement a **Token Bucket algorithm** using Redis. We execute a lightweight Lua script on Redis that atomically checks the current token count for a `TenantID_APIKey` and decrements it. If it drops below zero, the Gateway returns an HTTP 429 (Too Many Requests). We run this in an ElastiCache Redis cluster close to the Gateway nodes to keep latency under 5ms.
* **Observability:** The Gateway emits structured logs and distributed tracing headers (like OpenTelemetry) to **Datadog**. This ensures that if a downstream service 500s, we have a unified trace ID from the Gateway all the way down to the database query.

---
