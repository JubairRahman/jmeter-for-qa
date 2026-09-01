# Apache JMeter — Master Guide for QA Engineers

<p align="center">

  <img src="https://jmeter.apache.org/images/logo.svg" alt="Apache JMeter" width="180"/>

</p>

<p align="center">

<strong>A practical, hands-on guide to API and Performance Testing with Apache JMeter.</strong>

</p>

<p align="center">

  <img src="https://img.shields.io/badge/Apache%20JMeter-5.6.3-D22128?logo=apachejmeter&logoColor=white" alt="JMeter Version"/>

  <img src="https://img.shields.io/badge/Java-17-ED8B00?logo=openjdk&logoColor=white" alt="Java 17"/>

  <img src="https://img.shields.io/badge/Platform-macOS-000000?logo=apple&logoColor=white" alt="macOS"/>

  <img src="https://img.shields.io/badge/Focus-QA%20%7C%20Performance%20Testing-0A66C2" alt="QA Performance Testing"/>

  <img src="https://img.shields.io/badge/Status-Learning%20%7C%20Active-2EA44F" alt="Status"/>

</p>

---

## 📖 About This Guide

This is a practical and continuously evolving learning guide for **QA Engineers who want to understand and apply Apache JMeter for performance and API testing**.

The objective is not simply to learn where JMeter's buttons are.

The objective is to understand:

- How performance testing works
- How workloads are designed
- How JMeter models virtual users
- How API requests are generated
- How test data is managed
- How authentication and correlation work
- How load and stress tests are designed
- How performance results are analyzed
- How performance bottlenecks are identified
- How JMeter tests can be automated
- How performance testing can be integrated into CI/CD

> **Learn → Understand → Practice → Analyze → Document → Present**

---

## 🎯 Purpose

This document serves as the **single source of truth** for the JMeter learning journey in the [`jmeter-for-qa`](../) repository.

It has three primary purposes:

### 1. 🧠 Personal Learning

A structured notebook containing concepts, examples, experiments, observations, and lessons learned while mastering JMeter.

### 2. 🌎 Open-Source Learning Resource

A practical reference that other QA Engineers can use to learn JMeter and performance testing.

### 3. 🎤 Training & Presentation Reference

A concise source of presentation notes, QA perspectives, examples, and discussion points for knowledge-sharing sessions.

---

# 🧭 How to Use This Guide

Each major topic follows a consistent learning cycle:

```text
Concept
   ↓
Why It Matters
   ↓
Real-World Example
   ↓
JMeter Implementation
   ↓
Hands-on Exercise
   ↓
Result Analysis
   ↓
QA Perspective
   ↓
Presentation Notes
   ↓
Interview / Discussion Questions
   ↓
Key Takeaways
```

# ⚡ Performance Testing Foundations

> ![In Progress](https://img.shields.io/badge/Status-In%20Progress-yellow?style=for-the-badge&logo=clock)

---

## 1.1 What is Performance Testing?

**Performance testing** evaluates how a system behaves under a defined workload.

### 🎯 Key Focus Areas

It focuses on essential system characteristics such as:

- ⏱️ **Response time**
- 🚀 **Throughput**
- 👥 **Concurrency**
- ⚠️ **Error rate**
- 💻 **Resource utilization**
- 📈 **Scalability**
- 🛡️ **Stability**
- 📦 **Capacity**

---

> 💡 **Core Concept:**  
> Performance testing is **not** simply about determining whether an API returns `HTTP 200`.  
> It asks a broader question:  
> **"How does the system behave when subjected to a defined workload?"**

---

## 🔍 Practical Example

Consider the following endpoint:
`GET /api/patients`

---

### 🧪 Functional Test vs. ⚡ Performance Test

| 🟢 Functional Test (Verifies Correctness)                    | ⚡ Performance Test (Verifies Capability)                    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| • **HTTP Status** = `200 OK`                                 | • Can the API handle **100 concurrent users**?               |
| • **Payload validation** (Expected patient data is returned) | • Is the **P95 response time** below the agreed threshold?   |
|                                                              | • Does the **error rate** remain within acceptable limits?   |
|                                                              | • How does performance change as the **workload increases**? |

---

## 1.2 Functional Testing vs Performance Testing

| 🟢 Functional Testing                   | ⚡ Performance Testing                        |
| :-------------------------------------- | :-------------------------------------------- |
| **Does the feature work?**              | **How well does the system perform?**         |
| Focuses on **correctness**              | Focuses on **system behavior under workload** |
| Validates **expected functionality**    | Measures **performance characteristics**      |
| _Example:_ `HTTP 200`                   | _Example:_ `P95 < defined threshold`          |
| Usually uses **normal/small workloads** | Uses **controlled workloads**                 |

---

### 🔑 Key Principle

> ⚠️ **A successful response does not automatically mean good performance.**

```http
HTTP 200 OK
Response Time = 5 seconds
```

## 1.3 Core Performance Testing Metrics

### 👤 Virtual User (VU)

A **Virtual User (VU)** is a simulated user generated by a performance-testing tool.

In **JMeter**, virtual users are commonly represented by **threads** within a **Thread Group**.

> 📌 **Example:**  
> `Threads = 100`  
> Configures **100 JMeter threads**. The actual concurrency and request rate depend on test design, timing, controllers, and application behavior.

---

### 🔀 Concurrency

**Concurrency** represents activities or users that are active at approximately the same time.

> ⚠️ **Important Distinction:**  
> `100 concurrent users` should **not** automatically be interpreted as `100 requests per second`.  
> _These are two fundamentally different concepts._

---

### ⏱️ Response Time

**Response time** represents the elapsed time measured for a request or operation.

> 📌 **Example:**  
> `Response Time = 350 ms`

---

> 💡 **Best Practice:**  
> Response time should normally be **analyzed across multiple samples** rather than evaluated from a single request.

---

### 🚀 Throughput

**Throughput** represents the amount of work processed over a given period of time.

For HTTP performance testing, throughput is commonly expressed using the following badge unit:

![Requests Per Second](https://img.shields.io/badge/Unit-requests%2Fsecond-blue?style=flat-square&logo=speedtest)

> 📌 **Example:**  
> `250 requests/sec`

---

### ⚠️ Error Rate

**Error rate** represents the proportion of failed requests or samples within the observed test results.

#### 📊 Calculation Breakdown

- **Total Requests:** `10,000`
- **Failed Requests:** `150`

$$\text{Error Rate} = \left(\frac{150}{10,000}\right) \times 100 = 1.5\%$$

---

> 🎯 **Acceptance Criteria:**  
> The acceptable error threshold should always be derived from **application requirements**, **SLA/SLO**, or predefined **test acceptance criteria**.

---

### 📊 Percentiles

**Percentiles** describe the distribution of response times across your test dataset.

#### 📈 Example Metrics

| Metric  | Value     |
| :------ | :-------- |
| **P50** | `300 ms`  |
| **P90** | `500 ms`  |
| **P95** | `700 ms`  |
| **P99** | `1.8 sec` |

#### 🔍 Interpretation

- 🔹 **P50:** `50%` of observed requests completed at or below **300 ms**.
- 🔹 **P90:** `90%` of observed requests completed at or below **500 ms**.
- 🔹 **P95:** `95%` of observed requests completed at or below **700 ms**.
- 🔹 **P99:** `99%` of observed requests completed at or below **1.8 seconds**.

---

> 💡 **Why Use Percentiles?**  
> Percentiles are often far more informative than **averages** because average calculations tend to hide significant latency spikes and slow requests.

---

## 🎤 Short Summary

> 📢 **Key Takeaway:**  
> "Performance testing evaluates how a system behaves under a defined workload. Unlike functional testing, where we primarily verify whether a feature works correctly, performance testing evaluates characteristics such as **response time**, **throughput**, **concurrency**, **error rate**, **scalability**, and **stability**. A successful HTTP response alone doesn't prove that the system performs well."

---

## 💬 Discussion Questions

### ❓ Q1: Is `HTTP 200` enough to say the performance test passed?

> ❌ **Answer: No.**

`HTTP 200` merely indicates a successful HTTP response. Performance acceptance also depends on critical metrics and predefined requirements, such as:

- ⏱️ Response-time thresholds
- 🚀 Throughput
- ⚠️ Error rates
- 💻 Resource utilization and system behavior

---

### ❓ Q2: Is 100 virtual users the same as 100 requests per second?

> ❌ **Answer: No.**

- **Virtual Users (VUs):** Represent simulated active users or concurrent threads.
- **Requests Per Second (RPS):** Represents the actual request throughput processed by the server.

The relationship between VUs and RPS depends entirely on user behavior, request frequency, timers, logic controllers, and system response times.

---

### ❓ Q3: Why use P95 instead of only average response time?

> 💡 **Answer:**

Average response time can mask latency spikes and hide slow requests. **P95** provides clear visibility into the upper distribution of response times (the 95th percentile), making it far more effective for evaluating real-world user experience and performance SLAs.

---

## 📌 Key Takeaways

┌────────────────────────────────────────────────────────────────────────┐
│ SUMMARY OF CORE PRINCIPLES │
└────────────────────────────────────────────────────────────────────────┘

- ⚡ **Workload Evaluation:** Performance testing evaluates system behavior under workload.
- 🎯 **Scope Separation:** Functional correctness and performance are different concerns.
- 👥 **Metric Distinction:** Virtual users and requests per second are **not** the same metric.
- ⏱️ **Sample Depth:** Response time should always be analyzed across multiple samples.
- 🚀 **Work Rate:** Throughput describes the volume of work processed over time.
- ⚠️ **Failure Ratio:** Error rate measures failed requests/samples relative to total observations.
- 📈 **Tail Latency Visibility:** Percentiles such as **P95** and **P99** help expose slow responses.
- 🎯 **Requirement Alignment:** Performance acceptance must always be based on defined requirements.

---

# 🏗️ 2. JMeter Architecture

![Status](https://img.shields.io/badge/Status-In%20Progress-F59E0B?style=for-the-badge)
![JMeter](https://img.shields.io/badge/Apache%20JMeter-Performance%20Testing-D22128?style=for-the-badge&logo=apachejmeter&logoColor=white)
![Level](https://img.shields.io/badge/Level-Intermediate-6366F1?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Architecture-0EA5E9?style=for-the-badge)

> 🧠 **Goal:** Build a clear mental model of how JMeter test elements work together to simulate virtual users and produce measurable performance results.

---

## 📚 2.1 JMeter Mental Model

A basic JMeter test can be understood as a hierarchy of components where each element has a specific responsibility.

### 🔷 High-Level Architecture

```text
                         ┌─────────────────────┐
                         │     TEST PLAN       │
                         │   Overall Test      │
                         │    Definition       │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    THREAD GROUP     │
                         │ Virtual User Model  │
                         └──────────┬──────────┘
                                    │
                       ┌────────────┴────────────┐
                       │                         │
                       ▼                         ▼
              ┌─────────────────┐       ┌─────────────────┐
              │     SAMPLER     │       │    CONTROLLER   │
              │  Sends Request  │       │ Controls Flow   │
              └────────┬────────┘       └────────┬────────┘
                       │                         │
                       └────────────┬────────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │       TIMER        │
                         │   Controls Timing  │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │     ASSERTION       │
                         │  Validates Result   │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │       RESULT        │
                         │ Metrics & Outcome   │
                         └─────────────────────┘
```

### 🧩 Component Responsibilities

| Component           | Responsibility                                                |
| ------------------- | ------------------------------------------------------------- |
| 📋 **Test Plan**    | Defines the overall performance test                          |
| 👥 **Thread Group** | Defines virtual users and their execution behavior            |
| 🎯 **Sampler**      | Sends requests to the target system                           |
| 🔀 **Controller**   | Controls execution flow and request logic                     |
| ⏱️ **Timer**        | Introduces delays between requests                            |
| ✅ **Assertion**    | Validates whether a response meets expectations               |
| 📊 **Result**       | Captures response time, throughput, errors, and other metrics |

> 💡 **Mental Model:**
> **Test Plan → Users → Flow → Requests → Timing → Validation → Results**

---

# 📋 2.2 Test Plan

The **Test Plan** is the top-level container of a JMeter test.

It defines the overall structure of the performance test and can contain one or more **Thread Groups** along with their associated test elements.

### 🏛️ Example Structure

```text
Test Plan
│
├── 👥 Login Scenario
│
├── 🔎 Patient Search Scenario
│
└── ✏️ Patient Update Scenario
```

### 🎯 Think of It Like This

The Test Plan represents the **overall definition of the performance test**.

For example, a healthcare application performance test might contain:

```text
                    📋 TEST PLAN
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
       🔐 Login       🔎 Search       ✏️ Update
       Scenario       Scenario       Scenario
```

Each scenario can have its own:

- 👥 Virtual-user configuration
- 🔀 Execution logic
- 🎯 Requests
- ⏱️ Timing behavior
- ✅ Assertions
- 📊 Result collection

---

# 👥 2.3 Thread Group

A **Thread Group** defines and controls the **virtual-user execution model**.

In simple terms:

> 👤 **One JMeter thread ≈ One virtual user**

The Thread Group determines **how many users run, how quickly they start, how many times they execute the scenario, and how long the test continues**.

---

## ⚙️ Common Thread Group Settings

| Setting                          | Purpose                                     |
| -------------------------------- | ------------------------------------------- |
| 👥 **Number of Threads (Users)** | Number of virtual users                     |
| 🚀 **Ramp-up Period**            | Time taken to start all users               |
| 🔁 **Loop Count**                | Number of times each user executes the flow |
| ⏱️ **Duration**                  | How long the test runs                      |
| 🗓️ **Scheduler**                 | Controls scheduled execution                |

---

## 🧪 Example Configuration

```text
Threads        = 10
Ramp-up        = 20 seconds
Loop Count     = 5
```

### What does this mean?

```text
10 Virtual Users
       │
       │  Ramp-up = 20 seconds
       ▼
┌───────────────────────────────────┐
│                                   │
│   👤 User 1                       │
│   👤 User 2                       │
│   👤 User 3                       │
│   👤 User 4                       │
│   👤 User 5                       │
│   👤 User 6                       │
│   👤 User 7                       │
│   👤 User 8                       │
│   👤 User 9                       │
│   👤 User 10                      │
│                                   │
└───────────────────────────────────┘
       │
       ▼
Each User Executes the Flow
       │
       ├── 🔁 Iteration 1
       ├── 🔁 Iteration 2
       ├── 🔁 Iteration 3
       ├── 🔁 Iteration 4
       └── 🔁 Iteration 5
```

---

## 🧠 Thread Group Mental Model

Think of a Thread Group as the **virtual-user engine** of your JMeter test.

```text
                 👥 THREAD GROUP
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
      👤 User 1     👤 User 2    👤 User 3
          │            │            │
          ▼            ▼            ▼
       Scenario     Scenario     Scenario
          │            │            │
          ▼            ▼            ▼
       Requests      Requests      Requests
```

### 🔑 Key Takeaway

> **Thread Group answers the question:**
>
> **"How many virtual users should execute this test, and how should they execute it over time?"**

---

## 🧭 Architecture So Far

```text
                    📋 TEST PLAN
                         │
                         ▼
                  👥 THREAD GROUP
                         │
                 Virtual Users
                         │
             ┌───────────┴───────────┐
             │                       │
             ▼                       ▼
          🎯 SAMPLER             🔀 CONTROLLER
             │                       │
             └───────────┬───────────┘
                         │
                         ▼
                    ⏱️ TIMER
                         │
                         ▼
                   ✅ ASSERTION
                         │
                         ▼
                    📊 RESULT
```

> 🚀 **Next:** Continue with the individual JMeter test elements — **Samplers, Controllers, Timers, Assertions, and Listeners/Results** — and understand how they behave inside a Thread Group.

# 🧩 2.4–2.9 JMeter Test Elements

![JMeter](https://img.shields.io/badge/Apache%20JMeter-5.6.3-D22128?style=for-the-badge&logo=apachejmeter&logoColor=white)
![Testing](https://img.shields.io/badge/Testing-Performance-6366F1?style=for-the-badge)
![QA](https://img.shields.io/badge/Role-QA%20Engineering-0EA5E9?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-In%20Progress-F59E0B?style=for-the-badge)

> 🧠 **Objective:** Understand the core JMeter components responsible for generating traffic, controlling execution flow, introducing realistic timing, validating responses, providing reusable configuration, and analyzing results.

---

## 🎯 2.4 Sampler

A **Sampler** generates a request to the target system.

It is one of the most important components in JMeter because it represents the actual interaction between a virtual user and the system under test.

For HTTP/API performance testing, the **HTTP Request** sampler is one of the most commonly used samplers.

### 🔄 Sampler Execution Model

```text
👤 Virtual User
      │
      ▼
🎯 Sampler
      │
      ▼
🌐 Request
      │
      ▼
🖥️ Target System
      │
      ▼
📨 Response
```

### 🌐 HTTP Request Example

```text
HTTP Request
│
├── Protocol: https
├── Server: jsonplaceholder.typicode.com
├── Method: GET
└── Path: /posts/1
```

Equivalent API request:

```http
GET https://jsonplaceholder.typicode.com/posts/1
```

### 🧠 Key Concept

> **Sampler = The action performed by the virtual user.**

Examples:

```text
Login
   ↓
HTTP Request Sampler

Search Patient
   ↓
HTTP Request Sampler

Update Patient
   ↓
HTTP Request Sampler
```

---

## 🔀 2.5 Controller

Controllers control the **logical flow and execution of requests**.

They can be used to model:

- User journeys
- Conditional behavior
- Loops
- Transactions
- Execution frequency
- Runtime behavior

### 👤 Example User Journey

```text
👤 User
  │
  ▼
🔐 Login
  │
  ▼
🔎 Search Patient
  │
  ▼
👁️ View Patient
  │
  ▼
✏️ Update Patient
```

A controller can determine **when, how often, and under what conditions** these requests execute.

### 🧩 Common Controllers

| Controller                    | Primary Purpose                               |
| ----------------------------- | --------------------------------------------- |
| 📦 **Simple Controller**      | Organizes related requests                    |
| 🔀 **If Controller**          | Executes requests conditionally               |
| 🔁 **Loop Controller**        | Repeats a group of requests                   |
| 📊 **Transaction Controller** | Measures a group of requests as a transaction |
| 🎚️ **Throughput Controller**  | Controls execution frequency                  |
| ⏱️ **Runtime Controller**     | Controls execution based on runtime           |

### 🧠 Controller Mental Model

```text
                  🔀 CONTROLLER
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
       🔐 Login     🔎 Search     👁️ View
          │            │            │
          └────────────┼────────────┘
                       │
                       ▼
                    ✏️ Update
```

> 💡 **Key Concept:**
> A Controller generally **does not generate the actual HTTP traffic**. It determines **how samplers are executed**.

---

## ⏱️ 2.6 Timer

A **Timer** introduces a delay before a sampler executes.

Timers are useful for modelling:

- Realistic user behavior
- Think time
- Delays between actions
- Controlled request pacing

### 👤 Realistic User Flow

```text
🔐 Login
  │
  ▼
⏱️ Think Time
  │
  │ 2 seconds
  ▼
🔎 Search Patient
```

Without appropriate timing, a test may generate traffic that does not represent realistic user behavior.

### ⚠️ Why Think Time Matters

Consider a real user:

```text
Login
   ↓
Read screen
   ↓
Think
   ↓
Search
   ↓
Read results
   ↓
Open patient
```

A JMeter test without timers may behave more like:

```text
Login
 ↓
Search
 ↓
View
 ↓
Update
 ↓
Search
 ↓
View
 ↓
Update
```

with virtually no human-like delay.

That can produce an unrealistic workload.

### 🧠 Key Concept

> **Timer = Delay introduced to control request pacing and simulate user think time.**

---

## ✅ 2.7 Assertion

An **Assertion** validates whether a response satisfies an expected condition.

Assertions are important because a request can technically complete while the application behavior is still incorrect.

### ✔️ Example: HTTP Status Validation

```text
Expected:
HTTP Response Code = 200
```

### ✔️ Example: Response Content Validation

```text
Expected:
Response contains "patientId"
```

### ❌ Fast but Failed Request

A request may be very fast:

```text
Response Time = 50 ms
HTTP Status   = 500
```

From a performance perspective, **50 ms looks excellent**.

From a functional perspective, however, the request failed.

Therefore:

```text
Fast ≠ Successful
```

### 🎯 Performance Test Validation

A meaningful performance test should consider both:

```text
                 PERFORMANCE RESULT
                         │
              ┌──────────┴──────────┐
              │                     │
              ▼                     ▼
        ⏱️ Performance          ✅ Correctness
              │                     │
              ▼                     ▼
        Response Time          HTTP Status
        Throughput             Response Body
        Percentiles            Business Rules
        Error Rate             Data Validation
```

> 💡 **Key Concept:**
> Performance testing is not only about **how fast** the system responds. It is also about whether the system **responds correctly under load**.

---

## ⚙️ 2.8 Config Element

**Config Elements** provide configuration and data used by Samplers.

They help centralize reusable settings and reduce unnecessary duplication.

### 🧩 Common Config Elements

| Config Element                | Purpose                        |
| ----------------------------- | ------------------------------ |
| 🌐 **HTTP Request Defaults**  | Defines reusable HTTP settings |
| 📨 **HTTP Header Manager**    | Defines request headers        |
| 📄 **CSV Data Set Config**    | Reads test data from CSV files |
| 🍪 **HTTP Cookie Manager**    | Handles HTTP cookies           |
| ⚙️ **User Defined Variables** | Stores reusable variables      |

### 🏗️ Example

Instead of configuring this repeatedly:

```text
Protocol: https
Server: api.example.com
```

for every HTTP Request, we can use:

```text
HTTP Request Defaults
│
├── Protocol: https
└── Server: api.example.com
```

Then individual samplers only need to define what changes:

```text
GET /patients
GET /appointments
POST /patients
PUT /patients/{id}
```

### 🧠 Key Concept

> **Config Element = Reusable configuration and test data.**

This becomes especially valuable as a JMeter test grows from:

```text
3 Requests
```

to:

```text
30 Requests
```

or:

```text
300+ Requests
```

---

## 📊 2.9 Listener

**Listeners** provide ways to view and analyze JMeter results.

They are particularly useful during:

- Learning
- Debugging
- Test development
- Result inspection

### 📋 Common Listeners

| Listener                 | Typical Use                               |
| ------------------------ | ----------------------------------------- |
| 🌳 **View Results Tree** | Inspect individual requests and responses |
| 📄 **Summary Report**    | View summarized performance metrics       |
| 📊 **Aggregate Report**  | Analyze aggregated performance statistics |

### ⚠️ Important Practice

Listeners can consume significant **CPU and memory resources**.

Therefore:

```text
Learning / Debugging
        ↓
GUI Listeners can be useful
```

but:

```text
Serious Load Execution
        ↓
Avoid heavy GUI listeners
```

For larger tests, results are commonly collected using **non-GUI execution** and analyzed using JMeter's reporting capabilities or external analysis tools.

### 🧠 Key Concept

> **Listener = Result visualization and analysis.**

> ⚠️ **Professional Practice:**
> Do not use heavy GUI listeners as part of a serious load-generation strategy unless there is a specific debugging requirement.

---

# 🧠 2.10 Complete JMeter Component Model

Now we can connect the major JMeter components together.

```text
                         📋 TEST PLAN
                              │
                              ▼
                       👥 THREAD GROUP
                              │
                     Virtual Users
                              │
                              ▼
                       🔀 CONTROLLER
                              │
                 ┌────────────┴────────────┐
                 │                         │
                 ▼                         ▼
             ⏱️ TIMER                  🎯 SAMPLER
                 │                         │
                 │                         ▼
                 │                    🌐 REQUEST
                 │                         │
                 │                         ▼
                 │                    🖥️ SYSTEM
                 │                         │
                 │                         ▼
                 │                    📨 RESPONSE
                 │                         │
                 │                         ▼
                 └──────────────────► ✅ ASSERTION
                                           │
                                           ▼
                                      📊 RESULT
                                           │
                                           ▼
                                      👁️ LISTENER
```

### 🔑 One-Line Mental Model

> **Thread Group defines the users → Controller defines the flow → Sampler generates the request → Timer controls pacing → Assertion validates the response → Listener helps analyze the result.**

---

# 🎤 2.11 Presentation Summary

> **"JMeter organizes performance tests through a hierarchy of components. The Test Plan is the top-level container. Thread Groups model virtual-user execution, Samplers generate requests, Controllers define execution flow, Timers model delays or think time, Assertions validate responses, Config Elements provide reusable configuration and data, and Listeners help us inspect or analyze results."**

---

# 💬 2.12 Discussion Questions

### ❓ What is the most important component for defining virtual users?

**Answer:** 👥 **Thread Group**

The Thread Group defines the number of virtual users and controls their execution behavior.

---

### ❓ Which JMeter component actually sends an HTTP request?

**Answer:** 🎯 **HTTP Request Sampler**

The HTTP Request sampler generates the actual HTTP request sent to the target system.

---

### ❓ Why do we use Timers?

**Answer:** ⏱️ **To introduce controlled delays and model realistic user behavior or think time.**

---

### ❓ Why shouldn't we rely heavily on GUI listeners during a load test?

**Answer:** 📊 **GUI listeners can consume significant CPU and memory on the load generator and may interfere with the accuracy and scalability of the test.**

---

### ❓ Can a request be successful from a network perspective but still fail from a business perspective?

**Answer:** ✅ **Yes.**

For example:

```text
HTTP Status = 200
```

but:

```text
Response Body:
{
    "status": "error"
}
```

Therefore, appropriate **Assertions** are required to validate actual application behavior.

---

# 📌 2.13 Key Takeaways

```text
📋 Test Plan
    ↓
Defines the overall test

👥 Thread Group
    ↓
Models virtual-user execution

🎯 Sampler
    ↓
Generates requests

🔀 Controller
    ↓
Controls execution flow

⏱️ Timer
    ↓
Introduces delays / think time

✅ Assertion
    ↓
Validates responses

⚙️ Config Element
    ↓
Provides reusable configuration / data

📊 Listener
    ↓
Displays or helps analyze results
```

### 🧠 Remember

```text
Users
  ↓
Flow
  ↓
Requests
  ↓
Timing
  ↓
Validation
  ↓
Results
```

---

# 🌍 3. Environment & Installation

![Status](https://img.shields.io/badge/Status-Verified-22C55E?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-macOS-000000?style=for-the-badge&logo=apple&logoColor=white)
![Java](https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![JMeter](https://img.shields.io/badge/JMeter-5.6.3-D22128?style=for-the-badge&logo=apachejmeter&logoColor=white)

> 🎯 **Objective:** Establish and verify a reproducible local environment for JMeter performance testing.

---

## 🖥️ 3.1 Current Learning Environment

The current learning environment used for this repository:

| Component               | Version / Value     |
| ----------------------- | ------------------- |
| 🖥️ **Operating System** | macOS 15.7.9        |
| 🏗️ **Architecture**     | x86_64              |
| ☕ **Java**             | OpenJDK 17.0.20.1   |
| 🚀 **JMeter**           | Apache JMeter 5.6.3 |
| 🔀 **Git**              | 2.43.0              |
| 🍺 **Homebrew**         | 6.0.20              |

---

## 🔍 3.2 Verify macOS

Run:

```bash
sw_vers
```

Example:

```text
ProductName:    macOS
ProductVersion: 15.7.9
BuildVersion:   24G830
```

### ✅ Verification

```text
Operating System
      │
      ▼
    macOS
      │
      ▼
Version verified
```

---

## 🏗️ 3.3 Verify Architecture

Run:

```bash
uname -m
```

Expected:

```text
x86_64
```

This confirms that the current environment is running on an **x86_64 architecture**.

---

## ☕ 3.4 Verify Java

Run:

```bash
java --version
```

Expected environment:

```text
openjdk 17.0.20.1
OpenJDK Runtime Environment Temurin-17.0.20.1+1
OpenJDK 64-Bit Server VM Temurin-17.0.20.1+1
```

### 🧠 Why Java Matters

Apache JMeter runs on the **Java Virtual Machine (JVM)**.

Therefore:

```text
JMeter
  ↓
Java Runtime
  ↓
Operating System
```

A properly configured Java runtime is an important prerequisite for reliable JMeter execution.

---

## 🔎 3.5 Locate Java Installations

Run:

```bash
/usr/libexec/java_home -V
```

Example:

```text
Matching Java Virtual Machines (2):

17.0.20.1 ... /Library/Java/JavaVirtualMachines/temurin-17.jdk/Contents/Home

1.8.391.13 ... /Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home
```

For this learning environment:

```text
Active Java
    ↓
Java 17
    ↓
Temurin JDK
```

---

## 🚀 3.6 Verify JMeter

Run:

```bash
jmeter --version
```

Expected:

```text
Apache JMeter 5.6.3
```

JMeter may display warnings related to Java packages, plugin scanning, or environment configuration.

A warning does **not automatically mean that JMeter execution has failed**.

The important verification is:

```text
JMeter launches successfully
        +
Correct version is reported
        =
Environment is operational
```

---

## 🔀 3.7 Verify Git

Run:

```bash
git --version
```

Example:

```text
git version 2.43.0
```

Git is used to version-control:

- 🧪 JMeter test plans
- 📜 Documentation
- ⚙️ Configuration files
- 📊 Test artifacts
- 📝 Learning notes

---

## 🍺 3.8 Verify Homebrew

Run:

```bash
brew --version
```

Example:

```text
Homebrew 6.0.20
```

Homebrew provides a convenient package-management mechanism for macOS development and testing tools.

---

## ✅ 3.9 Environment Verification Checklist

```text
[✓] macOS detected
[✓] Architecture verified
[✓] Java 17 installed
[✓] Java runtime verified
[✓] JMeter installed
[✓] JMeter version verified
[✓] JMeter GUI launches
[✓] Git installed
[✓] Homebrew installed
```

### 🟢 Environment Status

> **Environment: VERIFIED**

---

# 🧪 4. First JMeter Test

![Status](https://img.shields.io/badge/Status-Completed-22C55E?style=for-the-badge)
![Test Type](https://img.shields.io/badge/Test-HTTP%20API-0EA5E9?style=for-the-badge)
![Result](https://img.shields.io/badge/Result-PASS-22C55E?style=for-the-badge)

> 🎯 **Objective:** Create and execute a basic HTTP API test using Apache JMeter and understand the fundamental request/response execution flow.

---

## 🎯 4.1 Objective

The purpose of this experiment is to understand the basic execution flow:

```text
📋 Test Plan
      ↓
👥 Thread Group
      ↓
🎯 HTTP Request
      ↓
🌐 Target API
      ↓
📨 HTTP Response
      ↓
📊 JMeter Result
```

---

## 🌐 4.2 Target API

```http
GET https://jsonplaceholder.typicode.com/posts/1
```

---

## ⚙️ 4.3 Test Configuration

```text
Virtual Users: 1
Loop Count:    1
HTTP Method:   GET
Path:          /posts/1
```

### 📐 Workload Model

```text
👤 Users = 1
   │
   ▼
🔁 Iterations = 1
   │
   ▼
🎯 Requests = 1
```

---

## 🏗️ 4.4 JMeter Test Structure

```text
📋 Test Plan
└── 👥 Thread Group
    ├── 🎯 HTTP Request
    └── 🌳 View Results Tree
```

---

## 🌐 4.5 HTTP Request Configuration

```text
HTTP Request
│
├── Protocol: https
├── Server: jsonplaceholder.typicode.com
├── Method: GET
└── Path: /posts/1
```

Equivalent request:

```http
GET /posts/1
Host: jsonplaceholder.typicode.com
```

---

## 📊 4.6 Execution Result

Observed result:

```text
Response Code:    200
Response Message: OK

Sample Count:     1
Error Count:      0

Load Time:        935 ms
Connect Time:     628 ms
Latency:          925 ms
```

Response type:

```text
Content-Type: application/json
```

---

## 🔎 4.7 Result Interpretation

The request completed successfully:

```text
HTTP 200
Error Count = 0
Sample Count = 1
```

Therefore:

```text
┌─────────────────────────┐
│        TEST RESULT      │
│                         │
│          ✅ PASS        │
└─────────────────────────┘
```

The API returned JSON data containing fields such as:

```json
{
  "userId": 1,
  "id": 1,
  "title": "...",
  "body": "..."
}
```

---

## ⏱️ 4.8 Performance Observation

The observed load time was:

```text
935 ms
```

However, this single measurement should **not** be used to conclude that the API is slow or fast.

The test contained:

```text
1 Virtual User
1 Request
1 Iteration
```

This represents an extremely small workload.

### ❌ Incorrect Conclusion

```text
935 ms
   ↓
"The API is slow."
```

### ✅ Correct Interpretation

```text
935 ms
   ↓
"One request completed in approximately 935 ms
under this specific test condition."
```

Meaningful performance analysis requires:

- Representative workload
- Sufficient samples
- Controlled test conditions
- Appropriate metrics
- Repeatable execution

---

## 📈 4.9 Scaling the Workload

A basic progression might look like:

```text
👤 1 User
    ↓
👥 10 Users
    ↓
👥 50 Users
    ↓
👥 100 Users
    ↓
👥 500 Users
```

As workload increases, observe:

```text
              PERFORMANCE
                   │
       ┌───────────┼───────────┐
       │           │           │
       ▼           ▼           ▼
Response Time  Throughput   Error Rate
       │           │           │
       └───────────┼───────────┘
                   ▼
              📊 Analysis
```

The objective is not simply to increase users.

The objective is to understand **how system behavior changes as workload increases**.

---

## 🎤 4.10 Presentation Summary

> **"In our first JMeter experiment, we created a Test Plan containing a Thread Group and an HTTP Request sampler. We simulated one virtual user executing one GET request against a public API. The API returned HTTP 200 with zero sample errors. JMeter also captured timing and response-size metrics. However, one successful request is not enough to establish performance characteristics. Meaningful performance testing requires a controlled workload and sufficient observations."**

---

## 📌 4.11 Experiment Takeaways

- 👥 JMeter can simulate virtual users.
- 🎯 Thread Groups control virtual-user execution.
- 🌐 HTTP Request Samplers generate HTTP traffic.
- 📊 JMeter captures response and timing information.
- ✅ HTTP 200 indicates a successful HTTP response.
- 🟢 Zero sample errors indicates no JMeter sample error for this request.
- ⚠️ A single request is not a meaningful performance benchmark.
- 📈 Performance conclusions require representative workloads and sufficient samples.

---

# 🧪 5. Practical Lab Log

![Lab](https://img.shields.io/badge/Lab-Practical-8B5CF6?style=for-the-badge)
![Learning](https://img.shields.io/badge/Learning-Hands--On-0EA5E9?style=for-the-badge)

This section records hands-on experiments performed while building this guide.

|      # | Experiment                                              |    Status    |
| -----: | ------------------------------------------------------- | :----------: |
| **01** | Execute first HTTP GET request                          | ✅ Completed |
| **02** | Observe multiple virtual users                          |  ⏳ Planned  |
| **03** | Compare response-time behavior under increased workload |  ⏳ Planned  |
| **04** | Add assertions                                          |  ⏳ Planned  |
| **05** | Add timers / think time                                 |  ⏳ Planned  |
| **06** | Build multi-step API journey                            |  ⏳ Planned  |

---

# 🎤 6. Presentation Framework

When presenting a JMeter topic, explain it using the following framework:

```text
┌─────────────────────────────────────┐
│        🎤 PRESENTATION FLOW         │
├─────────────────────────────────────┤
│ 1. What is it?                      │
│ 2. Why do we need it?               │
│ 3. How does it work?                │
│ 4. Where is it used?                │
│ 5. What does it look like in JMeter?│
│ 6. What happens during execution?   │
│ 7. How do we analyze the result?    │
│ 8. What mistakes should we avoid?  │
└─────────────────────────────────────┘
```

This approach keeps the presentation useful for:

- 🧪 QA Engineers
- 💻 Developers
- 📋 Project Managers
- 🏗️ Technical Leads
- 📈 Performance Engineers

---

# 📌 7. Master Learning Principle

> ## 🧠 Don't Learn JMeter as a Collection of UI Components

Learn JMeter as a system for:

```text
             🧠 PERFORMANCE ENGINEERING
                       │
       ┌───────────────┼───────────────┐
       │               │               │
       ▼               ▼               ▼
   🏗️ Workload      🌐 Traffic      ✅ Validation
    Modeling       Generation        & Correctness
       │               │               │
       └───────────────┼───────────────┘
                       │
                       ▼
                  📊 Measurement
                       │
                       ▼
                   🔎 Analysis
                       │
                       ▼
                🎯 Engineering Decision
```

> **The real goal is not to learn where a JMeter button is. The goal is to understand how to model workload, generate traffic, validate behavior, measure system performance, and turn test results into engineering decisions.**

---

# 🚀 8. Guide Progress

```text
Foundation
████████████████░░░░  In Progress

Architecture
████████████████░░░░  In Progress

Environment
████████████████████  Verified

First API Test
████████████████████  Completed

Multi-User Testing
████░░░░░░░░░░░░░░░░  Upcoming

Load Testing
░░░░░░░░░░░░░░░░░░░░  Upcoming

Stress Testing
░░░░░░░░░░░░░░░░░░░░  Upcoming

Performance Analysis
░░░░░░░░░░░░░░░░░░░░  Upcoming
```

---

# 🧭 Next Step

The next practical stage is to move from:

```text
👤 1 User
   +
🎯 1 Request
   +
🔁 1 Iteration
```

to a controlled workload:

```text
👥 Multiple Users
        ↓
🚀 Ramp-up
        ↓
🔁 Multiple Iterations
        ↓
⏱️ Think Time
        ↓
🎯 Multiple Requests
        ↓
✅ Assertions
        ↓
📊 Performance Metrics
```

> 🚀 **Next:** Build a multi-user workload and understand how **Threads, Ramp-up, Loop Count, Concurrency, Throughput, Response Time, and Error Rate** interact during a real JMeter test.
