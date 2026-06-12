Based on the image you provided, here is an explanation of the **three types of test plans** in software testing.

---

## Types of Test Plan

Test plans can be categorized into three main types based on scope, purpose, and level of testing.

---

### 1. Master Test Plan

**Description:** A single high-level test plan for a project or product that unifies all other test plans. It goes into great depth on the planning and management of testing at various test levels, providing a **bird's eye view** of important decisions, tactics used, test coverage, and the connection between different test levels.

| Aspect | Details |
|--------|---------|
| **Owner** | Senior QA Managers or Test Leads |
| **Scope** | Entire Project |
| **Content Includes** | List of tests to be executed, test coverage, relationships between test levels (unit, integration, system, acceptance), overall test strategy, resource allocation, major milestones |

**When to use:** Large projects with multiple testing phases or teams.

**Example:** A master test plan for an e-commerce platform covering unit testing by developers, integration testing by QA, system testing by test engineers, and UAT by business users.

---

### 2. Phase Test Plan

**Description:** A test plan that emphasizes **any one phase of testing**. It focuses on a single level or phase of the testing lifecycle.

| Aspect | Details |
|--------|---------|
| **Owner** | QA Leads or Testers |
| **Scope** | Single Level/Phase (e.g., Unit, Integration, System, Acceptance) |
| **Examples** | Unit Test Plan, Integration Test Plan, System Test Plan, Acceptance Test Plan |

**When to use:** When testing is organized into distinct phases, each requiring its own detailed plan.

**Example:** An **Integration Test Plan** that specifically defines how modules A, B, and C will be integrated and tested together, including interface specifications, stubs/drivers, and test data.

---

### 3. Specific Test Plan

**Description:** A test plan designed for **specific types of testing**, especially **non-functional testing**. It focuses on a single test type rather than a test level.

| Aspect | Details |
|--------|---------|
| **Owner** | Specialized Testers or QA Engineers |
| **Scope** | Single Test Type (e.g., Security, Performance, Usability, Stress) |

**When to use:** When specialized testing requires its own detailed approach, tools, and metrics separate from functional testing.

**Example:** A **Security Test Plan** detailing penetration testing, vulnerability scanning, authentication testing, and data encryption validation.

---

## Comparison Summary Table

| Test Plan Type | Owner | Scope | Focus |
|----------------|-------|-------|-------|
| **Master Test Plan** | Senior QA Manager / Test Lead | Entire Project | Unifies all testing activities; high-level strategy |
| **Phase Test Plan** | QA Lead / Tester | Single Phase (e.g., System Testing) | One specific level of testing |
| **Specific Test Plan** | Specialized Tester (e.g., Security Engineer) | Single Test Type (e.g., Performance) | One specific type of testing, especially non-functional |

---

## Relationship Between Test Plan Types

```
┌─────────────────────────────────────────────┐
│           Master Test Plan                  │
│         (Entire Project Scope)              │
│                                             │
│  ┌─────────────┐  ┌─────────────┐          │
│  │ Phase Test  │  │ Specific    │          │
│  │ Plan        │  │ Test Plan   │          │
│  │ (Unit)      │  │ (Security)  │          │
│  └─────────────┘  └─────────────┘          │
│  ┌─────────────┐  ┌─────────────┐          │
│  │ Phase Test  │  │ Specific    │          │
│  │ Plan        │  │ Test Plan   │          │
│  │ (System)    │  │ (Performance)│         │
│  └─────────────┘  └─────────────┘          │
└─────────────────────────────────────────────┘
```

---

## Practical Takeaway for Software Project Managers

| Project Size | Recommended Approach |
|--------------|----------------------|
| **Small project** | One Master Test Plan may be sufficient |
| **Medium project** | Master Test Plan + Phase Test Plans for each test level |
| **Large/complex project** | Master Test Plan + Phase Test Plans + Specific Test Plans (especially for security, performance, or compliance requirements) |

> **Key point:** The Master Test Plan provides overall direction and coordination, while Phase and Specific Test Plans provide detailed execution guidance for particular parts of testing. For contract-based software projects, the Master Test Plan is often referenced in the acceptance criteria section.

---
### [[Relaiton betewen Master, phase and specific test plans]]
