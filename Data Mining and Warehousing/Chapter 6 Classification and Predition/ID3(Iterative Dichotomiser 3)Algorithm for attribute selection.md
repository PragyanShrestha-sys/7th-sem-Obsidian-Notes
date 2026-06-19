[[simple theory explanation]]

[[Numerical Example]]

---
Here is a **simple, short, complete reference** for **ID3 as an Attribute Selection Algorithm** – ready to paste into your notes.

---
yo tala ko ramrari padheko chaina maile

## ID3 Attribute Selection – Simple Explanation

### What is Attribute Selection?
Choosing the **most useful question (attribute)** to ask first when building a decision tree.

### What ID3 Does:
> ID3 picks the attribute that **reduces uncertainty the most** = Highest **Information Gain**

---

## [[The Formula You Need]]

### 1. Entropy (How mixed is the data?)

![[Pasted image 20260619065411.png]]

```
Entropy = -p₁×log₂(p₁) - p₂×log₂(p₂)
```
- **0** = Pure (all same class) → Good
- **1** = 50-50 mixed → Bad

### 2. Information Gain (How useful is this attribute?)
```
Gain = Entropy(before split) - Weighted Entropy(after split)
```
- **Higher Gain** = Better attribute

### 3. Weighted Entropy (After split)
```
Weighted Entropy = Σ (size_of_subset / total_size) × Entropy(subset)
```

---

## Step-by-Step Algorithm

| Step | Action                                                                |
| ---- | --------------------------------------------------------------------- |
| 1    | Calculate **Entropy** of current node (before split)                  |
| 2    | For each attribute: Split data, calculate weighted entropy, then Gain |
| 3    | Select attribute with **highest Gain**                                |
| 4    | Split data using that attribute                                       |
| 5    | Repeat for each child node (using remaining attributes)               |

---

## Quick Log Values (Memorize These)

| p    | log₂(p) |
| ---- | ------- |
| 1.0  | 0       |
| 0.75 | -0.415  |
| 0.67 | -0.585  |
| 0.6  | -0.737  |
| 0.5  | -1.0    |
| 0.4  | -1.322  |
| 0.33 | -1.585  |
| 0.25 | -2.0    |

---
## Complete Numerical Example (Play Tennis)
### Starting Data:
- Total = 14 records
- Yes = 9, No = 5
- p(Yes) = 9/14 = 0.643, p(No) = 5/14 = 0.357

---

### Step 1: Root Entropy
```
Entropy(root) = -0.643×log₂(0.643) - 0.357×log₂(0.357)
              = -0.643×(-0.637) - 0.357×(-1.485)
              = 0.409 + 0.530 = 0.94
```

---

### Step 2: Evaluate Each Attribute
#### Attribute 1: Outlook

| Outlook  | Yes | No  | Total | Entropy |
| -------- | --- | --- | ----- | ------- |
| Sunny    | 2   | 3   | 5     | 0.97    |
| Overcast | 4   | 0   | 4     | 0       |
| Rain     | 3   | 2   | 5     | 0.97    |

```
Weighted Entropy = (5/14)×0.97 + (4/14)×0 + (5/14)×0.97 = 0.69

Gain(Outlook) = 0.94 - 0.69 = 0.25
```

#### Attribute 2: Temperature

| Temperature | Yes | No | Total | Entropy |
|-------------|-----|-----|-------|---------|
| Hot | 2 | 2 | 4 | 1.0 |
| Mild | 4 | 2 | 6 | 0.92 |
| Cool | 3 | 1 | 4 | 0.81 |

```
Weighted Entropy = (4/14)×1.0 + (6/14)×0.92 + (4/14)×0.81 = 0.91

Gain(Temperature) = 0.94 - 0.91 = 0.03
```

#### Attribute 3: Humidity

| Humidity | Yes | No | Total | Entropy |
|----------|-----|-----|-------|---------|
| High | 3 | 4 | 7 | 0.99 |
| Normal | 6 | 1 | 7 | 0.59 |

```
Weighted Entropy = (7/14)×0.99 + (7/14)×0.59 = 0.79

Gain(Humidity) = 0.94 - 0.79 = 0.15
```

#### Attribute 4: Wind

| Wind | Yes | No | Total | Entropy |
|------|-----|-----|-------|---------|
| Weak | 6 | 2 | 8 | 0.81 |
| Strong | 3 | 3 | 6 | 1.0 |

```
Weighted Entropy = (8/14)×0.81 + (6/14)×1.0 = 0.89

Gain(Wind) = 0.94 - 0.89 = 0.05
```

---

### Step 3: Compare Gains

| Attribute | Gain | Rank |
|-----------|------|------|
| **Outlook** | **0.25** | **1st ← SELECT** |
| Humidity | 0.15 | 2nd |
| Wind | 0.05 | 3rd |
| Temperature | 0.03 | 4th |

> **Decision:** Select **Outlook** because it has the highest Gain (0.25)

---

## What Happens Next?

After selecting Outlook:

```
                    [Outlook?]
                        │
        ┌───────────────┼───────────────┐
        │               │               │
     Sunny           Overcast           Rain
        │               │               │
    [2Y,3N]          [4Y,0N]          [3Y,2N]
        │               │               │
   Need split         Pure            Need split
                 (Leaf = Yes)
```

- **Overcast** → Pure (all Yes) → Make leaf node
- **Sunny** → Still mixed → Repeat ID3 with {Temperature, Humidity, Wind}
- **Rain** → Still mixed → Repeat ID3 with {Temperature, Humidity, Wind}

---

## Entropy Values Reference Table

| Yes | No | p(Yes) | Entropy | Meaning |
|-----|-----|--------|---------|---------|
| 4 | 0 | 1.0 | 0 | Pure |
| 3 | 1 | 0.75 | 0.81 | Mostly pure |
| 2 | 2 | 0.5 | 1.0 | 50-50 mixed |
| 2 | 3 | 0.4 | 0.97 | Mixed |
| 1 | 6 | 0.143 | 0.59 | Mostly pure |

---

## Stopping Conditions (When to Stop Splitting)

| Condition | Action |
|-----------|--------|
| All records same class | Make leaf node (output that class) |
| No attributes left | Make leaf node (output majority class) |
| Stopping criteria met (e.g., max depth) | Make leaf node |

---

## Important Notes (Confusing Points Clarified)

| Point | Explanation |
|-------|-------------|
| **Entropy = 0** | All records same class → Perfect, stop here |
| **Entropy = 1** | 50-50 split → Worst case, need to split |
| **Higher Gain = Better** | Gain = reduction in uncertainty |
| **Gain cannot be negative** | Ranges from 0 to current entropy |
| **ID3 bias** | Prefers attributes with many values (fixed by C4.5's Gain Ratio) |
| **log₂(0)** | Treat as 0 (by convention) |

---

## One-Line Summary

> **ID3 selects the attribute with highest Information Gain = Entropy(before) − Weighted Entropy(after). Entropy measures impurity (0 = pure, 1 = 50-50 mixed).**