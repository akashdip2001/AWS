### SECTION 1: Online Assessment (OA) / Coding & Scripting

1. Write a Python script to parse a 50GB log file and find the top 10 IP addresses making requests.
2. Given a directory structure, write a script to recursively find all files larger than 100MB and older than 30 days.
3. Write a Python script using `boto3` to find and stop all EC2 instances missing a specific tag.
4. Implement a basic rate limiter using a sliding window algorithm in Python.
5. Write a script to ping a list of 1000 URLs concurrently and output the HTTP status codes.
6. Given a string containing brackets `(){}[]`, write a function to determine if the string is valid.
7. Write a bash script using `awk` and `sed` to extract the 4th column of a CSV, remove duplicates, and sort alphabetically.
8. Write a function to implement an LRU (Least Recently Used) cache.
9. How would you merge two massive, sorted log files into a single sorted file without running out of memory?
10. Write a Python script that connects to a REST API, handles pagination, and aggregates a specific JSON field.
11. Implement the "Two Sum" problem using a Hash Map for  time complexity.
12. Write a script that reads `dmesg` output and triggers an alert if the OOM-killer is invoked.
13. Write a Python generator that yields lines from a file matching a specific regex pattern.
14. How would you reverse a linked list? (Rare, but sometimes asked in pure SWE screens).
15. Write a script to continuously monitor CPU usage and write metrics to a DynamoDB table.

### SECTION 2: Linux Systems Internals & Administration

16. Explain the Linux boot process from BIOS/UEFI to the user login prompt.
17. What is an inode? What happens when a disk runs out of inodes but still has physical space?
18. Explain the difference between a hard link and a soft (symbolic) link.
19. What is the difference between a process and a thread in Linux?
20. A server has a high load average, but CPU utilization is low. What is causing this?
21. Walk me through the output of the `top` command. What are `us`, `sy`, `ni`, `id`, and `wa`?
22. How do you find which process is listening on port 8080?
23. What does the `strace` command do, and when would you use it?
24. Explain the difference between `SIGTERM` (15) and `SIGKILL` (9).
25. How does virtual memory work? Explain paging and swapping.
26. You deleted a massive log file, but `df -h` still shows the disk is 100% full. Why, and how do you fix it?
27. What is SELinux, and how does it differ from standard Linux file permissions?
28. Explain the Linux directory structure (`/etc`, `/var`, `/usr`, `/bin`, `/tmp`).
29. How do you configure a cron job to run a script every 5 minutes on weekdays?
30. Explain what zombie and orphan processes are and how to clean them up.
31. How does the OOM (Out of Memory) killer decide which process to kill?
32. Walk me through how you would configure iptables to drop all incoming traffic except SSH and HTTP.
33. What is `systemd` and how do you write a custom service unit file?
34. Explain the concept of file descriptors. What are 0, 1, and 2?
35. How do you change the open file descriptor limit for a specific user?

### SECTION 3: Networking Fundamentals

36. Walk me through the OSI model. Give an example of a protocol at each layer.
37. Explain the TCP 3-way handshake in detail (`SYN`, `SYN-ACK`, `ACK`).
38. What is the difference between TCP and UDP? When would you use UDP over TCP?
39. Walk me through the exact steps of a DNS resolution when I type `amazon.com` into a browser.
40. What is an ARP request, and how does it map IP addresses to MAC addresses?
41. What is the difference between a Layer 4 (Network) and Layer 7 (Application) load balancer?
42. Explain the TLS/SSL handshake process.
43. What is MTU (Maximum Transmission Unit), and what happens if a packet is too large?
44. Explain subnetting. How many usable IP addresses are in a `/24` CIDR block?
45. What is the difference between a public IP, a private IP, and an Elastic IP?
46. Explain NAT (Network Address Translation) and how it works.
47. What is BGP (Border Gateway Protocol) and why is it important for the internet?
48. What is the difference between HTTP/1.1 and HTTP/2?
49. What is ICMP? Why might `ping` fail even if a web server is up and running?
50. Explain the concept of Anycast routing.
51. What is a MAC table on a switch, and how does it differ from a routing table on a router?
52. How does a reverse proxy like Nginx differ from a forward proxy?
53. Explain the concept of SNI (Server Name Indication) in HTTPS.
54. What are the common HTTP status code classes (2xx, 3xx, 4xx, 5xx) and their meanings?
55. How do you use `tcpdump` or Wireshark to capture packets on a specific port?

### SECTION 4: AWS Cloud Architecture & Infrastructure

56. Explain the difference between an AWS Region and an Availability Zone.
57. Describe the components of an AWS VPC (Subnets, Route Tables, IGW, NAT Gateway).
58. What is the difference between a Security Group and a Network ACL (NACL)?
59. Explain the consistency model of Amazon S3.
60. How do IAM Roles differ from IAM Users, and what is the principle of least privilege?
61. What is the difference between an Application Load Balancer (ALB) and a Network Load Balancer (NLB)?
62. How does an Auto Scaling Group determine when to scale in or scale out?
63. Explain the difference between Amazon RDS and Amazon DynamoDB.
64. How do you securely grant an EC2 instance access to an S3 bucket without hardcoding access keys?
65. What is the purpose of an S3 VPC Endpoint?
66. Explain how AWS Lambda cold starts work and how to mitigate them.
67. What is Amazon EventBridge, and how does it enable event-driven architecture?
68. Describe the difference between Amazon SQS and Amazon SNS.
69. How does Amazon MSK (Kafka) handle message ordering and consumer groups?
70. What is a Dead Letter Queue (DLQ), and why is it essential in distributed systems?
71. Explain AWS Transit Gateway vs. VPC Peering.
72. How do you encrypt data at rest in EBS and S3 using AWS KMS?
73. What is the difference between DynamoDB Provisioned capacity and On-Demand capacity?
74. How does AWS CloudFront caching work?
75. What are the different S3 storage classes, and when would you use Glacier vs. Standard?

### SECTION 5: DevOps, CI/CD, & IaC

76. Explain the concept of Infrastructure as Code (IaC). What problem does it solve?
77. What is the Terraform state file, and why should it be stored remotely (e.g., in S3)?
78. Explain the difference between continuous integration, continuous delivery, and continuous deployment.
79. What is a Docker image vs. a Docker container?
80. Explain Docker layering and how to optimize a Dockerfile to reduce image size.
81. How do you manage secrets (API keys, passwords) securely in a CI/CD pipeline?
82. Explain Blue/Green deployment vs. Canary deployment.
83. What is immutable infrastructure?
84. How do GitHub Actions workflows authenticate securely to AWS?
85. What is the difference between a virtual machine and a container?

### SECTION 6: System Design & Scalability

86. Design a log aggregation system for thousands of EC2 instances.
87. How would you design a URL shortener (like bit.ly)?
88. Explain horizontal vs. vertical scaling. When would you use each?
89. How do you design a system to handle a sudden traffic spike (e.g., Black Friday sale)?
90. Explain the concept of decoupling in distributed systems.
91. What is the role of a caching layer (like Redis or Memcached) in a web application?
92. Design an architecture to ingest and process millions of IoT telemetry events per minute.
93. Explain CAP Theorem and how it applies to databases.
94. How do you handle database migrations with zero downtime?
95. Design a rate-limiting service to protect an API.

### SECTION 7: Troubleshooting Scenarios (The SysDE Core)

96. "I'm getting an HTTP 502 Bad Gateway error on my web app." Walk me through your troubleshooting steps.
97. "I cannot SSH into my EC2 instance." List every possible reason from the local machine to the OS.
98. "My Lambda function is intermittently timing out after 3 seconds." How do you debug this?
99. "The database is experiencing high latency." What metrics do you check first?
100. "An EC2 instance in a private subnet cannot reach the internet to download a package." How do you fix it?
101. A Python application running on a server suddenly crashes with a memory error. How do you find the root cause?
102. A developer complains their code deploys fine to Dev but fails in Production. What do you check?
103. "We are seeing intermittent packet loss between two EC2 instances." How do you trace this?
104. How do you troubleshoot a system where CPU is at 100% but `top` shows no obvious offending process?
105. "A website is loading extremely slowly, but only for users in Europe." What is your approach?

### SECTION 8: HR & Behavioral (Amazon Leadership Principles)

*Note: Use the STAR method (Situation, Task, Action, Result) for all of these.*
106. **Customer Obsession:** Tell me about a time you went above and beyond for a customer or internal stakeholder.
107. **Ownership:** Tell me about a time you took on a task that was completely outside your job description.
108. **Invent and Simplify:** Tell me about a complex process you automated or simplified to save time.
109. **Are Right, A Lot:** Tell me about a time you made a decision with incomplete data. What was the outcome?
110. **Learn and Be Curious:** Describe a time you had to quickly learn a new technology to solve a problem.
111. **Hire and Develop the Best:** (Usually reserved for L5+, but you may be asked how you mentored a peer or classmate).
112. **Insist on Highest Standards:** Tell me about a time you refused to compromise on quality, even under a tight deadline.
113. **Think Big:** Tell me about a time you proposed a radical, large-scale solution to a systemic problem.
114. **Bias for Action:** Tell me about a time you had to act immediately to fix a critical issue without waiting for approval.
115. **Frugality:** Tell me about a time you reduced infrastructure costs or optimized resource usage.
116. **Earn Trust:** Tell me about a time you made a significant mistake. How did you handle it and communicate it?
117. **Dive Deep:** Walk me through the most complex bug you ever root-caused.
118. **Have Backbone; Disagree and Commit:** Tell me about a time you strongly disagreed with a manager or senior engineer's technical approach.
119. **Deliver Results:** Tell me about a project that was falling behind schedule. How did you ensure it was delivered on time?
120. **Strive to be Earth's Best Employer / Success and Scale Bring Broad Responsibility:** Tell me about a time you improved the safety, security, or operational environment for your team.
