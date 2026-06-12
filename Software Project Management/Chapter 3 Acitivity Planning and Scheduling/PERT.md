![[Pasted image 20260328090057.png]]


Here's an explanation of the **PERT (Program Evaluation and Review Technique)** network planning model:

---

## What Is PERT?

**PERT** is a network planning technique used to analyze and represent the tasks involved in completing a project. It was developed in the 1950s for the U.S. Navy's Polaris missile project to handle uncertainty in activity durations. Unlike CPM which uses a single time estimate, PERT uses **three time estimates** to account for variability and risk.

---

## Key Concept: Three Time Estimates

PERT recognizes that activity durations are often uncertain. Instead of a single estimate, it uses:

| Estimate             | Symbol         | Meaning                                                            |
| -------------------- | -------------- | ------------------------------------------------------------------ |
| **Optimistic Time**  | **O** or **a** | The minimum time if everything goes perfectly (best-case scenario) |
| **Most Likely Time** | **M** or **m** | The time most likely to be needed (realistic scenario)             |
| **Pessimistic Time** | **P** or **b** | The maximum time if everything goes wrong (worst-case scenario)    |

---

## PERT Formula

The **expected time** for each activity is calculated using a weighted average:

```
Expected Time (TE) = (O + 4M + P) / 6
```

The formula gives **4 times more weight** to the most likely estimate, balancing optimism and pessimism.

### Variance Formula

To measure uncertainty, PERT also calculates **variance** for each activity:

```
Variance (σ²) = [(P - O) / 6]²
```

A higher variance indicates more uncertainty in the activity duration.

---


## PERT Calculation Example

Let's calculate for a single activity:

**Activity: "Code Login Module"**
- Optimistic (O) = 3 days
- Most Likely (M) = 5 days
- Pessimistic (P) = 10 days

```
Expected Time = (3 + 4×5 + 10) / 6
             = (3 + 20 + 10) / 6
             = 33 / 6
             = 5.5 days

Variance = [(10 - 3) / 6]²
         = (7 / 6)²
         = (1.17)²
         = 1.36
```

This means the activity is expected to take **5.5 days**, with a variance of **1.36** (higher variance indicates more uncertainty).


---

## PERT vs CPM Comparison

| Aspect | PERT | CPM |
|--------|------|-----|
| **Time Estimates** | Three (O, M, P) | Single |
| **Focus** | Time and uncertainty | Time and cost trade-offs |
| **Best For** | R&D, new projects, high uncertainty | Construction, repetitive projects, low uncertainty |
| **Probability Analysis** | Yes | No |
| **Complexity** | Higher | Lower |

---

## In Simple Terms

Think of PERT as **planning with a safety margin**:

- **Without PERT**: You assume every task will take exactly the time you guess. If anything goes wrong, your schedule breaks.
- **With PERT**: You ask, "What's the best case? What's the worst case? What's most likely?" Then you calculate a realistic schedule with built-in awareness of risks.

It's like planning a road trip:
- **Optimistic**: 4 hours (no traffic, perfect weather)
- **Most Likely**: 5 hours (some traffic, one stop)
- **Pessimistic**: 7 hours (heavy traffic, construction, rain)

PERT gives you an **expected time of 5.2 hours** and tells you there's an 85% chance you'll arrive within 6 hours. This helps you set realistic expectations and build contingency into your schedule.

---
---
[[Sir ko slides ko explanation ]]

---
[[Question ]]
![[Pasted image 20260329092500.png]]


![[Pasted image 20260329092743.png]]