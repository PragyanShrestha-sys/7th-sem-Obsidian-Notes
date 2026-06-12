Here is an explanation of **Test Strategy** and its types based on the image you provided.

---

## What is a Test Strategy?

A **Test Strategy** is a high-level document or approach that defines **how testing will be carried out** for a software project. It outlines the testing principles, methods, risks, and objectives without going into the specific details of test cases or schedules (which belong to the Test Plan).

In simple terms:  
- **Test Strategy** = *What* testing approach to use and *why* (strategic)  
- **Test Plan** = *How* and *when* to execute that strategy (tactical)

The image describes three types of test strategies:

---

## Types of Test Strategy

### 1. Static Test Strategy

**Description:** Evaluates the quality of a system **without actually running the system**. It looks at portions or system elements to detect problems as early as possible.

| Aspect | Details |
|--------|---------|
| **Execution** | No code execution; analysis is done on documentation, code, or design |
| **Timing** | Performed early in the development lifecycle |
| **Goal** | Detect problems as early as possible to save time and money |
| **Requirement** | Static tests must be performed at the right time |

**Examples of Static Testing:**
- Code reviews (developers reviewing each other's code)
- Walkthroughs and inspections of requirements documents
- Static code analysis using tools (e.g., SonarQube, ESLint)
- Reviewing design documents before development begins

**Advantage:** Finds defects before any code is executed, making fixes extremely cheap.

---

### 2. Structural Test Strategy

**Description:** Tests that need to be operated on **"real devices"** with the system run in its entirety to find all bugs. Often run on individual components and interfaces to identify localized errors in data flows.

| Aspect | Details |
|--------|---------|
| **Execution** | System must be executed (running code) |
| **Environment** | Real devices or actual execution environments |
| **Focus** | Individual components, interfaces, data flows |
| **Goal** | Identify localized errors in how data moves through the system |

**Examples of Structural Testing:**
- Unit testing (testing individual functions or modules)
- Integration testing (testing interfaces between modules)
- Data flow testing (tracking how data moves from input to output)
- Running tests on actual hardware (e.g., mobile devices, IoT devices)

**Also known as:** White-box testing (when focused on internal structure)

**Advantage:** Finds errors related to code logic, data handling, and component interactions.

---

### 3. Behavioural Test Strategy

**Description:** Focuses on **how a system acts** rather than the mechanism behind its functions. Focuses on workflows, configurations, performance, and all elements of the user journey.

| Aspect | Details |
|--------|---------|
| **Execution** | System is executed, but internal structure is ignored |
| **Focus** | System behavior, outputs, user experience |
| **Goal** | Validate that the system behaves correctly from the user's perspective |

**Examples of Behavioural Testing:**
- Functional testing (does the login button actually log in?)
- User acceptance testing (UAT) – does the system meet business needs?
- Performance testing (how fast does the system respond?)
- Configuration testing (does it work in different environments?)
- End-to-end user journey testing

**Also known as:** Black-box testing (when internal structure is ignored)

**Advantage:** Ensures the system meets user expectations and business requirements, regardless of how it is built internally.

---

## Comparison Summary Table

| Aspect | Static Strategy | Structural Strategy | Behavioural Strategy |
|--------|----------------|---------------------|----------------------|
| **Execute the system?** | No | Yes | Yes |
| **Look at internal code?** | Yes (reviews) | Yes (components, data flows) | No |
| **Look at behavior/output?** | No | Sometimes | Yes (primary focus) |
| **When performed** | Early (requirements, design) | During development (unit/integration) | Later (system, UAT) |
| **Main goal** | Find defects early before execution | Find localized logic/data errors | Validate user-facing behavior |
| **Examples** | Code reviews, static analysis | Unit tests, integration tests | Functional tests, UAT, performance tests |

---

## Relationship Between Test Strategy and Test Plan

```
Test Strategy (Strategic)
    │
    ├── "We will use Static testing during requirements phase"
    ├── "We will use Structural testing for unit and integration"
    └── "We will use Behavioural testing for system and UAT"
                    │
                    ▼
Test Plan (Tactical)
    │
    ├── "Static review of SOW will happen on Day 2"
    ├── "Unit tests will be written in JUnit by developers"
    └── "UAT will be conducted by business users from Day 25-30"
```

---

## Practical Takeaway

| If you want to...                       | Use this strategy |
| --------------------------------------- | ----------------- |
| Find defects before writing any code    | **Static**        |
| Test internal logic and data flows      | **Structural**    |
| Test what the user actually experiences | **Behavioural**   |

> **Key point:** A complete test strategy typically uses **all three** approaches at different stages of the project. Static testing catches early design issues, structural testing ensures code correctness, and behavioural testing confirms the software meets user needs.


---

### [[Test strategy Components]]


---
![[Pasted image 20260403080249.png]]