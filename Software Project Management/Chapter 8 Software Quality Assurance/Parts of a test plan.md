### 1. Test Plan ID

**Description:** A unique identifier that defines the test plan. It can be a number, a name, or a mix of both, as per convenience.

**Purpose:** Helps uniquely identify and reference the test plan across project documentation.

**Example:** `TP-LoginModule-v2.1` or `TP-2025-001`



### 2. Test Environment

**Description:** Defines what kind of environment is needed for testing to be carried out.

**Purpose:** Ensures the necessary hardware, software, network, and tools are available before testing begins.

**Example:** In device testing, usually a virtual setup is made to test emergency calling.

**Other examples:**  
- Operating systems (Windows 11, macOS, iOS 17)  
- Browsers (Chrome 120, Safari 17)  
- Databases (PostgreSQL 15, MySQL 8)  
- Virtual machines or cloud instances (AWS EC2, Docker containers)



### 3. Features to be Tested / Not Tested

**Description:** Contains all details about which features the tester needs to test and which features are not tested (either because they are not yet implemented or not included in this particular release).

**Purpose:** Sets clear boundaries for testing scope, preventing wasted effort and managing stakeholder expectations.

**Example:**  
- **Tested:** User login, password reset, dashboard navigation  
- **Not Tested:** Payment gateway (not implemented yet), analytics module (deferred to next release)



### 4. Entry / Exit Criteria

**Description:** Terms that define when to start or stop testing. Standards are defined under the test strategy and followed by testers in the test plan.

**Purpose:** Provides objective conditions to begin and end testing activities, preventing premature or delayed testing.

| Criteria | Meaning | Example |
|----------|---------|---------|
| **Entry Criteria** | Conditions to start testing | All code is deployed to test environment; test data is ready; no critical open bugs blocking testing |
| **Exit Criteria** | Conditions to stop testing | All planned test cases executed; 100% of critical defects fixed; 95% pass rate for high-priority tests |



### 5. Status

**Description:** Whether a test case is passed, failed, or not tested. All test results are included in the test plan with a proper reason.

**Purpose:** Tracks testing progress and provides visibility into software quality.

**Example:**  

| Test Case ID | Status | Reason (if not passed or not tested) |
|--------------|--------|--------------------------------------|
| TC-LOGIN-01 | Passed | – |
| TC-LOGIN-02 | Failed | Incorrect error message for empty password |
| TC-LOGIN-03 | Not Tested | Test environment crashed during execution |



### 6. Types of Testing

**Description:** The types of testing required (e.g., regression, functional, non-functional, stress) are defined and then executed by the respective tester.

**Purpose:** Clarifies which testing techniques will be applied, ensuring appropriate coverage.

**Common types:**  
- **Functional testing** – Validating features work as specified  
- **Regression testing** – Ensuring new code doesn't break existing features  
- **Non-functional testing** – Performance, security, usability, reliability  
- **Stress testing** – System behavior under extreme load


### 7. Brief Introduction

**Description:** A brief introduction is sometimes included so that if any new member joins the team, they can get an idea of how things work.

**Purpose:** Provides context and onboarding support for new testers or stakeholders.

**Typical content:**  
- Project background  
- Testing objectives  
- Key contacts  
- High-level approach  
- References to related documents (test strategy, requirements)


## Practical Takeaway for Software Project Managers

A well-structured test plan ensures that testing is **systematic, traceable, and manageable**. Include these seven components even in lightweight test plans for smaller projects. The **Entry/Exit Criteria** and **Features Not Tested** sections are particularly important for managing client expectations and avoiding disputes over release readiness.