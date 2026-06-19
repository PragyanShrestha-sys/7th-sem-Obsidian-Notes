Absolutely! Let me walk you through a **complete numerical example** of ID3 as an attribute selection algorithm, step-by-step, with all calculations shown clearly.

---

## Problem: Predict Whether to Play Tennis

We have 14 days of historical data. We want to predict **Play?** (Yes/No) based on 4 attributes:

| Day | Outlook  | Temperature | Humidity | Wind   | Play? |
| --- | -------- | ----------- | -------- | ------ | ----- |
| 1   | Sunny    | Hot         | High     | Weak   | No    |
| 2   | Sunny    | Hot         | High     | Strong | No    |
| 3   | Overcast | Hot         | High     | Weak   | Yes   |
| 4   | Rain     | Mild        | High     | Weak   | Yes   |
| 5   | Rain     | Cool        | Normal   | Weak   | Yes   |
| 6   | Rain     | Cool        | Normal   | Strong | No    |
| 7   | Overcast | Cool        | Normal   | Strong | Yes   |
| 8   | Sunny    | Mild        | High     | Weak   | No    |
| 9   | Sunny    | Cool        | Normal   | Weak   | Yes   |
| 10  | Rain     | Mild        | Normal   | Weak   | Yes   |
| 11  | Sunny    | Mild        | Normal   | Strong | Yes   |
| 12  | Overcast | Mild        | High     | Strong | Yes   |
| 13  | Overcast | Hot         | Normal   | Weak   | Yes   |
| 14  | Rain     | Mild        | High     | Strong | No    |

**Goal:** Which attribute (Outlook, Temperature, Humidity, or Wind) should be selected FIRST to split the data?

---
## Step 1: Understand What We Start With (Root Node)
Before any split, at the root node, we have all 14 records.
### Count the classes:

| Class      | Count  |
| ---------- | ------ |
| Play = Yes | 9      |
| Play = No  | 5      |
| **Total**  | **14** |

### Calculate proportions:

| Proportion | Formula | Value |
| ---------- | ------- | ----- |
| p(Yes)     | 9/14    | 0.643 |
| p(No)      | 5/14    | 0.357 |

---
## Step 2: Calculate Current Entropy (How "Mixed" We Are)
### Formula:

```
Entropy(S) = -p(Yes) × log₂(p(Yes)) - p(No) × log₂(p(No))
```

### Step-by-step calculation:

**First term:** -p(Yes) × log₂(p(Yes))

```
p(Yes) = 0.643
log₂(0.643) = ? 
```

To calculate log₂(0.643):
- 0.643 is between 2⁻¹ = 0.5 and 2⁰ = 1
- log₂(0.643) = -0.637 (approximately)

```
- p(Yes) × log₂(p(Yes)) = -0.643 × (-0.637) = 0.409
```

**Second term:** -p(No) × log₂(p(No))

```
p(No) = 0.357
log₂(0.357) = -1.485 (approximately)
-0.357 × (-1.485) = 0.530
```

**Add them:**

```
Entropy(root) = 0.409 + 0.530 = 0.94
```

| Current State | Entropy |
|---------------|---------|
| Root Node | **0.94 bits** |

> **Interpretation:** 0.94 is close to 1, meaning the data is highly mixed (almost 50-50). We need to split.

---

## Step 3: Evaluate Each Candidate Attribute

We will calculate **Information Gain** for each attribute using:

![[Pasted image 20260619135435.png]]
Where:
- S = Current set (14 records)
- A = Attribute being tested
- S_v = Subset where attribute A = value v

---
## Attribute 1: Outlook

### Step 3.1: Split data by Outlook

Outlook has 3 possible values: Sunny, Overcast, Rain

| Outlook  | Records         | Yes | No  | Total |
| -------- | --------------- | --- | --- | ----- |
| Sunny    | Day 1,2,8,9,11  | 2   | 3   | 5     |
| Overcast | Day 3,7,12,13   | 4   | 0   | 4     |
| Rain     | Day 4,5,6,10,14 | 3   | 2   | 5     |

### Step 3.2: Calculate entropy for each subset

#### Sunny subset (2 Yes, 3 No):

```
Total = 5
p(Yes) = 2/5 = 0.4
p(No) = 3/5 = 0.6

Entropy(Sunny) = -0.4 × log₂(0.4) - 0.6 × log₂(0.6)
               = -0.4 × (-1.322) - 0.6 × (-0.737)
               = 0.529 + 0.442
               = 0.97
```

#### Overcast subset (4 Yes, 0 No):

```
Total = 4
p(Yes) = 4/4 = 1.0
p(No) = 0/4 = 0

Entropy(Overcast) = -1.0 × log₂(1.0) - 0 × log₂(0)
                  = -1.0 × 0 - 0
                  = 0
```

> **Note:** log₂(1) = 0, and by convention, 0 × log₂(0) = 0

#### Rain subset (3 Yes, 2 No):

```
Total = 5
p(Yes) = 3/5 = 0.6
p(No) = 2/5 = 0.4

Entropy(Rain) = -0.6 × log₂(0.6) - 0.4 × log₂(0.4)
              = -0.6 × (-0.737) - 0.4 × (-1.322)
              = 0.442 + 0.529
              = 0.97
```

### Step 3.3: Calculate weighted average entropy after split

```
Weighted Entropy = (5/14)×0.97 + (4/14)×0 + (5/14)×0.97
                 = (0.357 × 0.97) + (0.286 × 0) + (0.357 × 0.97)
                 = 0.346 + 0 + 0.346
                 = 0.69
```

### Step 3.4: Calculate Information Gain

```
Gain(Outlook) = Entropy(root) - Weighted Entropy
              = 0.94 - 0.69
              = 0.25
```

| Attribute   | Gain     |
| ----------- | -------- |
| **Outlook** | **0.25** |

---

## Attribute 2: Temperature

### Step 3.1: Split data by Temperature

Temperature has 3 values: Hot, Mild, Cool

| Temperature | Records | Yes | No | Total |
|-------------|---------|-----|-----|-------|
| Hot | Day 1,2,3,13 | 2 | 2 | 4 |
| Mild | Day 4,8,10,11,12,14 | 4 | 2 | 6 |
| Cool | Day 5,6,7,9 | 3 | 1 | 4 |

### Step 3.2: Calculate entropy for each subset

#### Hot subset (2 Yes, 2 No):

```
p(Yes) = 2/4 = 0.5
p(No) = 2/4 = 0.5

Entropy(Hot) = -0.5 × log₂(0.5) - 0.5 × log₂(0.5)
             = -0.5 × (-1) - 0.5 × (-1)
             = 0.5 + 0.5
             = 1.0
```

#### Mild subset (4 Yes, 2 No):

```
p(Yes) = 4/6 = 0.667
p(No) = 2/6 = 0.333

log₂(0.667) = -0.585
log₂(0.333) = -1.585

Entropy(Mild) = -0.667 × (-0.585) - 0.333 × (-1.585)
              = 0.390 + 0.528
              = 0.92
```

#### Cool subset (3 Yes, 1 No):

```
p(Yes) = 3/4 = 0.75
p(No) = 1/4 = 0.25

log₂(0.75) = -0.415
log₂(0.25) = -2.0

Entropy(Cool) = -0.75 × (-0.415) - 0.25 × (-2.0)
              = 0.311 + 0.5
              = 0.81
```

### Step 3.3: Calculate weighted average entropy

```
Weighted Entropy = (4/14)×1.0 + (6/14)×0.92 + (4/14)×0.81
                 = (0.286 × 1.0) + (0.429 × 0.92) + (0.286 × 0.81)
                 = 0.286 + 0.395 + 0.232
                 = 0.91
```

### Step 3.4: Calculate Information Gain

```
Gain(Temperature) = 0.94 - 0.91 = 0.03
```

| Attribute   | Gain     |
| ----------- | -------- |
| Temperature | **0.03** |

---

## Attribute 3: Humidity

### Step 3.1: Split data by Humidity

Humidity has 2 values: High, Normal

| Humidity | Records | Yes | No | Total |
|----------|---------|-----|-----|-------|
| High | Day 1,2,3,4,8,12,14 | 3 | 4 | 7 |
| Normal | Day 5,6,7,9,10,11,13 | 6 | 1 | 7 |

### Step 3.2: Calculate entropy for each subset

#### High subset (3 Yes, 4 No):

```
Total = 7
p(Yes) = 3/7 = 0.429
p(No) = 4/7 = 0.571

log₂(0.429) = -1.221
log₂(0.571) = -0.807

Entropy(High) = -0.429 × (-1.221) - 0.571 × (-0.807)
              = 0.524 + 0.461
              = 0.99
```

#### Normal subset (6 Yes, 1 No):

```
Total = 7
p(Yes) = 6/7 = 0.857
p(No) = 1/7 = 0.143

log₂(0.857) = -0.222
log₂(0.143) = -2.807

Entropy(Normal) = -0.857 × (-0.222) - 0.143 × (-2.807)
                = 0.190 + 0.401
                = 0.59
```

### Step 3.3: Calculate weighted average entropy

```
Weighted Entropy = (7/14)×0.99 + (7/14)×0.59
                 = (0.5 × 0.99) + (0.5 × 0.59)
                 = 0.495 + 0.295
                 = 0.79
```

### Step 3.4: Calculate Information Gain

```
Gain(Humidity) = 0.94 - 0.79 = 0.15
```

| Attribute | Gain     |
| --------- | -------- |
| Humidity  | **0.15** |

---

## Attribute 4: Wind

### Step 3.1: Split data by Wind

Wind has 2 values: Weak, Strong

| Wind   | Records               | Yes | No  | Total |
| ------ | --------------------- | --- | --- | ----- |
| Weak   | Day 1,3,4,5,8,9,10,13 | 6   | 2   | 8     |
| Strong | Day 2,6,7,11,12,14    | 3   | 3   | 6     |

### Step 3.2: Calculate entropy for each subset

#### Weak subset (6 Yes, 2 No):

```
Total = 8
p(Yes) = 6/8 = 0.75
p(No) = 2/8 = 0.25

log₂(0.75) = -0.415
log₂(0.25) = -2.0

Entropy(Weak) = -0.75 × (-0.415) - 0.25 × (-2.0)
              = 0.311 + 0.5
              = 0.81
```

#### Strong subset (3 Yes, 3 No):

```
Total = 6
p(Yes) = 3/6 = 0.5
p(No) = 3/6 = 0.5

Entropy(Strong) = -0.5 × (-1) - 0.5 × (-1)
                = 0.5 + 0.5
                = 1.0
```

### Step 3.3: Calculate weighted average entropy

```
Weighted Entropy = (8/14)×0.81 + (6/14)×1.0
                 = (0.571 × 0.81) + (0.429 × 1.0)
                 = 0.463 + 0.429
                 = 0.89
```

### Step 3.4: Calculate Information Gain

```
Gain(Wind) = 0.94 - 0.89 = 0.05
```

| Attribute | Gain |
|-----------|------|
| Wind | **0.05** |

---

## Step 4: Compare All Gains and Select the Best

| Attribute   | Information Gain | Rank               |
| ----------- | ---------------- | ------------------ |
| **Outlook** | **0.25**         | **1st ← SELECTED** |
| Humidity    | 0.15             | 2nd                |
| Wind        | 0.05             | 3rd                |
| Temperature | 0.03             | 4th                |


### Selection Decision:

```
        Outlook has the HIGHEST Information Gain (0.25)
                              │
                              ▼
                    "Select Outlook as the
                     first splitting attribute"
```

---

## Step 5: What Happens After Selection?

Once we select **Outlook**, we split the data into 3 branches:

```
                    [Outlook?]
                        │
        ┌───────────────┼───────────────┐
        │               │               │
     Sunny           Overcast           Rain
        │               │               │
    [2 Yes,         [4 Yes,          [3 Yes,
     3 No]           0 No]            2 No]
        │               │               │
    Need to           Pure           Need to
    split further    (Leaf = Yes)   split further
```

### For the Sunny branch (2 Yes, 3 No):
We repeat the SAME process with the remaining attributes {Temperature, Humidity, Wind}

| Attribute   | Gain (in Sunny branch) |
| ----------- | ---------------------- |
| Humidity    | 0.97                   |
| Temperature | 0.57                   |
| Wind        | 0.02                   |

**Select Humidity** next for the Sunny branch.

### For the Rain branch (3 Yes, 2 No):

We repeat the SAME process with remaining attributes

| Attribute | Gain (in Rain branch) |
|-----------|-----------------------|
| Wind | 0.02 |
| Humidity | 0.01 |
| Temperature | 0.00 |

**Select Wind** next for the Rain branch.

---

## Step 6: Final Decision Tree

```
                    [Outlook?]
                        │
        ┌───────────────┼───────────────┐
        │               │               │
     Sunny           Overcast           Rain
        │               │               │
    [Humidity?]         Yes           [Wind?]
        │                               │
    ┌───┴───┐                       ┌───┴───┐
    │       │                       │       │
  High    Normal                   Weak    Strong
    │       │                       │       │
   No      Yes                      Yes     No
```

---

## Summary Table of All Calculations

| Attribute | Step | Calculation | Result |
|-----------|------|-------------|--------|
| **Base Entropy** | Root | -0.643×log₂(0.643) - 0.357×log₂(0.357) | **0.94** |
| Outlook | Weighted avg | (5/14)×0.97 + (4/14)×0 + (5/14)×0.97 | 0.69 |
| Outlook | Gain | 0.94 - 0.69 | **0.25** |
| Temperature | Weighted avg | (4/14)×1.0 + (6/14)×0.92 + (4/14)×0.81 | 0.91 |
| Temperature | Gain | 0.94 - 0.91 | **0.03** |
| Humidity | Weighted avg | (7/14)×0.99 + (7/14)×0.59 | 0.79 |
| Humidity | Gain | 0.94 - 0.79 | **0.15** |
| Wind | Weighted avg | (8/14)×0.81 + (6/14)×1.0 | 0.89 |
| Wind | Gain | 0.94 - 0.89 | **0.05** |

---

## Final Answer

> **ID3 selects Outlook as the first splitting attribute because it has the highest Information Gain (0.25), meaning it reduces uncertainty the most.**

	The numerical values show that after splitting by Outlook, the weighted entropy drops from 0.94 to 0.69 (a reduction of 0.25), while other attributes give much smaller reductions (0.15, 0.05, 0.03).