## Precedence Diagramming Method (PDM) Explained

Based on the content you provided, let me explain PDM in a clear, structured way.



## What is PDM?

The **Precedence Diagramming Method (PDM)** is a project scheduling technique used to visually represent the **logical relationships and dependencies** among project activities.

### Key Characteristics

| Feature | Description |
|---------|-------------|
| **Representation** | Activities = Nodes (boxes), Dependencies = Arrows |
| **Also Known As** | Activity-on-Node (AON) |
| **Purpose** | Create accurate and flexible project schedule network diagrams |
| **Advantage** | Supports multiple types of activity relationships |



## Why PDM Was Developed

| Older Methods (PERT/CPM) | PDM |
|--------------------------|-----|
| Limited to **Finish-to-Start (FS)** relationships only | Supports **four types** of dependency relationships |
| Less flexible for real-world scenarios | More realistic schedule representation |
| Couldn't represent overlapping activities | Can show overlapping and parallel work |



## The Four Task Dependency Relationships in PDM
![[Pasted image 20260329093332.png]]

### 1. Finish-to-Start (FS)

**Rule:** Task Y cannot start until Task X finishes.

```
[X] ──FS──► [Y]
```

| Aspect | Description |
|--------|-------------|
| **Meaning** | X must finish before Y can start |
| **Common Name** | "Finish-start" |
| **Usage** | Most common relationship type |
| **Example** | Coding (X) must finish before Testing (Y) can start |



### 2. Start-to-Start (SS)

**Rule:** Task Y cannot start until Task X starts.

```
[X] ──SS──► [Y]
```

| Aspect | Description |
|--------|-------------|
| **Meaning** | X must start before Y can start |
| **Common Name** | "Start-start" |
| **Usage** | Activities that can happen in parallel but need to begin together |
| **Example** | Design (X) and Coding (Y) can start simultaneously, but coding can't start before design begins |



### 3. Finish-to-Finish (FF)

**Rule:** Task Y cannot finish until Task X finishes.

```
[X] ──FF──► [Y]
```

| Aspect | Description |
|--------|-------------|
| **Meaning** | X must finish before Y can finish |
| **Common Name** | "Finish-finish" |
| **Usage** | Activities that must end together |
| **Example** | Testing (X) and Documentation (Y) must both finish before deployment |



### 4. Start-to-Finish (SF)

**Rule:** Task Y cannot finish until Task X starts.

```
[X] ──SF──► [Y]
```

| Aspect | Description |
|--------|-------------|
| **Meaning** | X must start before Y can finish |
| **Common Name** | "Start-finish" |
| **Usage** | Least common relationship type |
| **Example** | New shift (X) must start before current shift (Y) can finish |



## Visual Summary of Dependency Types

| Dependency | Diagram | Meaning | Example |
|------------|---------|---------|---------|
| **FS** | X → Y | X finishes before Y starts | Design → Coding |
| **SS** | X → Y | X starts before Y starts | Design starts → Coding starts |
| **FF** | X → Y | X finishes before Y finishes | Testing finishes → Documentation finishes |
| **SF** | X → Y | X starts before Y finishes | New shift starts → Old shift finishes |



## PDM Diagram Example

Here's a PDM network showing multiple dependency types:

```
┌─────────┐     FS     ┌─────────┐
│ Design  │ ────────► │ Coding  │
│ (5 days)│           │ (10 days)│
└─────────┘           └─────────┘
                           │
                           │ SS
                           ▼
                      ┌─────────┐
                      │ Testing │
                      │ (4 days)│
                      └─────────┘
                           │
                           │ FF
                           ▼
                      ┌─────────┐
                      │  Docs   │
                      │ (3 days)│
                      └─────────┘
```




## PDM vs Traditional Methods

| Aspect | Traditional (PERT/CPM) | PDM |
|--------|------------------------|-----|
| **Dependency Types** | Only FS | FS, SS, FF, SF |
| **Flexibility** | Limited | High |
| **Realism** | Less realistic | More realistic |
| **Overlapping Activities** | Not supported | Fully supported |
| **Dummy Activities** | Sometimes needed | Not needed |



## Why PDM is Important

| Benefit | Explanation |
|---------|-------------|
| **More Realistic Scheduling** | Can model overlapping activities (SS) and parallel work (FF) |
| **Better Resource Planning** | Shows when resources are actually needed |
| **Improved Accuracy** | Reflects real-world project constraints |
| **Flexibility** | Accommodates different types of logical relationships |
| **Industry Standard** | Used by MS Project, Primavera, and other scheduling software |




PDM was developed to overcome the limitations of earlier techniques (PERT/CPM) that were restricted to only Finish-to-Start relationships, allowing for more realistic project scheduling.


---

[[Types of dependencies]]

Based on the content you provided, let me explain the **four types of dependencies** used in the Precedence Diagramming Method (PDM). These dependencies help project managers determine the logical relationships between activities for proper sequencing and scheduling.

## Overview

In PDM, dependencies define **how activities relate to each other**. They are categorized based on:

- **Nature of the relationship** (mandatory vs. discretionary)
- **Source of the relationship** (internal vs. external)

---
Diagramming method


![[Pasted image 20260329094422.png]]
![[Pasted image 20260329094427.png]]

---

![[Pasted image 20260329094446.png]]


---
## Shortening Project Duration
![[Pasted image 20260329094945.png]]
![[Pasted image 20260329094955.png]]
![[Pasted image 20260329095000.png]]