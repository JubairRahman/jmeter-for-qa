# JMeter Experiments

> A collection of practical, hands-on Apache JMeter experiments focused on API performance testing, workload modeling, test execution, result analysis, and real-world QA practices.

---

## Purpose

This directory contains the practical experiments performed while learning and applying Apache JMeter.

Each experiment is designed to answer three questions:

1. **What are we testing?**
2. **How do we configure it in JMeter?**
3. **What did we learn from the results?**

The experiments progressively move from basic JMeter execution to realistic performance-testing scenarios.

---

## Experiment Roadmap

| #   | Experiment                                                               | Primary Focus                  | Status         |
| --- | ------------------------------------------------------------------------ | ------------------------------ | -------------- |
| 01  | [First JMeter Test](./01-first-jmeter-test.md)                           | HTTP Request & Basic Execution | ✅ Completed   |
| 02  | [Workload Modeling & Concurrency](./02-workload-modeling-concurrency.md) | Virtual Users & Concurrency    | 🔄 In Progress |
| 03  | Ramp-Up Comparison                                                       | User Arrival Pattern           | ⏳ Planned     |
| 04  | Loop Count & Iterations                                                  | Request Volume                 | ⏳ Planned     |
| 05  | Increasing Load                                                          | Load Behavior                  | ⏳ Planned     |

---

# Learning Progression

The experiments follow a progressive workload model.

```text
Single Request
      │
      ▼
Multiple Virtual Users
      │
      ▼
Concurrency
      │
      ▼
Ramp-Up
      │
      ▼
Iterations
      │
      ▼
Increasing Load
      │
      ▼
Performance Analysis
      │
      ▼
Real-World Performance Testing
```

The objective is to understand **why workload configuration matters**, rather than simply learning where JMeter components are located in the GUI.

---

# Experiment Documentation Standard

Each experiment follows a consistent documentation structure.

### 1. Objective

What concept or JMeter capability are we trying to understand?

### 2. Test Scenario

What system, API, or workflow are we testing?

### 3. JMeter Configuration

What Thread Group, Sampler, Controller, Timer, Assertion, or other components are being used?

### 4. Workload Model

How many users, iterations, requests, and what arrival pattern are being simulated?

### 5. Test Execution

How was the test executed?

### 6. Actual Results

What did JMeter report?

### 7. Result Analysis

What do the metrics actually mean?

### 8. QA Interpretation

What does the result tell us from a QA/performance-testing perspective?

### 9. Key Learning

What was learned from the experiment?

### 10. Next Experiment

What concept will be investigated next?

---

# Result Philosophy

A performance-testing result should never be evaluated using HTTP status code alone.

For example:

```text
HTTP 200
```

only indicates that the request was successfully processed.

Performance analysis should consider metrics such as:

```text
Response Time
Latency
Throughput
Error Rate
Percentiles
Concurrency
Request Rate
Resource Utilization
SLA / SLO
```

The experiments will progressively introduce these concepts.

---

# Test Environment

The experiments are currently being performed using:

| Component        | Environment                    |
| ---------------- | ------------------------------ |
| Apache JMeter    | 5.6.3                          |
| Java             | Temurin 17                     |
| Operating System | macOS                          |
| Architecture     | x86_64                         |
| Test Type        | API / HTTP Performance Testing |
| Primary Tool     | Apache JMeter                  |

---

# Target API

Early experiments use:

```text
JSONPlaceholder
https://jsonplaceholder.typicode.com
```

Example endpoint:

```text
GET /posts/1
```

JSONPlaceholder is used as a safe learning target for basic API and JMeter experimentation.

---

# Important Note

These experiments are primarily intended for **learning and demonstration purposes**.

A production performance test should use:

- An authorized target environment
- Realistic workload models
- Appropriate test data
- Defined performance requirements
- Monitoring and observability
- Clearly defined SLAs/SLOs
- Appropriate test duration
- Infrastructure/resource monitoring

Never perform load or stress testing against systems without proper authorization.

---

# How to Use This Directory

If you are learning JMeter from the beginning, follow the experiments in order:

```text
01 → 02 → 03 → 04 → 05 → ...
```

Each experiment builds on concepts introduced earlier.

For the theoretical explanation of JMeter components and performance-testing concepts, refer to:

**[JMeter Master Guide](../JMETER_MASTER_GUIDE.md)**

For the overall learning roadmap, refer to:

**[JMeter Roadmap](../../ROADMAP.md)**

---

# Current Progress

### Completed

- [x] JMeter environment setup
- [x] First HTTP/API request
- [x] Basic response validation
- [x] Basic JMeter metrics
- [x] Experiment 01 documentation

### In Progress

- [ ] Workload modeling
- [ ] Concurrent virtual users
- [ ] Ramp-up behavior

### Upcoming

- [ ] Ramp-up comparison
- [ ] Loop count and iterations
- [ ] Increasing workload
- [ ] Timers and think time
- [ ] Parameterization
- [ ] Assertions
- [ ] Correlation
- [ ] Load testing
- [ ] Stress testing
- [ ] Result analysis
- [ ] Percentile analysis
- [ ] CLI execution
- [ ] HTML reporting
- [ ] Automation
- [ ] CI/CD integration

---

## Learning Principle

> **Don't learn JMeter as a collection of GUI components. Learn it as a system for modeling workload, generating traffic, validating behavior, measuring performance, and analyzing results.**
