# Experiment 02 — Workload Modeling & Concurrency

## Objective

Understand how JMeter models concurrent users using:

- Number of Threads (Users)
- Ramp-Up Period
- Loop Count

The goal is to understand how workload configuration affects request execution and performance measurements.

---

## Test Scenario

Target API:

```text
GET https://jsonplaceholder.typicode.com/posts/1
```

This experiment uses a public REST API only for learning and JMeter practice.

---

## JMeter Configuration

| Parameter              |      Value |
| ---------------------- | ---------: |
| Threads (Users)        |         10 |
| Ramp-Up Period         | 10 seconds |
| Loop Count             |          1 |
| Total Iterations       |         10 |
| Requests per Iteration |          1 |
| Expected Samples       |         10 |

### Test Plan Structure

```text
Test Plan
└── Thread Group
    └── HTTP Request
        ├── Protocol: https
        ├── Server: jsonplaceholder.typicode.com
        ├── Method: GET
        └── Path: /posts/1
```

---

## Workload Model

The test uses:

```text
10 virtual users
10-second ramp-up
1 iteration per user
```

JMeter gradually starts the users during the ramp-up period rather than starting all users simultaneously.

Conceptually:

```text
Time
│
├── 0s      User 1
├── 1s      User 2
├── 2s      User 3
├── 3s      User 4
├── ...
├── 9s      User 10
│
└── 10s     Ramp-up completed
```

The exact timing can vary because thread scheduling and request execution are not perfectly synchronized.

---

## Expected Request Count

Formula:

```text
Total Requests
=
Number of Threads × Loop Count × Requests per Iteration
```

Therefore:

```text
10 × 1 × 1 = 10 requests
```

Expected:

```text
Sample Count = 10
```

---

## Results

Record the actual result after execution.

| Metric                | Result |
| --------------------- | -----: |
| Sample Count          |     10 |
| Error Count           |        |
| Error %               |        |
| Average Response Time |        |
| Minimum Response Time |        |
| Maximum Response Time |        |
| Throughput            |        |
| Received Bytes        |        |
| Sent Bytes            |        |

### Response Validation

Expected HTTP response:

```text
Response Code: 200
Response Message: OK
```

---

## Observation

### What happened?

Describe what you observed during execution.

Example:

> JMeter executed the test using 10 virtual users with a 10-second ramp-up period. Each virtual user executed the HTTP request once, resulting in approximately 10 samples.

---

## Key Concepts Learned

### 1. Thread

A JMeter thread represents a virtual user.

```text
1 Thread ≈ 1 Virtual User
```

Therefore:

```text
10 Threads ≈ 10 Virtual Users
```

---

### 2. Ramp-Up Period

Ramp-up controls how quickly JMeter starts the configured users.

For this experiment:

```text
Threads = 10
Ramp-Up = 10 seconds
```

Conceptually, JMeter distributes thread startup across the ramp-up period.

A shorter ramp-up creates a more aggressive arrival pattern.

---

### 3. Loop Count

Loop Count controls how many times each virtual user executes the configured test flow.

For this experiment:

```text
Loop Count = 1
```

Therefore each virtual user executes the request once.

---

## QA Interpretation

This experiment demonstrates that performance testing is not simply:

> "Send many requests and check whether the API returns 200."

A performance test must model a realistic workload.

Important workload characteristics include:

- Number of concurrent users
- User arrival rate
- Request frequency
- Think time
- User journey
- Test duration
- Load pattern

---

## Important Learning

A successful HTTP `200` response only confirms that the request was successfully processed.

It does **not** prove that the system can handle production-level traffic.

Performance analysis should consider:

- Response time
- Percentiles
- Throughput
- Error rate
- Concurrent users
- Resource utilization
- SLA/SLO requirements

---

## Presentation Notes

### Simple explanation

> "In JMeter, a Thread represents a virtual user. The Thread Group allows us to control how many virtual users we want, how quickly they should arrive, and how many times they should execute the test."

### Example

If we configure:

```text
Users = 100
Ramp-Up = 10 seconds
```

we are modeling approximately 100 users arriving over a 10-second period.

Changing the ramp-up changes the workload pattern even when the number of users remains the same.

---

## Questions to Think About

1. What happens if we increase Threads from 10 to 100?
2. What happens if Ramp-Up changes from 10 seconds to 1 second?
3. What happens if Loop Count changes from 1 to 10?
4. Does increasing users always increase throughput?
5. What happens to response time as concurrency increases?
6. What is the difference between concurrency and total request count?
7. Why is a single successful request not a performance test?

---

## Result Summary

| Area          | Learning                                   |
| ------------- | ------------------------------------------ |
| Virtual Users | Threads represent virtual users            |
| Concurrency   | Multiple threads can execute concurrently  |
| Ramp-Up       | Controls user arrival/startup pattern      |
| Loop Count    | Controls iterations per user               |
| Sample Count  | Represents executed samples                |
| HTTP 200      | Confirms successful HTTP response          |
| Performance   | Requires workload + measurement + analysis |

---

## Next Experiment

**Experiment 03 — Ramp-Up Comparison**

Compare:

### Test A

```text
Threads: 10
Ramp-Up: 10 seconds
Loop Count: 1
```

### Test B

```text
Threads: 10
Ramp-Up: 1 second
Loop Count: 1
```

The objective is to understand how changing the user arrival pattern affects:

- Response time
- Throughput
- Concurrency
- Server behavior
- Performance characteristics
