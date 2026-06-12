
Here is a **detailed, step-by-step explanation** of how **Evaluating Risk to the Schedule using Z-Values** works, using a complete example from start to finish.

---

## The Big Picture

**What are we trying to do?**

We want to answer questions like:
- *"What is the probability that we will finish the project in 60 days?"*
- *"If we want to be 95% confident, what deadline should we promise?"*

**How does Z-Value help?**

Z-Value tells you how many **standard deviations** your target date is from your expected date. Then we convert that to a **probability percentage**.

---

## Complete Step-by-Step Example

### Project: Building a Mobile App Feature

We have 4 tasks on the **critical path** (the chain of tasks that determines project duration).

---

### Step 1: Get 3 Estimates for Each Task (PERT)

For each task, we need three time estimates (in days):

| Term | Meaning | How to get it |
|------|---------|---------------|
| **O (Optimistic)** | Best case – everything goes perfectly | Ask team: "Fastest possible?" |
| **M (Most Likely)** | Realistic case – normal challenges | Ask team: "What's most realistic?" |
| **P (Pessimistic)** | Worst case – everything goes wrong | Ask team: "Slowest possible?" |

---

### Step 2: Calculate Expected Duration (TE) for Each Task

**Formula:**
```
TE = (O + 4M + P) ÷ 6
```

This gives more weight to the "Most Likely" estimate (4x) than optimistic or pessimistic.

#### Task 1: Requirements Gathering

| Estimate | Days |
|----------|------|
| Optimistic (O) | 5 |
| Most Likely (M) | 8 |
| Pessimistic (P) | 15 |

```
TE = (5 + 4×8 + 15) ÷ 6
    = (5 + 32 + 15) ÷ 6
    = 52 ÷ 6
    = 8.67 days
```

#### Task 2: Design

| Estimate | Days |
|----------|------|
| O | 4 |
| M | 6 |
| P | 10 |

```
TE = (4 + 4×6 + 10) ÷ 6
    = (4 + 24 + 10) ÷ 6
    = 38 ÷ 6
    = 6.33 days
```

#### Task 3: Coding

| Estimate | Days |
|----------|------|
| O | 10 |
| M | 15 |
| P | 30 |

```
TE = (10 + 4×15 + 30) ÷ 6
    = (10 + 60 + 30) ÷ 6
    = 100 ÷ 6
    = 16.67 days
```

#### Task 4: Testing

| Estimate | Days |
|----------|------|
| O | 6 |
| M | 10 |
| P | 20 |

```
TE = (6 + 4×10 + 20) ÷ 6
    = (6 + 40 + 20) ÷ 6
    = 66 ÷ 6
    = 11.0 days
```

---

### Step 3: Calculate Variance (σ²) for Each Task

**Formula:**
```
σ² = [(P - O) ÷ 6]²
```

Variance measures **uncertainty** – the wider the gap between Pessimistic and Optimistic, the higher the variance.

#### Task 1: Requirements
```
σ² = [(15 - 5) ÷ 6]²
    = [10 ÷ 6]²
    = [1.67]²
    = 2.78
```

#### Task 2: Design
```
σ² = [(10 - 4) ÷ 6]²
    = [6 ÷ 6]²
    = [1]²
    = 1.0
```

#### Task 3: Coding
```
σ² = [(30 - 10) ÷ 6]²
    = [20 ÷ 6]²
    = [3.33]²
    = 11.09
```

#### Task 4: Testing
```
σ² = [(20 - 6) ÷ 6]²
    = [14 ÷ 6]²
    = [2.33]²
    = 5.43
```

---

### Step 4: Calculate Project Expected Duration

**Formula:**
```
Project TE = Sum of all task TEs
```

```
Project TE = 8.67 + 6.33 + 16.67 + 11.0
          = 42.67 days
```

> **Meaning:** Based on realistic estimates, we expect the project to take **about 43 days**.

---

### Step 5: Calculate Project Variance

**Formula:**
```
Project σ² = Sum of all task variances
```

```
Project σ² = 2.78 + 1.0 + 11.09 + 5.43
           = 20.3
```

---

### Step 6: Calculate Project Standard Deviation

**Formula:**
```
Project σ = √(Project σ²)
```

```
Project σ = √20.3 = 4.51 days
```

> **Meaning:** The typical uncertainty in our schedule is about **4.5 days**. This is our "risk measure."

---

### Step 7: Calculate Z-Value for a Target Date

**Formula:**
```
Z = (Target Date - Project TE) ÷ Project σ
```

#### Scenario A: Target Date = 43 days (exactly expected)

```
Z = (43 - 42.67) ÷ 4.51
    = 0.33 ÷ 4.51
    = 0.07
```

#### Scenario B: Target Date = 50 days (comfortable)

```
Z = (50 - 42.67) ÷ 4.51
    = 7.33 ÷ 4.51
    = 1.63
```

#### Scenario C: Target Date = 38 days (aggressive)

```
Z = (38 - 42.67) ÷ 4.51
    = -4.67 ÷ 4.51
    = -1.04
```

---

### Step 8: Convert Z-Value to Probability

Use a **Z-table** (Standard Normal Distribution). Here are key values:

| Z-Value | Probability | Meaning |
|---------|-------------|---------|
| 0.0 | 50% | Even chance |
| 0.5 | 69% | Better than 2 in 3 |
| 1.0 | 84% | About 5 in 6 |
| 1.65 | 95% | Very confident |
| 2.0 | 97.7% | Extremely confident |
| -1.0 | 16% | Only 1 in 6 chance |

#### Our Scenarios:

| Scenario | Z-Value | Probability | Interpretation |
|----------|---------|-------------|----------------|
| **A: 43 days** | 0.07 | ~52% | Almost even chance – very risky promise |
| **B: 50 days** | 1.63 | ~95% | Very high confidence – safe promise |
| **C: 38 days** | -1.04 | ~15% | Very low chance – unrealistic deadline |

---

### Step 9: Set a Confident Deadline (Reverse Calculation)

**Question:** *"What deadline gives us 95% confidence?"*

From Z-table, 95% probability corresponds to **Z = 1.65**

**Formula:**
```
Confident Target = Project TE + (Z × Project σ)
```

```
95% Confident Date = 42.67 + (1.65 × 4.51)
                   = 42.67 + 7.44
                   = 50.11 days
```

> **Answer:** Promise **50 days** to have 95% confidence in meeting the deadline.

---

## Complete Summary Table

| Step | What We Did | Result |
|------|-------------|--------|
| 1 | Got 3 estimates for each task | O, M, P values |
| 2 | Calculated Expected Duration (TE) | Task TEs: 8.67, 6.33, 16.67, 11.0 |
| 3 | Calculated Variance (σ²) | Task variances: 2.78, 1.0, 11.09, 5.43 |
| 4 | Summed TEs → Project TE | 42.67 days |
| 5 | Summed variances → Project σ² | 20.3 |
| 6 | Square root → Project σ | 4.51 days |
| 7 | Calculated Z for target dates | 43d: Z=0.07, 50d: Z=1.63, 38d: Z=-1.04 |
| 8 | Converted Z to probability | 43d: 52%, 50d: 95%, 38d: 15% |
| 9 | Set 95% confident deadline | 50.11 days |

---

## Visual Representation

```
                    Project Expected = 42.67 days
                              |
                              ▼
    ────┬────┬────┬────┬────┬────┬────┬────┬────┬────► Days
       30   35   40   42.67 45   50   55
                    │         │
                    │         └── 95% confident (50 days)
                    │
                    └── 50% chance (42.67 days)

    Z = -1.04    Z = 0    Z = 1.63
    (15% chance)  (52%)    (95% chance)
```

---

## Practical Takeaways

| If You Want... | Then... |
|----------------|---------|
| A realistic deadline | Use Expected Date (50% chance) |
| A safe deadline | Use Expected + 1.65σ (95% chance) |
| To understand risk | Look at Standard Deviation (σ) |
| To compare two target dates | Calculate Z for each |

---

## Bottom Line

**Z-Value analysis in 3 sentences:**

1. Calculate your **expected project duration** and **standard deviation** from 3-point estimates.
2. **Z = (Target - Expected) ÷ Standard Deviation** – positive Z means good chance, negative Z means risky.
3. Convert Z to probability using a Z-table, or set a confident deadline by adding `1.65 × σ` to your expected date.

> **Key takeaway:** Never promise a single date. Use Z-values to understand your risk and set realistic expectations with stakeholders.


---
Z value bata kasari Probability nikaleko??


Excellent question! You are absolutely right. The conversion from a Z-value to a probability is done using a **Standard Normal Distribution Table** (also called a Z-table).

Let me explain exactly how to read this table, step by step.

---

## The Core Concept

The Z-value tells you how many **standard deviations** you are away from the mean (expected date). The Z-table then tells you: *"What is the probability that we will finish **on or before** this target date?"*

**Important:** The Z-table assumes a perfect bell-shaped curve (normal distribution) around your expected date.

---

## The Z-Table (Standard Normal Distribution)

Here is a simplified version of a Z-table. It shows probabilities for positive Z-values (target date is **after** the expected date).

| Z | 0.00 | 0.01 | 0.02 | 0.03 | 0.04 | 0.05 | 0.06 | 0.07 | 0.08 | 0.09 |
|---|------|------|------|------|------|------|------|------|------|------|
| 0.0 | 0.5000 | 0.5040 | 0.5080 | 0.5120 | 0.5160 | 0.5199 | 0.5239 | 0.5279 | 0.5319 | 0.5359 |
| 0.1 | 0.5398 | 0.5438 | 0.5478 | 0.5517 | 0.5557 | 0.5596 | 0.5636 | 0.5675 | 0.5714 | 0.5753 |
| 0.2 | 0.5793 | 0.5832 | 0.5871 | 0.5910 | 0.5948 | 0.5987 | 0.6026 | 0.6064 | 0.6103 | 0.6141 |
| 0.3 | 0.6179 | 0.6217 | 0.6255 | 0.6293 | 0.6331 | 0.6368 | 0.6406 | 0.6443 | 0.6480 | 0.6517 |
| 0.4 | 0.6554 | 0.6591 | 0.6628 | 0.6664 | 0.6700 | 0.6736 | 0.6772 | 0.6808 | 0.6844 | 0.6879 |
| 0.5 | 0.6915 | 0.6950 | 0.6985 | 0.7019 | 0.7054 | 0.7088 | 0.7123 | 0.7157 | 0.7190 | 0.7224 |
| 0.6 | 0.7257 | 0.7291 | 0.7324 | 0.7357 | 0.7389 | 0.7422 | 0.7454 | 0.7486 | 0.7517 | 0.7549 |
| 0.7 | 0.7580 | 0.7611 | 0.7642 | 0.7673 | 0.7704 | 0.7734 | 0.7764 | 0.7794 | 0.7823 | 0.7852 |
| 0.8 | 0.7881 | 0.7910 | 0.7939 | 0.7967 | 0.7995 | 0.8023 | 0.8051 | 0.8078 | 0.8106 | 0.8133 |
| 0.9 | 0.8159 | 0.8186 | 0.8212 | 0.8238 | 0.8264 | 0.8289 | 0.8315 | 0.8340 | 0.8365 | 0.8389 |
| 1.0 | 0.8413 | 0.8438 | 0.8461 | 0.8485 | 0.8508 | 0.8531 | 0.8554 | 0.8577 | 0.8599 | 0.8621 |
| 1.1 | 0.8643 | 0.8665 | 0.8686 | 0.8708 | 0.8729 | 0.8749 | 0.8770 | 0.8790 | 0.8810 | 0.8830 |
| 1.2 | 0.8849 | 0.8869 | 0.8888 | 0.8907 | 0.8925 | 0.8944 | 0.8962 | 0.8980 | 0.8997 | 0.9015 |
| 1.3 | 0.9032 | 0.9049 | 0.9066 | 0.9082 | 0.9099 | 0.9115 | 0.9131 | 0.9147 | 0.9162 | 0.9177 |
| 1.4 | 0.9192 | 0.9207 | 0.9222 | 0.9236 | 0.9251 | 0.9265 | 0.9279 | 0.9292 | 0.9306 | 0.9319 |
| 1.5 | 0.9332 | 0.9345 | 0.9357 | 0.9370 | 0.9382 | 0.9394 | 0.9406 | 0.9418 | 0.9429 | 0.9441 |
| 1.6 | 0.9452 | 0.9463 | 0.9474 | 0.9484 | 0.9495 | 0.9505 | 0.9515 | 0.9525 | 0.9535 | 0.9545 |
| 1.7 | 0.9554 | 0.9564 | 0.9573 | 0.9582 | 0.9591 | 0.9599 | 0.9608 | 0.9616 | 0.9625 | 0.9633 |
| 1.8 | 0.9641 | 0.9649 | 0.9656 | 0.9664 | 0.9671 | 0.9678 | 0.9686 | 0.9693 | 0.9699 | 0.9706 |
| 1.9 | 0.9713 | 0.9719 | 0.9726 | 0.9732 | 0.9738 | 0.9744 | 0.9750 | 0.9756 | 0.9761 | 0.9767 |
| 2.0 | 0.9772 | 0.9778 | 0.9783 | 0.9788 | 0.9793 | 0.9798 | 0.9803 | 0.9808 | 0.9812 | 0.9817 |

---

## How to Read the Z-Table (Step by Step)

### Example 1: Z = 1.63 (from our previous example)

**Step 1:** Split Z into two parts:
- Row value = **1.6** (the first two digits)
- Column value = **0.03** (the second decimal)

**Step 2:** Find the row for **1.6**

**Step 3:** Find the column for **0.03**

**Step 4:** Where they meet, read the number: **0.9484**

**Step 5:** Convert to percentage: 0.9484 × 100 = **94.84%**

> **Meaning:** There is a **94.84% probability** of finishing **on or before** the target date when Z = 1.63.

---

### Example 2: Z = 0.07 (from our previous example)

**Step 1:** Split Z = 0.07
- Row = **0.0**
- Column = **0.07**

**Step 2:** Find row 0.0, column 0.07

**Step 3:** Read the value: **0.5279**

**Step 4:** Convert: 0.5279 × 100 = **52.79%**

> **Meaning:** When Z = 0.07 (target almost equal to expected date), probability is about **53%**.

---

### Example 3: Z = 1.0

**Step 1:** Z = 1.00
- Row = **1.0**
- Column = **0.00**

**Step 2:** Find row 1.0, column 0.00

**Step 3:** Value = **0.8413**

**Step 4:** 84.13% probability

> **Meaning:** If your target is 1 standard deviation **above** the expected date, you have an **84% chance** of meeting it.

---

## What About Negative Z-Values?

The table above is for **positive Z-values** (target date > expected date).

For **negative Z-values** (target date < expected date), use this rule:

```
Probability for Negative Z = 1 - Probability for Positive Z
```

### Example: Z = -1.04 (from our earlier example)

**Step 1:** Ignore the negative sign. Find probability for Z = 1.04

Z = 1.04:
- Row = 1.0
- Column = 0.04
- Value = **0.8508** (about 85%)

**Step 2:** Subtract from 1

```
Probability for Z = -1.04 = 1 - 0.8508 = 0.1492
```

**Step 3:** Convert to percentage: **14.92%**

> **Meaning:** If your target is 1.04 standard deviations **below** the expected date (aggressive deadline), you only have a **15% chance** of meeting it.

---

## Quick Reference: Common Z-Values

| Z-Value | Probability (Positive Z) | Meaning |
|---------|------------------------|---------|
| 0.0 | 50% | Exactly expected date |
| 0.5 | 69% | A little buffer |
| 1.0 | 84% | Good buffer |
| 1.65 | 95% | Standard "confident" deadline |
| 2.0 | 97.7% | Very confident |
| 2.5 | 99.4% | Extremely confident |
| -1.0 | 16% | Very risky |
| -1.65 | 5% | Almost impossible |

---

## Visual Representation

```
                    Z = 0 (50% chance)
                           │
        Negative Z ←───────┼───────→ Positive Z
        (Early target)     │      (Late target)
                           │
    ────┬────┬────┬────┬───┼───┬────┬────┬────► Days
        -2   -1    0    1   2   3
        2%   16%  50%  84% 98% 99.9%
        
        Z = -1.04 (15%)     Z = 1.63 (95%)
             ↑                    ↑
        Aggressive target    Safe target
```


---

## Practice Exercise

Try these yourself:

| Z-Value | Your Answer | Check |
|---------|-------------|-------|
| Z = 0.50 | ? | 0.6915 → 69.15% |
| Z = 1.25 | ? | 0.8944 → 89.44% |
| Z = -0.80 | ? | 1 - 0.7881 = 0.2119 → 21.19% |
| Z = 1.96 | ? | 0.9750 → 97.50% |

---

## Bottom Line

**How to convert Z to probability:**

1. **Positive Z:** Look up directly in Z-table → that's your probability
2. **Negative Z:** Look up the positive version, then do `1 - that value`
3. The result is the **probability of finishing on or before** the target date

> **Key takeaway:** You don't memorize probabilities. You just learn to read the Z-table. It's a standard tool used in statistics, project management, and risk analysis.