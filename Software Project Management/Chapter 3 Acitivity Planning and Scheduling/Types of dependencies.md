## Types of PDM Dependencies

Based on the content you provided, let me explain the **four types of dependencies** used in the Precedence Diagramming Method (PDM). These dependencies help project managers determine the logical relationships between activities for proper sequencing and scheduling.

---

## Overview

In PDM, dependencies define **how activities relate to each other**. They are categorized based on:

- **Nature of the relationship** (mandatory vs. discretionary)
- **Source of the relationship** (internal vs. external)

---

## 1. Mandatory Dependency (Hard Logic)

### Definition
Mandatory dependencies are **inherent and unavoidable relationships** dictated by the **nature of the work** itself. One activity must be completed before another can start due to technical or physical constraints.

### Key Characteristics

| Aspect | Description |
|--------|-------------|
| **Also Known As** | Hard Logic, Physical Constraints |
| **Flexibility** | None - cannot be changed |
| **Source** | Nature of the work |
| **Risk** | High - if delayed, project is delayed |

### Example
> **Software testing cannot begin before the software is developed.**

You cannot test code that doesn't exist yet. This is a physical/technical constraint.

### Other Examples

| Activity A | Activity B | Reason |
|------------|------------|--------|
| Pour concrete | Let concrete cure | Concrete must harden before next step |
| Install foundation | Build walls | Walls need foundation for support |
| Write code | Test code | Testing requires code to exist |
| Dig trench | Lay pipes | Pipes need a trench to go into |

### Why They Matter
These dependencies are **critical** for project success. If a mandatory dependency is missed in scheduling, the project plan becomes impossible to execute.

---

## 2. Discretionary Dependency (Soft Logic)

### Definition
Discretionary dependencies are defined by the **project team based on experience, best practices, or preferences**. Although activities are required, their **sequence can be changed if needed**.

### Key Characteristics

| Aspect | Description |
|--------|-------------|
| **Also Known As** | Soft Logic, Preferred Logic |
| **Flexibility** | High - can be changed |
| **Source** | Team experience, best practices |
| **Risk** | Lower - can be adjusted |

### Example
> **Code documentation may be done after or alongside development.**

Documentation doesn't technically require coding to be 100% complete. The team can choose to do it in parallel or after, based on what works best.

### Other Examples

| Activity A | Activity B | Alternative |
|------------|------------|-------------|
| Design UI | Develop UI | Could do simultaneously |
| Write user manual | Test software | Could do in parallel |
| Create training materials | Deploy system | Could be done before or after |

### Why They Matter
Discretionary dependencies provide **flexibility** in scheduling. Project managers can use them to:
- Optimize resource allocation
- Compress the schedule (fast-tracking)
- Balance workload across teams

---

## 3. External Dependency

### Definition
External dependencies arise from factors **outside the project's control**. These include approvals, regulations, inputs from external organizations, or third-party deliverables.

### Key Characteristics

| Aspect | Description |
|--------|-------------|
| **Control** | Outside project team's control |
| **Source** | External organizations, government, vendors |
| **Risk** | High - difficult to influence |
| **Planning** | Requires buffer time |

### Example
> **A project may require government approval before development can begin.**

The project team cannot start development until an external agency grants permission.

### Other Examples

| External Dependency | Impact |
|---------------------|--------|
| Vendor delivers materials | Construction cannot start |
| Regulatory inspection | Operations cannot begin |
| Client provides requirements | Design cannot start |
| Weather conditions | Outdoor work cannot proceed |
| Import customs clearance | Equipment cannot arrive |

### Why They Matter
External dependencies are **high-risk** because the project team has limited control. Smart project management includes:
- Building **buffer time** for external dependencies
- Starting the approval process **early**
- Having **backup plans** for key external inputs

---

## 4. Internal Dependency

### Definition
Internal dependencies occur **within the project itself** and are **controlled by the project team**. One activity depends on the completion of another project activity.

### Key Characteristics

| Aspect | Description |
|--------|-------------|
| **Control** | Within project team's control |
| **Source** | Internal project activities |
| **Risk** | Manageable - team can influence |
| **Planning** | Directly manageable |

### Example
> **System integration cannot start until all modules are completed.**

Both activities (module development and integration) are managed by the same project team.

### Other Examples

| Internal Dependency | Relationship |
|---------------------|--------------|
| Requirements approved → Design starts | FS |
| Design completed → Development starts | FS |
| Development completed → Testing starts | FS |
| Testing completed → Deployment starts | FS |

### Why They Matter
Internal dependencies are **within the team's control**, making them easier to manage. The team can:
- Adjust resources between activities
- Resolve bottlenecks internally
- Coordinate directly with dependent teams

---

## Summary Table: Four Types of PDM Dependencies

| Type | Also Known As | Source | Flexibility | Control | Example |
|------|---------------|--------|-------------|---------|---------|
| **Mandatory** | Hard Logic | Nature of work | None (fixed) | Technical constraint | Concrete must cure before next step |
| **Discretionary** | Soft Logic | Team preference | High (flexible) | Project team | Code docs during or after coding |
| **External** | Third-party | Outside project | None | External | Government approval needed |
| **Internal** | Project | Inside project | Manageable | Project team | Module completion → integration |

---

## Visual Classification

```
                    ┌─────────────────────────────────────────┐
                    │           DEPENDENCY TYPES              │
                    └─────────────────────────────────────────┘
                                      │
            ┌─────────────────────────┴─────────────────────────┐
            │                                                   │
            ▼                                                   ▼
┌───────────────────────┐                           ┌───────────────────────┐
│   BY NATURE/LOGIC     │                           │    BY SOURCE          │
├───────────────────────┤                           ├───────────────────────┤
│                       │                           │                       │
│  • Mandatory          │                           │  • Internal           │
│    (Hard Logic)       │                           │    (Inside project)   │
│                       │                           │                       │
│  • Discretionary      │                           │  • External           │
│    (Soft Logic)       │                           │    (Outside project)  │
│                       │                           │                       │
└───────────────────────┘                           └───────────────────────┘
```

---

## Practical Application: When to Use Each

| Dependency Type | Best Used When | Caution |
|-----------------|----------------|---------|
| **Mandatory** | Technical constraints exist | Cannot be compressed or changed |
| **Discretionary** | Team has flexibility in sequencing | Avoid over-optimizing; document rationale |
| **External** | Third parties involved | Build buffer time; start early |
| **Internal** | Activities within team control | Manage actively; track closely |

---

## Combining with Logical Relationships

These dependency types work alongside the **logical relationships** (FS, SS, FF, SF):

| Logical Relationship | Can Be Combined With |
|---------------------|---------------------|
| **FS (Finish-to-Start)** | Mandatory, Discretionary, Internal, External |
| **SS (Start-to-Start)** | Usually Discretionary or Internal |
| **FF (Finish-to-Finish)** | Usually Discretionary or Internal |
| **SF (Start-to-Finish)** | Rare; usually Mandatory or External |

---

## Summary

| Dependency Type | Key Takeaway |
|-----------------|--------------|
| **Mandatory** | Unavoidable - dictated by the work itself |
| **Discretionary** | Flexible - based on team preference/best practices |
| **External** | Outside control - from vendors, government, etc. |
| **Internal** | Within control - between project activities |

Understanding these four types helps project managers:
1. **Identify** all dependencies correctly
2. **Sequence** activities logically
3. **Manage risk** associated with external and mandatory dependencies
4. **Optimize schedule** using discretionary dependencies for fast-tracking