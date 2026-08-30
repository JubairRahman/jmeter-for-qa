# JMeter for QA Engineers — Learning Roadmap

## 🎯 Objective

Build practical competency in Apache JMeter and performance engineering, progressing from fundamentals to real-world performance test design, execution, analysis, and automation.

---

## 📚 Documentation

- [Learning Roadmap](ROADMAP.md)
- [Changelog](CHANGELOG.md)
- [Contributing Guide](CONTRIBUTING.md)

---

## 01 — Performance Testing Foundations & JMeter Architecture

### Concepts

* Performance testing fundamentals
* Functional vs performance testing
* Load testing
* Stress testing
* Spike testing
* Endurance/soak testing
* Volume testing
* Capacity testing
* JMeter architecture
* Test Plan
* Thread Group
* Samplers
* Controllers
* Listeners
* Configuration Elements
* Timers
* Assertions

### Practical Outcomes

* Install and configure JMeter
* Create a basic Test Plan
* Configure virtual users
* Execute a basic HTTP test
* Understand JMeter execution flow

---

## 02 — HTTP/API Performance Engineering

* HTTP fundamentals
* REST APIs
* HTTP methods
* Status codes
* Headers
* Query parameters
* Path parameters
* Request bodies
* JSON
* Content types
* HTTP Request sampler
* HTTP Header Manager
* HTTP Request Defaults
* API workflow modeling

### Practical Outcome

Build a multi-request API performance scenario.

---

## 03 — Test Data Parameterization & Correlation

* JMeter variables
* User-defined variables
* CSV Data Set Config
* Parameterization
* Dynamic test data
* Correlation
* Extractors
* JSON Extractor
* Regular Expression Extractor
* JSONPath
* Variable reuse

### Practical Outcome

Build a dynamic API workflow using external test data and extracted values.

---

## 04 — Assertions, Authentication & Session Management

* Response assertions
* JSON assertions
* HTTP status validation
* Authentication
* Basic authentication
* Token-based authentication
* Bearer tokens
* Cookies
* Sessions
* Authorization headers
* Authentication workflows

### Practical Outcome

Build an authenticated performance test scenario.

---

## 05 — Workload Modeling & Performance Test Design

* Virtual users
* Concurrency
* Ramp-up
* Ramp-down
* Iterations
* Duration
* Think time
* Throughput control
* Workload models
* Baseline testing
* Load testing
* Stress testing
* Spike testing
* Endurance testing
* Capacity testing

### Practical Outcome

Design multiple workload profiles for the same application.

---

## 06 — Performance Metrics & Bottleneck Analysis

* Response time
* Latency
* Throughput
* Requests per second
* Error rate
* Percentiles
* Median
* 90th percentile
* 95th percentile
* 99th percentile
* Concurrent users
* Saturation
* Performance degradation
* Bottleneck analysis
* Result interpretation

### Practical Outcome

Analyze performance results and identify potential bottlenecks.

---

## 07 — CLI Execution, Automation & CI/CD

* Non-GUI execution
* JMeter CLI
* Test result files
* HTML reports
* Command-line parameters
* Environment configuration
* Git integration
* CI/CD fundamentals
* GitHub Actions
* Jenkins

### Practical Outcome

Execute a JMeter test automatically from the command line and CI/CD pipeline.

---

## 08 — Advanced JMeter & Scripting

* JMeter functions
* JSR223
* Groovy
* Advanced correlation
* Custom logic
* Advanced controllers
* Performance optimization
* Distributed testing
* Remote execution
* Load generator considerations

### Practical Outcome

Implement advanced test logic and understand distributed load generation.

---

## 09 — Real-World Performance Testing Project

Build an end-to-end performance testing project covering:

```text
Requirements
    ↓
Workload Model
    ↓
Test Data
    ↓
Test Scenario
    ↓
JMeter Test Plan
    ↓
Baseline
    ↓
Load Test
    ↓
Stress Test
    ↓
Result Analysis
    ↓
Performance Report
```

---

## 10 — Performance Engineering Practices

* Test strategy
* Test planning
* Performance acceptance criteria
* Environment readiness
* Data preparation
* Monitoring
* Test execution strategy
* Result interpretation
* Reporting
* Troubleshooting
* Common anti-patterns
* Best practices
* Interview preparation

---

## 🏆 Final Competency

By completing this roadmap, a QA Engineer should be able to:

> Design, implement, execute, analyze, and automate API performance tests using Apache JMeter, including workload modeling, parameterization, correlation, authentication, load/stress testing, reporting, CLI execution, and CI/CD integration.
