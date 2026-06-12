Here is a detailed explanation of **Earned Value Analysis (EVA)** specifically in the context of monitoring and controlling software project management.

While traditional project tracking often looks at "Are we on schedule?" and "Are we on budget?" as separate questions, Earned Value Analysis integrates these two dimensions to answer a more critical question: **"Are we getting the value we expected for the money and time spent?"**

In software projects—where deliverables are intangible and progress is difficult to measure by simply looking at "lines of code"—EVA provides a quantitative framework to assess health and predict outcomes.

### 1. The Three Fundamental Data Points

To perform EVA, you must first establish three core values based on the project’s scope baseline (the approved budget and schedule):

| Term              | Abbr.            | Definition                                                                                            | Software Context                                                                                                                   |
| :---------------- | :--------------- | :---------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------- |
| **Planned Value** | **PV** (or BCWS) | The authorized budget assigned to the work scheduled to be completed by a specific date.              | *Example:* By the end of Sprint 4, you planned to have completed the "Login API" module, budgeted at \$10,000. PV = \$10,000.      |
| **Actual Cost**   | **AC** (or ACWP) | The total costs actually incurred (labor, licenses, cloud spend) for the work completed by that date. | *Example:* To finish the "Login API," the team worked 20 overtime hours and consumed extra cloud testing resources. AC = \$13,000. |
| **Earned Value**  | **EV** (or BCWP) | The **value** of the work *actually* completed by that date, measured against the original budget.    | *Example:* The "Login API" is 100% done. Its budgeted value was \$10,000. EV = \$10,000.                                           |
[[Example for PV(planned value), AC (Actual cost), EV(Earned Value]]


---

![[Pasted image 20260402071527.png]]

### 2. The Variance Analysis (Monitoring)

During the **monitoring** phase, the project manager calculates variances to see if the project is deviating from the plan.

#### A. Schedule Variance (SV)
**Formula:** $ SV = EV - PV $
- **Interpretation:** This tells you if you are ahead or behind schedule in **dollar terms** (not time).


#### B. Cost Variance (CV)
**Formula:** $ CV = EV - AC $
- **Interpretation:** This tells you if you are under or over budget for the work completed.

### 3. The Performance Indices (Control & Forecasting)

While variances tell you *where you are*, performance indices allow you to **control** the future and **forecast** the final outcome.

| Index                                | Formula           | Significance in Software                                                                                                                                                                              |
| :----------------------------------- | :---------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Cost Performance Index (CPI)**     | $ CPI = EV / AC $ | **The efficiency ratio.** If CPI is < 1.0, you are overspending. In software, a CPI below 0.9 often triggers a review of the development process (e.g., is the team wasting time on technical debt?). |
| **Schedule Performance Index (SPI)** | $ SPI = EV / PV $ | **The progress efficiency.** If SPI is < 1.0, you are behind schedule. In Agile contexts, this correlates to the team’s velocity against the release plan.                                            |


### 6. Summary for Monitoring and Control

In the context of software project management monitoring and control, Earned Value Analysis serves as the **early warning system**.

1.  **Monitoring:** It distinguishes between a project that is "bad" because it is slow (low SPI) versus one that is "bad" because it is wasteful (low CPI).
2.  **Control:** It forces corrective action.
    - If **CPI is low**: The manager must address efficiency—automate builds, fix technical debt, or renegotiate vendor contracts.
    - If **SPI is low**: The manager must address scope—reduce features for the release (MVP) or add resources (though adding resources to a late software project often makes it later, per Brooks' Law).
3.  **Forecasting:** It provides stakeholders with data-driven predictions (EAC) so there are no "surprises" regarding the final budget at the end of the project lifecycle.

By using EVA, a software project manager moves from subjective status reporting ("I think we are about 80% done and maybe a little over budget") to objective performance metrics ("We have an SPI of 0.9 and a CPI of 0.7; based on this, we will exhaust the budget in 6 weeks, requiring a scope reduction of 20% to meet the deadline").


---
---
## Formulas for Earned Value, Planned Value and actual cost

Here are the formulas in a clean, plain-text format that you can copy and paste directly into Obsidian:



## Planned Value (PV)

**Formula:**

PV = Planned Percentage Complete × Budget at Completion (BAC)

**Alternative:**

PV = BAC × (Planned Time Elapsed / Total Project Duration)



## Actual Cost (AC)

**Formula:**

AC = Sum of all costs actually incurred for work completed to date



## Earned Value (EV)

**Formula:**

EV = Actual Percentage Complete × BAC

**Alternative:**

EV = BAC × (Work Actually Completed / Total Scope)



## Summary Table

| Metric | Formula | What It Answers |
|-------|--------|-----------------|
| PV | PV = Planned % Complete × BAC | What should we have spent by now? |
| AC | AC = Sum of actual costs incurred | What did we actually spend? |
| EV | EV = Actual % Complete × BAC | What value did we actually get? |

---

## Software Project Example

Given:
- BAC = $200,000
- Duration = 20 weeks
- End of Week 10 (planned completion = 50%)
- Actual work completed = 40%
- Actual costs incurred = $120,000

| Metric | Calculation | Result |
|-------|------------|--------|
| PV | 50% × $200,000 | $100,000 |
| AC | Actual costs | $120,000 |
| EV | 40% × $200,000 | $80,000 |

---

## Key Relationships

- If EV >= PV: Ahead of schedule
- If EV >= AC: Under budget
- If EV < AC: Over budget
- If EV < PV: Behind schedule

---
---
## [[Advantages and Disadvantages of Earned Value Analysis]]

|Advantages|Disadvantages|
|---|---|
|Project Performance Measurement|Complexity|
|Objective Performance Metrics|Resource-Intensive|
|Integration of Cost and Schedule|Subjectivity in EV Calculation|
|Early Issue Identification|Assumption of Linear Progression|
|Benchmarking|Time-Consuming|
|Effective Communication|Focus on Metrics Rather than Problems|

---
---

## TU practice Questions 

![[Pasted image 20260402072744.png]]
![[Pasted image 20260402072752.png]]![[Pasted image 20260402072801.png]]