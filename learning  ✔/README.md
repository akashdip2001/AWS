Here are the top 5 "Super-Node" questions from beginner to super-advanced. Mastering these 5 scenarios covers about 50 standard interview questions.

---

### Level 1: The Core Systems Foundation (Linux & Networking)

This tests your fundamental understanding of how traffic actually reaches a server, expanding on your Apple infrastructure training.

**Q1: "A user types amazon.com into their browser, and it routes to your Nginx server. Walk me through the exact journey of that request from the DNS resolution to the Nginx worker process."**

* **Domain Coverage:** DNS, OSI Layer 3/4 (TCP/IP), Layer 7 (HTTP), Linux processes.
* **The 'Smart' Connection:** You must explain the DNS lookup (A-records), the TCP 3-way handshake (`SYN`, `SYN-ACK`, `ACK`), how the Linux kernel accepts the connection on Port 443, and how the Nginx master process hands the connection to a worker process.

---

### Level 2: The Coding OA (Applied Python & DSA)

This is exactly what you will face in the pre-interview Hackerrank round.

**Q2: "You have a 50GB Nginx `access.log` file. Write a Python script to find the top 3 IP addresses that are causing '500 Internal Server Error' responses. You cannot load the whole file into memory."**

* **Domain Coverage:** Python scripting, File I/O, Time/Space Complexity, Hash Maps (Dictionaries).
* **The 'Smart' Connection:** This proves you understand DSA without doing LeetCode. You must read the file line-by-line (to keep space complexity at ) and use a Python dictionary to count occurrences (keeping time complexity at ). You then sort the dictionary keys by value.

---

### Level 3: DevOps & CI/CD Automation

This targets the Alexa Connections role requirements and your daily work.

**Q3: "Your GitHub Actions pipeline is attempting to deploy a new Docker container to AWS Elastic Container Registry (ECR). The pipeline fails with an 'Unauthorized' error, but it worked yesterday. Walk me through your troubleshooting steps."**

* **Domain Coverage:** CI/CD pipelines, Docker, AWS IAM, OIDC (OpenID Connect).
* **The 'Smart' Connection:** You must connect pipeline automation to cloud security. You would check if the IAM Role trust policy used by GitHub Actions was modified, check if the temporary STS (Security Token Service) token expired, and verify the IAM policy attached to the role actually has `ecr:GetAuthorizationToken` and `ecr:BatchCheckLayerAvailability` permissions.

---

### Level 4: Enterprise Cloud Architecture

This is tailored to your ODIE data pipeline experience and the ICON SysDE role.

**Q4: "We are ingesting 10,000 IoT telemetry messages per second into Amazon MSK (Kafka). An AWS Lambda function consumes these messages and writes them to DynamoDB. Suddenly, the Lambda function starts dropping messages and timing out. How do you architecturally fix this bottleneck?"**

* **Domain Coverage:** AWS Serverless, Distributed Systems, Event-Driven Architecture, Observability.
* **The 'Smart' Connection:** This tests your ability to scale. You would first check CloudWatch metrics for Lambda concurrency limits and DynamoDB Write Capacity Units (WCU) throttling. To fix it, you would discuss batching the Kafka records, increasing the Lambda memory (which proportionally increases CPU), or implementing a Dead Letter Queue (DLQ) in EventBridge so failed messages aren't lost forever.

---

### Level 5: Super Advanced System Design (The Bar Raiser)

This tests if you can think like a Senior Engineer.

**Q5: "Our API is getting hit by a massive DDoS attack from thousands of different IPs. We need you to write a custom Rate Limiter in Python to sit in front of the application. How do you design it?"**

* **Domain Coverage:** System Design, Advanced Python, Security, DSA (Queues/Hash Maps).
* **The 'Smart' Connection:** You would combine DSA with system architecture. You would explain the "Token Bucket" or "Sliding Window" algorithm. In Python, you would use a Dictionary where the Key is the IP address, and the Value is a queue of timestamps. If the length of the queue exceeds 100 requests in the last 60 seconds, your code drops the packet and returns an HTTP 429 (Too Many Requests).

---

# 🔑 Here are the 5 "Super-Node" text diagrams mapping out the exact architecture, bottlenecks, and data flows for those scenarios.

---

### Level 1: The Request Journey (DNS, Linux & Nginx)

**The Scenario:** A browser request hitting your Nginx server.
**The Interviewer Trap:** They want to see if you skip straight to Nginx or if you understand the underlying Linux networking stack.

```text
[User Browser]
      │
      ├── 1. DNS Query (amazon.com) ──> [Route 53 / DNS] (Returns IP: 203.0.113.1)
      │
      ├── 2. TCP Handshake (SYN -> SYN/ACK -> ACK) ──> [AWS Security Group (Port 443)]
      │                                                       │
      └── 3. HTTP GET Request (Encrypted) ─────────────> [Linux Kernel Stack]
                                                              │ (Binds to Port 443)
                                                              v
                                                 [Nginx Master Process (Root)]
                                                              │ (Delegates task)
                                            ┌─────────────────┴─────────────────┐
                                            v                                   v
                                [Worker Process 1 (nginx user)]       [Worker Process 2]
                                 (Reads file: 200 OK)                  (Idle)

```

---

### Level 2: The Coding OA (Python Log Parsing)

**The Scenario:** Parsing a 50GB log file for top errors without crashing the server.
**The Interviewer Trap:** If you use `logs = file.read()` or `logs = file.readlines()`, you fail. That loads 50GB into RAM and crashes the machine. You must use a generator (reading line-by-line).

```text
[50GB access.log on Disk]
      │
      │  (1. Read line-by-line using: 'with open(file) as f: for line in f:')
      │  (Space Complexity: O(1) - Only 1 line in memory at a time)
      v
[Python Script Execution]
      │
      │  (2. Regex/Split checks if line contains "500")
      │  (3. If yes, extract IP and update Hash Map)
      v
[Hash Map / Python Dictionary] 
      │  {
      │    "192.168.1.10": 450,
      │    "10.0.0.5": 112,
      │    "172.16.0.4": 89
      │  }
      │
      │  (4. Sort dictionary by values descending)
      v
[Output: Top 3 Offending IPs]

```

---

### Level 3: DevOps & CI/CD Security

**The Scenario:** GitHub Actions pipeline failing with an 'Unauthorized' error pushing to AWS ECR.
**The Interviewer Trap:** They want to know if you understand *how* systems authenticate. Hardcoding AWS keys in GitHub secrets is an anti-pattern. You should be using OIDC (OpenID Connect).

```text
[Developer Push] ──> [GitHub Actions Runner]
                           │
                           ├── 1. Auth Request ──> [AWS IAM (OIDC Identity Provider)]
                           │                            │ (Validates repo & branch)
                           │                            v
                           ├── 2. Temp Token <──── [AWS STS (Security Token Service)]
                           │
                           └── 3. docker push ───> [AWS ECR (Container Registry)]
                                                        │
                                                        ├── [IAM Policy Check]
                                                        │   (Requires: ecr:GetAuthorizationToken)
                                                        │   (Requires: ecr:BatchCheckLayerAvailability)
                                                        v
                                                 [Push Success / Fail]

```

---

### Level 4: Enterprise Serverless Architecture

**The Scenario:** Kafka (MSK) to Lambda to DynamoDB pipeline is dropping messages.
**The Interviewer Trap:** Identifying the bottleneck. Is DynamoDB rejecting writes, or is Lambda not scaling fast enough? You must introduce a Dead Letter Queue (DLQ) to save the dropped data.

```text
[IoT Devices] ──> (10k msgs/sec)
                       │
                       v
             [Amazon MSK (Kafka)] 
                       │
                       ├──> [AWS Lambda Consumer] ──> (Write) ──> [DynamoDB]
                       │      ^ (Bottleneck: CPU/Memory limit)      ^ (Bottleneck: WCU Limit)
                       │
             (If Lambda fails 3 times)
                       │
                       v
             [EventBridge / SQS]
               (Dead Letter Queue)
               (Saves failed data for retry)

```

---

### Level 5: System Design (Rate Limiter)

**The Scenario:** Writing a Rate Limiter to stop a DDoS attack (Sliding Window Algorithm).
**The Interviewer Trap:** How do you track timestamps efficiently without running out of memory? You use a dictionary where the key is the IP, and the value is a Queue (or list) of request timestamps.

```text
[Attacker IPs] ──> [AWS API Gateway / Load Balancer]
                                │
                                v
                       [Rate Limiter Logic]
                                │
             (Check IP in Dictionary Hash Map) 
             {
               "Attacker_IP_1": [10:01:00, 10:01:02, 10:01:05...],
               "Normal_User_IP": [10:01:04]
             }
                                │
                 [Are there > 100 timestamps in the last 60 seconds?]
                   /                                           \
                 YES                                            NO
                 /                                               \
      [Drop Packet]                                   [Allow Request]
      (Return HTTP 429 Too Many Requests)             (Route to Backend App)

```

---
