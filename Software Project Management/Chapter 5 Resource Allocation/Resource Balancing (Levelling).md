## Resource Balancing (Leveling)

**Resource leveling** (also called resource balancing) is a resource optimization technique where project start and end dates are adjusted to resolve resource conflicts, with the primary constraint being **fixed resource limits** rather than a fixed timeline.

Unlike resource smoothing (which keeps the deadline fixed), resource leveling **allows the project timeline to extend** to accommodate resource availability.

---

## Core Concept

The fundamental difference:

| Technique | Constraint | What Gives |
|-----------|------------|-----------|
| **Resource Leveling** | Resource limits are fixed | Timeline may extend |
| **Resource Smoothing** | Timeline is fixed | Resource usage is adjusted within float |

Resource leveling answers the question: *"Given that I have limited resources, when can this project realistically finish?"*

---

## When to Use Resource Leveling

| Situation                                   | Why Leveling Fits                                                        |
| ------------------------------------------- | ------------------------------------------------------------------------ |
| **Critical resources are limited**          | Only one specialist exists; tasks must be sequenced rather than parallel |
| **Resource availability is fixed**          | No ability to hire or borrow additional resources                        |
| **Timeline is flexible**                    | Project end date is negotiable                                           |
| **Overallocation is severe**                | Cannot be resolved within available float                                |
| **Resource constraints drive the schedule** | Availability, not deadlines, determines the timeline                     |

---

## How Resource Leveling Works

### Basic Approach

1. **Identify overallocations** – Find where resources are scheduled beyond capacity
2. **Delay tasks** – Shift tasks to times when resources are available
3. **Accept timeline extension** – The project end date moves if critical path tasks are delayed
4. **Repeat** – Continue until all resources are within capacity

### Methods

| Method | Description |
|--------|-------------|
| **Critical Path Method (CPM) Leveling** | Delay non-critical tasks first; critical tasks are only delayed if necessary |
| **Critical Chain Method** | Add buffers and focus on resource constraints rather than task dependencies |
| **Heuristic/Software Leveling** | Tools like Microsoft Project use algorithms to automatically level resources |

---

## Example

**Scenario:** A software project requires a senior database architect for three critical tasks. Only one architect is available, and they can only work on one task at a time.

| Task | Duration | Original Schedule | Resource |
|------|----------|-------------------|----------|
| Database Design | 2 weeks | Weeks 1–2 | Senior DB Architect |
| Data Migration | 2 weeks | Weeks 2–3 | Senior DB Architect |
| Performance Tuning | 1 week | Weeks 3–4 | Senior DB Architect |

**Problem:** The architect is overallocated in weeks 2–3 (working on Database Design and Data Migration simultaneously).

**Leveling solution:**

| Task | Duration | Leveled Schedule |
|------|----------|------------------|
| Database Design | 2 weeks | Weeks 1–2 |
| Data Migration | 2 weeks | Weeks 3–4 |
| Performance Tuning | 1 week | Weeks 5–6 |

**Result:** The architect is never overallocated, but the project end date extends from week 4 to week 6.

---

## Impact on Project Parameters

| Parameter | Effect of Leveling |
|-----------|-------------------|
| **Timeline** | Extends (sometimes significantly) |
| **Cost** | May increase due to longer duration (labor, overhead, extended contracts) |
| **Scope** | Unchanged |
| **Resource usage** | Balanced, no overallocations |
| **Critical path** | May change as delays propagate |


---

## Advantages of Resource Leveling

| Advantage | Explanation |
|-----------|-------------|
| **Prevents burnout** | Ensures no resource is overallocated |
| **Realistic scheduling** | Creates schedules that reflect actual resource availability |
| **Reduces risk** | Avoids the chaos of overcommitted resources |
| **Improves quality** | Sustainable workloads lead to better output |
| **Enables resource-limited planning** | Works within real constraints rather than ideal assumptions |

---

## Disadvantages of Resource Leveling

| Disadvantage | Explanation |
|--------------|-------------|
| **Timeline extension** | Projects take longer, potentially missing market windows |
| **Increased cost** | Longer duration typically increases total project cost |
| **Stakeholder impact** | Extended deadlines may disappoint stakeholders |
| **Complexity** | Leveling can be complex to calculate manually |
| **May hide inefficiencies** | Can mask underlying issues like poor estimation or inefficient processes |

---

## When Leveling is Unavoidable

Some scenarios make leveling the only viable option:

| Scenario | Why Leveling is Required |
|----------|-------------------------|
| **Single subject matter expert** | Only one person possesses a critical skill; tasks must be sequenced |
| **No hiring budget** | Additional resources cannot be brought in |
| **Specialized equipment** | Only one testing environment or license exists |
| **Regulatory constraints** | Compliance requires specific personnel for specific phases |
| **Fixed team size** | Organization cannot reallocate people from other projects |

---

## Example: Software Project Leveling

**Project:** Mobile app development with only one iOS developer

| Task | Duration | Dependency |
|------|----------|------------|
| iOS App Setup | 1 week | — |
| Core Features | 3 weeks | iOS App Setup |
| Payment Integration | 2 weeks | Core Features |
| App Store Submission | 1 week | Payment Integration |

**Problem:** The single iOS developer must work sequentially on all iOS tasks.

**Leveled schedule:**
- iOS App Setup: Weeks 1–2 (spread due to other tasks)
- Core Features: Weeks 3–5
- Payment Integration: Weeks 6–7
- App Store Submission: Week 8

**Result:** Timeline extends to accommodate the single resource constraint, but the developer is never overallocated.

---

## Tools for Resource Leveling

| Tool | Leveling Features |
|------|------------------|
| **Microsoft Project** | Automatic and manual leveling algorithms |
| **Jira + Portfolio** | Capacity planning and resource-aware scheduling |
| **Primavera P6** | Advanced leveling for complex projects |
| **Smartsheet** | Resource management with leveling capabilities |
| **Excel** | Manual leveling using formulas and manual adjustments |

---

## Summary

**Resource leveling** is the technique of balancing resource usage by **allowing the project timeline to extend**. It is used when:

- Resource availability is the primary constraint
- Overallocation cannot be resolved within existing float
- The timeline is flexible or negotiable

The trade-off is simple: **extended timeline in exchange for balanced, sustainable resource usage**.

Where smoothing says *"We must deliver on time, so we'll redistribute work within that constraint,"* leveling says *"We have limited resources, so we'll let the timeline reflect that reality."*