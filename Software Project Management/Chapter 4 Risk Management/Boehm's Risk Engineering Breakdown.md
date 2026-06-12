![[Pasted image 20260329170521.png]]

This image provides a detailed breakdown of **Barry Boehm’s Risk Engineering** framework. It organizes risk management into two major phases: **Risk Assessment** (understanding the risks) and **Risk Control** (taking action against them).

Here is the complete explanation based on your image.

---

## Overview of Boehm’s Risk Engineering

Boehm divides risk management into two main categories:

| Phase | Purpose | Question it Answers |
|-------|---------|---------------------|
| **Risk Assessment** | Identify and analyze risks | *"What could go wrong and how bad is it?"* |
| **Risk Control** | Prioritize and resolve risks | *"What are we going to do about it?"* |

---

## Part 1: Risk Assessment

This phase is about **finding and understanding** risks.

### 1.1 Risk Identification

**Purpose:** Discover potential risks.

| Technique | What It Is | Example |
|-----------|-----------|---------|
| **Checklist** | Use a predefined list of common risks | "Personnel shortfall, unrealistic schedule, technology change..." |
| **Design analysis** | Examine the system design for weak points | "The database design has a single point of failure" |
| **Assumption analysis** | Identify assumptions and test if they are valid | "We assume the API will be stable – but is it?" |
| **Decomposition** | Break the project into smaller parts and analyze each | "Break WBS into tasks and examine each for risks" |

---

### 1.2 Risk Analysis

**Purpose:** Evaluate the probability and impact of identified risks.

| Technique | What It Is | Example |
|-----------|-----------|---------|
| **Performance models** | Simulate system behavior under stress | "Model shows response time degrades at 10,000 users" |
| **Cost models** | Estimate financial impact of risks | "If delayed 2 months, cost overrun = $200,000" |
| **Network analysis** | Analyze task dependencies (PERT/CPM) | "Delay in Task A pushes back Tasks B, C, D" |
| **Design analysis** | Evaluate design alternatives for risk | "Option X has 30% failure risk; Option Y has 10%" |
| **Quality factor analysis** | Assess risks to reliability, security, maintainability | "Low test coverage → high defect risk" |

---

## Part 2: Risk Control

This phase is about **taking action** on risks.

### 2.1 Risk Prioritization

**Purpose:** Decide which risks to address first.

| Concept | Formula / Meaning |
|---------|-------------------|
| **Risk Exposure (RE)** | RE = Probability × Loss (e.g., 0.3 × $100k = $30k) |
| **Risk Leverage** | (RE before - RE after) ÷ Cost of reduction |
| **Risk Reduction** | Actions taken to lower probability or impact |

**Risk Leverage Example:**
- RE before action = $50,000
- RE after action = $10,000
- Cost of action = $5,000
- **Risk Leverage** = ($50,000 - $10,000) ÷ $5,000 = 8.0 (good investment)

---

### 2.2 Risk Planning

**Purpose:** Create strategies to handle risks.

| Strategy | What It Is | Example |
|----------|-----------|---------|
| **Buying information** | Spend time/money to learn more about a risk | Build a prototype to test feasibility |
| **Risk avoidance** | Change the plan to eliminate the risk | Use a stable, proven technology instead of experimental one |
| **Risk transfer** | Shift the risk to someone else | Buy insurance, outsource risky component |
| **Risk reduction** | Lower probability or impact | Add code reviews, cross-train team members |

> **Note:** Your image shows "Buying information" as a parent category, meaning you invest in learning before committing to other strategies.

---

### 2.3 Risk Resolution

**Purpose:** Execute specific actions to resolve risks.

| Technique | What It Is | Example |
|-----------|-----------|---------|
| **Prototypes** | Build a working model to test risky areas | Prototype the user login to test security |
| **Simulations** | Run virtual models of system behavior | Simulate server load to find breaking point |
| **Benchmarks** | Measure performance against standards | Benchmark database query speed |
| **Analysis** | Perform detailed technical review | Code inspection for security vulnerabilities |
| **Staffing** | Assign experts to high-risk areas | Put senior dev on the critical payment module |

---

### 2.4 Risk Monitoring

**Purpose:** Track risks and take corrective action.

| Technique | What It Is | Example |
|-----------|-----------|---------|
| **Milestone tracking** | Check progress at key project points | "Is the architecture review complete by March 15?" |
| **Top 10 tracking** | Maintain and review the top 10 risks weekly | Update list: Risk #3 moved from 30% to 50% probability |
| **Corrective action** | Adjust the plan when a risk becomes real | "API failed – switching to backup vendor now" |

---

## Summary Table

| Phase | Sub-Phase | Key Techniques |
|-------|-----------|----------------|
| **Risk Assessment** | Identification | Checklist, Design analysis, Assumption analysis, Decomposition |
| | Analysis | Performance models, Cost models, Network analysis, Quality factor |
| **Risk Control** | Prioritization | Risk Exposure, Risk Leverage, Risk reduction strategies |
| | Planning | Buying information, Avoidance, Transfer, Reduction |
| | Resolution | Prototypes, Simulations, Benchmarks, Analysis, Staffing |
| | Monitoring | Milestone tracking, Top 10 tracking, Corrective action |

---

## Bottom Line

**Boehm’s Risk Engineering Breakdown** provides a complete, actionable framework:

1. **Assess** risks by identifying and analyzing them
2. **Prioritize** using Risk Exposure and Risk Leverage
3. **Plan** strategies (avoid, transfer, reduce, or buy information)
4. **Resolve** using prototypes, simulations, benchmarks, analysis, or staffing
5. **Monitor** continuously with milestones and Top 10 tracking

> **Key takeaway:** This is not just theory. Every box in your image is a concrete technique you can apply on real software projects.

