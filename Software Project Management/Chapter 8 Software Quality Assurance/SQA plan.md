
## What is an SQA Plan?

A **Software Quality Assurance (SQA) Plan** is a **document that outlines the strategies, processes, and procedures** that will be used to ensure the quality of a software product.

It is typically developed **early** in the software development process and is used to guide the entire development and testing process.

---

## Purpose of an SQA Plan

| Purpose | Explanation |
|---------|-------------|
| **Guide quality activities** | Provides a roadmap for all quality-related tasks |
| **Set expectations** | Defines quality goals, roles, and standards |
| **Ensure consistency** | Makes sure quality is built in, not just tested at the end |
| **Comply with standards** | Demonstrates adherence to industry regulations |

---

## Elements of an SQA Plan

The images list **8 key elements** of an SQA plan:

### 1. Quality Objectives

**Description:** The specific goals and targets that the software development team is trying to achieve with respect to quality.

**Examples:**
- Defect density < 2 per 1000 lines of code
- 99.9% uptime for critical features
- 95% test pass rate before release

---

### 2. Standards and Regulations

**Description:** Any relevant industry standards or government regulations that the software must comply with.

**Examples:**
- ISO 9001 (Quality management)
- ISO 25000 (Software quality)
- GDPR (Data protection for EU users)
- HIPAA (Healthcare data privacy)
- PCI-DSS (Payment card security)

---

### 3. Roles and Responsibilities

**Description:** A clear definition of the roles and responsibilities of the development team and the QA team, and how they will work together.

**Examples of roles:**
- QA Manager – Oversees quality strategy
- Test Engineer – Executes test cases
- Developer – Writes unit tests, fixes defects
- Product Owner – Defines acceptance criteria

---

### 4. Testing Strategy

**Description:** A description of the types of testing that will be performed, such as unit testing, integration testing, and acceptance testing, as well as the tools and techniques that will be used.

**Examples:**
- Unit testing (JUnit, PyTest)
- Integration testing (Postman, SoapUI)
- System testing
- User Acceptance Testing (UAT)
- Performance testing (JMeter)
- Security testing (OWASP ZAP)

---

### 5. Configuration Management

**Description:** Procedures for managing and controlling changes to the software throughout the development process.

**Examples:**
- Version control (Git, SVN)
- Change request approval process
- Build and release management
- Environment configuration control

---

### 6. Problem Reporting and Resolution

**Description:** Procedures for identifying and resolving defects in the software.

**Examples:**
- Defect tracking tool (JIRA, Bugzilla, Trello)
- Severity levels (Critical, Major, Minor, Trivial)
- Workflow: New → Assigned → In Progress → Fixed → Verified → Closed
- Escalation process for unresolved issues

---

### 7. Audits and Reviews

**Description:** Plans for performing regular audits and reviews to ensure that the software development process is meeting its quality objectives.

**Examples:**
- Code reviews (peer reviews, pull requests)
- Design reviews
- Process audits (are we following SQA plan?)
- Requirements reviews
- Test case reviews

---

### 8. Training and Documentation

**Description:** Plans for providing training and documentation to support the software development and testing process.

**Examples:**
- Training: New tool onboarding, security awareness, testing methodology
- Documentation: Test plans, test cases, user manuals, QA procedures

---

## Summary Table: 8 Elements of SQA Plan

| #   | Element                        | Key Question                         |
| --- | ------------------------------ | ------------------------------------ |
| 1   | Quality Objectives             | What quality goals are we targeting? |
| 2   | Standards & Regulations        | What rules must we follow?           |
| 3   | Roles & Responsibilities       | Who does what?                       |
| 4   | Testing Strategy               | How will we test?                    |
| 5   | Configuration Management       | How do we control changes?           |
| 6   | Problem Reporting & Resolution | How do we track and fix defects?     |
| 7   | Audits & Reviews               | How do we check ourselves?           |
| 8   | Training & Documentation       | How do we support the team?          |

---

## When is the SQA Plan Created?

```
Requirements → SQA Plan Created Early → Development → Testing → Release
                     ▲
                     │
              Guides entire process
```

The SQA plan is created **early** in the software development lifecycle, typically after requirements are gathered but before development begins.

---

## SQA Plan vs. Test Plan

| Aspect | SQA Plan | Test Plan |
|--------|----------|-----------|
| **Scope** | Broader (process + product quality) | Narrower (testing activities only) |
| **Focus** | Preventing defects through processes | Detecting defects through testing |
| **Audience** | Entire project team | Testing team |
| **Elements** | Standards, audits, training, configuration | Test cases, schedule, environment, exit criteria |

---

## Practical Takeaway

> **An SQA plan is your quality roadmap.** It answers: "How will we ensure quality from start to finish?" It covers not just testing, but also standards, roles, change management, defect tracking, audits, and training. Develop it early and use it throughout the project to keep quality on track.