# Experiment 01 — First JMeter Test

> **Track:** JMeter Fundamentals  
> **Focus:** HTTP Request Execution & Result Validation  
> **Tool:** Apache JMeter 5.6.3  
> **Test Type:** Basic API Request  
> **Status:** Completed

---

## 1. Objective

The objective of this experiment is to execute the first HTTP request using Apache JMeter and understand the basic JMeter execution flow.

This experiment establishes the foundation for later performance-testing experiments by introducing:

- Test Plan
- Thread Group
- Virtual User
- HTTP Request Sampler
- Request execution
- Response validation
- Basic JMeter metrics
- JMeter result interpretation

The goal is not to perform a meaningful load test yet.

The goal is to understand:

> **How JMeter generates and executes an HTTP request and how the resulting metrics are captured.**

---

# 2. Test Scenario

A simple public REST API was selected as the target system:

```text
https://jsonplaceholder.typicode.com
```

### Endpoint

```text
GET /posts/1
```

### Complete Request

```text
GET https://jsonplaceholder.typicode.com/posts/1
```

The endpoint returns a sample JSON object representing a post.

---

# 3. JMeter Test Plan

The initial test plan contains a Thread Group and an HTTP Request sampler.

```text
Test Plan
└── Thread Group
    └── HTTP Request
```

### Test Plan Configuration

| Configuration           | Value                        |
| ----------------------- | ---------------------------- |
| Virtual Users / Threads | 1                            |
| Ramp-Up Period          | 1 second                     |
| Loop Count              | 1                            |
| HTTP Method             | GET                          |
| Protocol                | HTTPS                        |
| Server                  | jsonplaceholder.typicode.com |
| Path                    | /posts/1                     |

---

# 4. HTTP Request Configuration

The HTTP Request sampler was configured as follows:

```text
Protocol:
https

Server Name or IP:
jsonplaceholder.typicode.com

Method:
GET

Path:
/posts/1
```

### Request Structure

```text
https://jsonplaceholder.typicode.com/posts/1
       └──────────────┬──────────────┘
                    Host

                                  └──────┘
                                    Path
```

---

# 5. Test Execution

The test was executed from the JMeter GUI.

For this initial experiment:

```text
Threads = 1
Ramp-Up = 1 second
Loop Count = 1
```

Therefore, JMeter generated:

```text
1 virtual user
        ↓
1 iteration
        ↓
1 HTTP request
        ↓
1 response
```

Expected sample count:

```text
1
```

---

# 6. Actual Test Result

The request was executed successfully.

### Sampler Result

```text
Thread Name: Thread Group 1-1
Sample Start: 2026-09-01 16:02:12 BDT

Load time: 935 ms
Connect Time: 628 ms
Latency: 925 ms

Size in bytes: 1519
Sent bytes: 137

Headers size in bytes: 1227
Body size in bytes: 292

Sample Count: 1
Error Count: 0

Data type: text

Response code: 200
Response message: OK
```

### Response Metadata

```text
Content-Type:
application/json; charset=utf-8

Data Encoding:
utf-8
```

---

# 7. Response Body

The API returned the following JSON response:

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

---

# 8. Result Analysis

## 8.1 Sample Count

```text
Sample Count = 1
```

Only one HTTP request was executed because the test used:

```text
1 Thread × 1 Loop = 1 Request
```

---

## 8.2 Error Count

```text
Error Count = 0
```

No JMeter-level request error occurred.

The API successfully returned an HTTP response.

---

## 8.3 Response Code

```text
HTTP 200 OK
```

The HTTP `200` response indicates that the request was successfully processed by the target API.

---

## 8.4 Load Time

```text
Load Time = 935 ms
```

Load Time represents the total time JMeter took to complete the sample.

For this experiment, the observed value was:

```text
935 ms
```

This value should **not** yet be interpreted as the application's normal or average performance because only one request was executed.

---

## 8.5 Connect Time

```text
Connect Time = 628 ms
```

Connect Time represents the time associated with establishing the connection to the target server.

The observed value was:

```text
628 ms
```

---

## 8.6 Latency

```text
Latency = 925 ms
```

Latency represents the time until JMeter receives the initial response from the server.

Observed:

```text
925 ms
```

---

## 8.7 Response Size

```text
Total Size = 1519 bytes
Body Size  = 292 bytes
```

The response included both HTTP headers and the response body.

---

# 9. Understanding the Execution Flow

The experiment can be visualized as:

```text
JMeter Test Plan
       │
       ▼
 Thread Group
       │
       ▼
 Virtual User
       │
       ▼
 HTTP Request
       │
       ▼
JSONPlaceholder API
       │
       ▼
 HTTP 200 OK
       │
       ▼
 JMeter captures metrics
       │
       ▼
 Result Analysis
```

This is the fundamental execution model that will be expanded throughout the later experiments.

---

# 10. What This Experiment Proves

This experiment successfully demonstrated that:

- JMeter is installed and operational.
- JMeter can create a virtual user.
- A Thread Group can execute a test flow.
- An HTTP Request sampler can generate an API request.
- JMeter can communicate with an HTTPS endpoint.
- JMeter captures response information.
- JMeter records performance-related metrics.
- JMeter can identify HTTP-level success or failure.

---

# 11. What This Experiment Does NOT Prove

This experiment is **not a performance benchmark**.

A single successful request cannot tell us:

- How many users the API can support
- Maximum throughput
- System capacity
- Behavior under concurrent load
- Response-time distribution
- Performance degradation under load
- Stress limits
- Endurance characteristics
- SLA compliance

For example:

```text
1 request → 200 OK
```

does not mean:

```text
1,000 concurrent users → 200 OK
```

Performance testing requires a properly modeled workload and sufficient test duration.

---

# 12. Key Learning

The most important learning from this experiment is:

> **JMeter is not simply an API request tool. It is a workload-generation and performance-measurement tool.**

At this stage, the HTTP request is only the starting point.

The next experiments will introduce:

```text
Virtual Users
      ↓
Concurrency
      ↓
Ramp-Up
      ↓
Iterations
      ↓
Throughput
      ↓
Response-Time Analysis
      ↓
Load Modeling
```

---

# 13. QA Perspective

From a QA perspective, the first experiment establishes a basic validation loop:

```text
Configure
   ↓
Execute
   ↓
Observe
   ↓
Validate
   ↓
Analyze
```

However, performance testing requires more than functional correctness.

A QA engineer should eventually answer questions such as:

> How does the system behave when multiple users access it simultaneously?

> How quickly does the system respond as load increases?

> At what point does performance begin to degrade?

> What is the system's sustainable throughput?

> Does the system meet the defined SLA/SLO?

These questions will be addressed in subsequent experiments.

---

# 14. Presentation Notes

### Simple explanation

> "This is my first JMeter test. I created a Thread Group with one virtual user and configured an HTTP Request sampler to call a public REST API. The request returned HTTP 200, and JMeter captured metrics such as response time, latency, connection time, and response size."

### Important clarification

> "This is not a performance test yet. It is a baseline execution test that verifies the JMeter environment and establishes how JMeter executes and measures an HTTP request."

---

# 15. Interview / Discussion Questions

### Q1. What is a Thread in JMeter?

A Thread represents a virtual user executing the configured test flow.

---

### Q2. What is a Sampler?

A Sampler generates a request to the target system.

In this experiment, the HTTP Request sampler generated the REST API request.

---

### Q3. What does HTTP 200 mean?

HTTP 200 indicates that the server successfully processed the request.

---

### Q4. Is HTTP 200 enough to say the system performed well?

No.

HTTP 200 indicates functional/request-level success, but performance must be evaluated using metrics such as:

- Response time
- Percentiles
- Throughput
- Error rate
- Concurrency
- Resource utilization

---

### Q5. Why is one request insufficient for performance analysis?

Because one request does not represent realistic workload behavior.

A meaningful performance test requires multiple users, requests, iterations, or sustained traffic depending on the scenario being modeled.

---

# 16. Experiment Summary

| Category         | Result                   |
| ---------------- | ------------------------ |
| Test Type        | Basic HTTP/API execution |
| Target           | JSONPlaceholder          |
| Method           | GET                      |
| Endpoint         | `/posts/1`               |
| Virtual Users    | 1                        |
| Iterations       | 1                        |
| Samples          | 1                        |
| Errors           | 0                        |
| Response Code    | 200                      |
| Response Message | OK                       |
| Load Time        | 935 ms                   |
| Connect Time     | 628 ms                   |
| Latency          | 925 ms                   |
| Status           | Passed                   |

---

# 17. Final Takeaway

This experiment established the fundamental JMeter execution workflow:

```text
Test Plan
   ↓
Thread Group
   ↓
Virtual User
   ↓
HTTP Request
   ↓
Target API
   ↓
Response
   ↓
JMeter Metrics
   ↓
Analysis
```

The next step is to move from **single-user execution** toward **workload modeling and concurrency**.

---

## Next Experiment

**Experiment 02 — Workload Modeling & Concurrency**

The next experiment increases the workload to:

```text
Threads: 10
Ramp-Up: 10 seconds
Loop Count: 1
```

The objective is to understand how JMeter models multiple virtual users and how concurrency changes the test execution.
