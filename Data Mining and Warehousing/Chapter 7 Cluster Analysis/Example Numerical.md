![[Pasted image 20260511162344.png]]

Thank you for sharing the full dataset. Let me restate it clearly:

## Dataset

| Object | X | Y | Z |
|--------|---|---|---|
| 1 | 1 | 6 | -1 |
| 2 | 3 | 7 | 0 |
| 3 | 3 | 5 | -2 |
| 4 | 4 | 8 | -1 |
| 5 | 5 | 8 | 0 |

We will solve this using **both approaches**:

1. **Agglomerative** (Bottom-Up) - Single Linkage
2. **Divisive (DIANA)** (Top-Down)

---

# PART 1: THE QUESTION BEFORE MAKING THE PROXIMITY MATRIX

**The question:** *"Given my 5 objects with three attributes (X, Y, Z), how far apart is every pair of objects from each other?"*

We will use **Euclidean distance** formula:

> Distance = √[(X₁ - X₂)² + (Y₁ - Y₂)² + (Z₁ - Z₂)²]

---

# PART 2: BUILDING THE PROXIMITY MATRIX

## Step 1: Calculate Distance for Every Pair

### Pair (1,2)
| Difference | Square |
|------------|--------|
| X: 1-3 = -2 | 4 |
| Y: 6-7 = -1 | 1 |
| Z: -1-0 = -1 | 1 |
| Sum of squares | 6 |
| Distance = √6 | **2.45** |

### Pair (1,3)
| Difference | Square |
|------------|--------|
| X: 1-3 = -2 | 4 |
| Y: 6-5 = 1 | 1 |
| Z: -1-(-2) = 1 | 1 |
| Sum of squares | 6 |
| Distance = √6 | **2.45** |

### Pair (1,4)
| Difference | Square |
|------------|--------|
| X: 1-4 = -3 | 9 |
| Y: 6-8 = -2 | 4 |
| Z: -1-(-1) = 0 | 0 |
| Sum of squares | 13 |
| Distance = √13 | **3.61** |

### Pair (1,5)
| Difference | Square |
|------------|--------|
| X: 1-5 = -4 | 16 |
| Y: 6-8 = -2 | 4 |
| Z: -1-0 = -1 | 1 |
| Sum of squares | 21 |
| Distance = √21 | **4.58** |

### Pair (2,3)
| Difference | Square |
|------------|--------|
| X: 3-3 = 0 | 0 |
| Y: 7-5 = 2 | 4 |
| Z: 0-(-2) = 2 | 4 |
| Sum of squares | 8 |
| Distance = √8 | **2.83** |

### Pair (2,4)
| Difference | Square |
|------------|--------|
| X: 3-4 = -1 | 1 |
| Y: 7-8 = -1 | 1 |
| Z: 0-(-1) = 1 | 1 |
| Sum of squares | 3 |
| Distance = √3 | **1.73** |

### Pair (2,5)
| Difference | Square |
|------------|--------|
| X: 3-5 = -2 | 4 |
| Y: 7-8 = -1 | 1 |
| Z: 0-0 = 0 | 0 |
| Sum of squares | 5 |
| Distance = √5 | **2.24** |

### Pair (3,4)
| Difference | Square |
|------------|--------|
| X: 3-4 = -1 | 1 |
| Y: 5-8 = -3 | 9 |
| Z: -2-(-1) = -1 | 1 |
| Sum of squares | 11 |
| Distance = √11 | **3.32** |

### Pair (3,5)
| Difference | Square |
|------------|--------|
| X: 3-5 = -2 | 4 |
| Y: 5-8 = -3 | 9 |
| Z: -2-0 = -2 | 4 |
| Sum of squares | 17 |
| Distance = √17 | **4.12** |

### Pair (4,5)
| Difference | Square |
|------------|--------|
| X: 4-5 = -1 | 1 |
| Y: 8-8 = 0 | 0 |
| Z: -1-0 = -1 | 1 |
| Sum of squares | 2 |
| Distance = √2 | **1.41** |

---

## Step 2: The Proximity Matrix

**The question this matrix answers:** *"For any two objects, how far apart are they in 3D space?"*

| Object | 1 | 2 | 3 | 4 | 5 |
|--------|---|---|---|---|---|
| **1** | 0 | 2.45 | 2.45 | 3.61 | 4.58 |
| **2** | 2.45 | 0 | 2.83 | 1.73 | 2.24 |
| **3** | 2.45 | 2.83 | 0 | 3.32 | 4.12 |
| **4** | 3.61 | 1.73 | 3.32 | 0 | 1.41 |
| **5** | 4.58 | 2.24 | 4.12 | 1.41 | 0 |

---

# PART 3: AGGLOMERATIVE (BOTTOM-UP) - SINGLE LINKAGE

**The question at each step:** *"Among all current clusters, which two are closest (have the smallest distance)?"*

---

### Round 1

**Start:** {1}, {2}, {3}, {4}, {5}

**Step 1:** Find smallest distance in proximity matrix.

Looking at all pairs:
- 4-5 = 1.41 (smallest)
- 2-4 = 1.73
- 2-5 = 2.24
- 1-2 = 2.45
- 1-3 = 2.45
- 2-3 = 2.83
- and so on...

**Smallest distance = 1.41** (between Object 4 and Object 5)

**Step 2:** Merge 4 and 5 into cluster **{4,5}**

**Current clusters:** {1}, {2}, {3}, {4,5}

**Step 3:** Update proximity matrix (Single Linkage = minimum distance)

| Distance | Calculation | Result |
|----------|-------------|--------|
| dist({4,5}, 1) | min(dist(4,1), dist(5,1)) = min(3.61, 4.58) | 3.61 |
| dist({4,5}, 2) | min(dist(4,2), dist(5,2)) = min(1.73, 2.24) | 1.73 |
| dist({4,5}, 3) | min(dist(4,3), dist(5,3)) = min(3.32, 4.12) | 3.32 |

Also keep existing distances:
- 1-2 = 2.45
- 1-3 = 2.45
- 2-3 = 2.83

**New proximity matrix:**

| | {1} | {2} | {3} | {4,5} |
|--|-----|-----|-----|-------|
| **{1}** | 0 | 2.45 | 2.45 | 3.61 |
| **{2}** | 2.45 | 0 | 2.83 | 1.73 |
| **{3}** | 2.45 | 2.83 | 0 | 3.32 |
| **{4,5}** | 3.61 | 1.73 | 3.32 | 0 |

---

### Round 2

**Step 1:** Find smallest distance.

Pairs:
- {2} to {4,5} = 1.73 (smallest)
- {1} to {2} = 2.45
- {1} to {3} = 2.45
- {2} to {3} = 2.83
- {3} to {4,5} = 3.32
- {1} to {4,5} = 3.61

**Smallest distance = 1.73** (between Object 2 and cluster {4,5})

**Step 2:** Merge Object 2 with {4,5} into cluster **{2,4,5}**

**Current clusters:** {1}, {3}, {2,4,5}

**Step 3:** Update proximity matrix.

| Distance | Calculation | Result |
|----------|-------------|--------|
| dist({2,4,5}, 1) | min(dist(2,1), dist(4,1), dist(5,1)) = min(2.45, 3.61, 4.58) | 2.45 |
| dist({2,4,5}, 3) | min(dist(2,3), dist(4,3), dist(5,3)) = min(2.83, 3.32, 4.12) | 2.83 |

Also keep distance between 1 and 3 = 2.45

**New proximity matrix:**

| | {1} | {3} | {2,4,5} |
|--|-----|-----|---------|
| **{1}** | 0 | 2.45 | 2.45 |
| **{3}** | 2.45 | 0 | 2.83 |
| **{2,4,5}** | 2.45 | 2.83 | 0 |

---

### Round 3

**Step 1:** Find smallest distance.

Pairs:
- {1} to {3} = 2.45
- {1} to {2,4,5} = 2.45
- {3} to {2,4,5} = 2.83

**Smallest distance = 2.45** (tie between {1} to {3} and {1} to {2,4,5})

Let us merge {1} and {3} (arbitrary choice, both are same distance)

**Step 2:** Merge Object 1 and Object 3 into cluster **{1,3}**

**Current clusters:** {1,3}, {2,4,5}

**Step 3:** Update proximity matrix.

| Distance | Calculation | Result |
|----------|-------------|--------|
| dist({1,3}, {2,4,5}) | min(dist(1,2), dist(1,4), dist(1,5), dist(3,2), dist(3,4), dist(3,5)) = min(2.45, 3.61, 4.58, 2.83, 3.32, 4.12) | 2.45 |

**New proximity matrix:**

| | {1,3} | {2,4,5} |
|--|-------|---------|
| **{1,3}** | 0 | 2.45 |
| **{2,4,5}** | 2.45 | 0 |

---

### Round 4

Only two clusters left. Merge them.

**Final cluster:** {1,2,3,4,5}

---

### Summary of Merges (Agglomerative)

| Round | Merged | Distance |
|-------|--------|----------|
| 1 | Object 4 and Object 5 | 1.41 |
| 2 | Object 2 with {4,5} | 1.73 |
| 3 | Object 1 and Object 3 | 2.45 |
| 4 | {1,3} with {2,4,5} | 2.45 |

---

### How to Get Clusters from This History

| Cut at distance... | Number of clusters | Which clusters? |
|--------------------|-------------------|-----------------|
| < 1.41 | 5 clusters | {1}, {2}, {3}, {4}, {5} |
| Between 1.41 and 1.73 | 4 clusters | {1}, {2}, {3}, {4,5} |
| Between 1.73 and 2.45 | 3 clusters | {1}, {3}, {2,4,5} |
| Between 2.45 and 2.45 | 2 clusters | {1,3}, {2,4,5} |
| > 2.45 | 1 cluster | All together |

---

# PART 4: DIVISIVE (DIANA ALGORITHM) - TOP-DOWN

**The question at each step:** *"Among all objects in the current cluster, which two are farthest apart (have the largest distance)?"*

Then split using those as seeds.

---

### Round 1

**Start:** One cluster containing all objects: {1,2,3,4,5}

**Step 1:** Find the two objects farthest apart in the original proximity matrix.

Looking at all pairs from original matrix:
- 1-5 = 4.58
- 3-5 = 4.12
- 1-4 = 3.61
- 3-4 = 3.32
- 2-3 = 2.83
- ... and so on

**Largest distance = 4.58** (between Object 1 and Object 5)

**Step 2:** Use Object 1 and Object 5 as "seeds" to split.

**Step 3:** Assign every other object to the closer seed.

| Object | Distance to Seed 1 | Distance to Seed 5 | Closer to |
|--------|-------------------|-------------------|-----------|
| 2 | 2.45 | 2.24 | Seed 5 |
| 3 | 2.45 | 4.12 | Seed 1 |
| 4 | 3.61 | 1.41 | Seed 5 |

**Result of split:**
- Cluster A: {1, 3}
- Cluster B: {5, 2, 4} or {2,4,5}

---

### Round 2

Now split each cluster separately.

#### First, split cluster {1,3}:

Only two objects. They split automatically.

**Split result:** {1} and {3}

#### Second, split cluster {2,4,5}:

**Step 1:** Find farthest pair in {2,4,5}.

Look at distances from original matrix:
- 2-4 = 1.73
- 2-5 = 2.24
- 4-5 = 1.41

**Largest distance = 2.24** (between Object 2 and Object 5)

**Step 2:** Use Object 2 and Object 5 as seeds.

**Step 3:** Assign remaining object (Object 4) to closer seed.

| Object | Distance to Seed 2 | Distance to Seed 5 | Closer to |
|--------|-------------------|-------------------|-----------|
| 4 | 1.73 | 1.41 | Seed 5 |

**Split result:** {2} and {5,4} or {4,5}

---

### Round 3

Now split {4,5}:

Only two objects. Split into {4} and {5}.

---

### Summary of Splits (DIANA)

| Round | Cluster split into | Split distance |
|-------|-------------------|----------------|
| 1 | {1,2,3,4,5} → {1,3} and {2,4,5} | 4.58 (1 to 5) |
| 2a | {1,3} → {1} and {3} | 2.45 (1 to 3) |
| 2b | {2,4,5} → {2} and {4,5} | 2.24 (2 to 5) |
| 3 | {4,5} → {4} and {5} | 1.41 (4 to 5) |

---

# PART 5: COMPARISON OF BOTH APPROACHES

| Step | Agglomerative (Bottom-Up) | Divisive / DIANA (Top-Down) |
|------|--------------------------|---------------------------|
| **Step 1** | Merge 4 and 5 (1.41) | Split {1,3} and {2,4,5} (4.58) |
| **Step 2** | Merge 2 with {4,5} (1.73) | Split {1,3} → {1},{3} (2.45) |
| **Step 3** | Merge 1 and 3 (2.45) | Split {2,4,5} → {2},{4,5} (2.24) |
| **Step 4** | Merge {1,3} with {2,4,5} (2.45) | Split {4,5} → {4},{5} (1.41) |

**Notice:** The distances used are the same in both approaches, just in reverse order.

---

# PART 6: FINAL ANSWER

## Agglomerative Result (Single Linkage)

| Merge Order | Action | Distance |
|-------------|--------|----------|
| 1 | Merge 4 and 5 | 1.41 |
| 2 | Merge 2 with (4,5) | 1.73 |
| 3 | Merge 1 and 3 | 2.45 |
| 4 | Merge (1,3) with (2,4,5) | 2.45 |

**To get 2 clusters:** {1,3} and {2,4,5}

---

## Divisive (DIANA) Result

| Split Order | Action | Distance |
|-------------|--------|----------|
| 1 | Split into {1,3} and {2,4,5} | 4.58 |
| 2 | Split {1,3} into {1} and {3} | 2.45 |
| 3 | Split {2,4,5} into {2} and {4,5} | 2.24 |
| 4 | Split {4,5} into {4} and {5} | 1.41 |

**To get 2 clusters:** {1,3} and {2,4,5} (same as agglomerative)

---

## One Sentence Summary

> **Agglomerative clustering merged {4,5} first (smallest distance 1.41), then {2} with {4,5} (1.73), then {1} with {3} (2.45); DIANA did the opposite, first splitting {1,3} from {2,4,5} (largest distance 4.58), then splitting further until each object was alone.**