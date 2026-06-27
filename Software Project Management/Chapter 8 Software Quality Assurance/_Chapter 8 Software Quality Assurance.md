## [[Software Testing Objectives and Importance]]

**Software Testing** is the process of evaluating and verifying that a software application or system meets specified requirements and works as expected. It involves executing software components (or the entire system) to find defects, ensure quality, and validate that the software does what it is supposed to do—and does not do what it is not supposed to do.

In simple terms: **Testing checks if the software is bug-free, reliable, and fit for use.**

---
## [[Software Testing Principles]]

Software Testing is a crucial activity in software development that ensures quality, reliability, and
correctness of a system. Due to its complexity, structured guidelines are required.

One widely accepted set of principles is given by ISTQB (International Software Testing
Qualifications Board), which can be listed below as:

| #   | Principle                 | Core Message                                     |
| --- | ------------------------- | ------------------------------------------------ |
| 1   | Defects, not absence      | Testing finds bugs, doesn't prove perfection     |
| 2   | Exhaustive impossible     | Can't test everything → prioritize risks         |
| 3   | Early testing             | Find bugs early → cheaper to fix                 |
| 4   | Defects cluster           | 80% of bugs in 20% of modules                    |
| 5   | Pesticide paradox         | Same tests stop finding new bugs → update them   |
| 6   | Context dependent         | Different apps need different testing strategies |
| 7   | Absence of errors fallacy | No bugs ≠ right product; user needs matter       |

---
## [[Test Plan]]

A **Test Plan** is a formal document that describes the scope, approach, resources, schedule, and activities for software testing. It serves as a roadmap for the testing team, guiding what will be tested, how it will be tested, who will do the testing, and when testing activities will occur.

In simple terms: **A test plan answers the question, "How are we going to test this software?"**

---
## [[Types of Tests]]

Two types of tests in general 

1. Manual Testing
2.  Automated Testing

| Aspect                 | Manual Testing                         | Automated Testing                                 |
| ---------------------- | -------------------------------------- | ------------------------------------------------- |
| **Execution**          | Performed by human testers             | Performed by automation tools                     |
| **Speed**              | Slow                                   | Fast                                              |
| **Accuracy**           | Prone to human error                   | Highly accurate and precise                       |
| **Initial Cost**       | Low (no tools needed)                  | High (tools + script development)                 |
| **Maintenance**        | Low (no scripts to update)             | High (scripts need updating)                      |
| **Reusability**        | Low (same effort each cycle)           | High (scripts reused many times)                  |
| **Best For**           | Exploratory, usability, ad-hoc testing | Regression, load, performance, repetitive testing |
| **Human Judgment**     | Yes                                    | No                                                |
| **Programming Skills** | Not required                           | Required                                          |

---
## [[Test Strategy ]]
## What is a Test Strategy?

A **Test Strategy** is a high-level document or approach that defines **how testing will be carried out** for a software project. It outlines the testing principles, methods, risks, and objectives without going into the specific details of test cases or schedules (which belong to the Test Plan).

In simple terms:

- **Test Strategy** = _What_ testing approach to use and _why_ (strategic)
- **Test Plan** = _How_ and _when_ to execute that strategy (tactical)
- 

| If you want to...                       | Use this strategy |
| --------------------------------------- | ----------------- |
| Find defects before writing any code    | **Static**        |
| Test internal logic and data flows      | **Structural**    |
| Test what the user actually experiences | **Behavioural**   |

---
## [[Verification and Validation]]

**Verification and Validation (V&V)** is the process of **investigating whether a software system satisfies specifications and standards and fulfills the required purpose**.

The system should be **verified and validated at each stage** of the software development process using documents produced in earlier stages. V&V thus starts with requirements reviews and continues through design and code reviews to product testing.

---

## [[Software Quality Management ]]

**Software Quality Management (SQM)** is a **management process** aimed at **developing and managing** the quality of software to ensure the product meets customer expectations, regulatory standards, and developer requirements.

Software quality managers use a **cyclical process-based** quality assessment to test software before release and identify and fix bugs.

---

## [[SEI (Software Engineering Institute and its Missions)]]

---
## [[QA Organizational Structure]]

The **QA Organizational Structure** defines how the Quality Assurance team is organized, how reporting lines work, and how different testing functions (functional, automation, performance, environment management) relate to each other and to the rest of the organization.

A key principle is that the structure must provide the **QA manager with direct organizational paths into every department**, while employees continue to report to their **department manager** for disciplinary and non-QA matters.

---
## [[SQA plan]]

A **Software Quality Assurance (SQA) Plan** is a **document that outlines the strategies, processes, and procedures** that will be used to ensure the quality of a software product.

It is typically developed **early** in the software development process and is used to guide the entire development and testing process.

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
