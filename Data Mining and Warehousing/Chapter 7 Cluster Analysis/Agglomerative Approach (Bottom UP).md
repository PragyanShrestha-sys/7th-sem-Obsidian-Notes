https://www.youtube.com/watch?v=N_afb0_jhjA&list=PLtusNRRQtirxX15AaS1BmJyusN236JFdk&index=27&t=379s

You have **5 students** with **one mark each** (single attribute). Let me restate your data clearly:

| Student ID | Marks |
|------------|-------|
| 1 | 10 |
| 2 | 7 |
| 3 | 28 |
| 4 | 20 |
| 5 | 35 |

Now I will explain **Hierarchical Clustering** from scratch using this data.

---

## PART 1: THE QUESTION BEFORE MAKING THE PROXIMITY MATRIX

### The Question

> **"Given my 5 students with their marks, how far apart is every pair of students from each other?"**

Since we only have one attribute (Marks), distance is simply the absolute difference between their marks.

**Formula:** Distance = |Mark₁ - Mark₂|

---

## PART 2: BUILDING THE PROXIMITY MATRIX

### Step 1: Calculate Distance for Every Pair

Let me calculate the distance between each pair of students.

| Pair | Calculation | Distance |
|------|-------------|----------|
| Student 1 (10) and Student 2 (7) | |10-7| = |3| | 3 |
| Student 1 (10) and Student 3 (28) | |10-28| = | -18| | 18 |
| Student 1 (10) and Student 4 (20) | |10-20| = | -10| | 10 |
| Student 1 (10) and Student 5 (35) | |10-35| = | -25| | 25 |
| Student 2 (7) and Student 3 (28) | |7-28| = | -21| | 21 |
| Student 2 (7) and Student 4 (20) | |7-20| = | -13| | 13 |
| Student 2 (7) and Student 5 (35) | |7-35| = | -28| | 28 |
| Student 3 (28) and Student 4 (20) | |28-20| = |8| | 8 |
| Student 3 (28) and Student 5 (35) | |28-35| = | -7| | 7 |
| Student 4 (20) and Student 5 (35) | |20-35| = | -15| | 15 |

---

### Step 2: Build the Proximity Matrix

Now arrange all these distances in a table.

**The question this matrix answers:** "For any two students, how far apart are their marks?"

| Student | 1 | 2 | 3 | 4 | 5 |
|---------|---|---|---|---|---|
| **1** | 0 | 3 | 18 | 10 | 25 |
| **2** | 3 | 0 | 21 | 13 | 28 |
| **3** | 18 | 21 | 0 | 8 | 7 |
| **4** | 10 | 13 | 8 | 0 | 15 |
| **5** | 25 | 28 | 7 | 15 | 0 |

**How to read this matrix:**
- Row 1, Column 2 = 3 → Distance between Student 1 (mark 10) and Student 2 (mark 7) is 3
- Row 3, Column 5 = 7 → Distance between Student 3 (mark 28) and Student 5 (mark 35) is 7
- Diagonal is all 0 → Distance from a student to themselves
- Matrix is symmetric → Distance 1→2 equals distance 2→1

---

## PART 3: AGGLOMERATIVE APPROACH (Bottom-Up)

### The Question at Each Step

> **"Among all current clusters, which two are closest (have the smallest distance)?"**

Then merge them.

---

### Round 1

**Start:** Each student is its own cluster: {1}, {2}, {3}, {4}, {5}

**Step 1:** Find the smallest distance in the proximity matrix.

Looking at all pairs:
- 1-2 = 3 (smallest)
- 3-5 = 7
- 3-4 = 8
- 1-4 = 10
- 4-5 = 15
- and so on...

**Smallest distance = 3** (between Student 1 and Student 2)

**Step 2:** Merge Student 1 and Student 2 into a cluster. Call it **{1,2}**

**Current clusters:** {1,2}, {3}, {4}, {5}

**Step 3:** Update the proximity matrix.

We need distances from the new cluster {1,2} to all other clusters {3}, {4}, {5}.

**For Single Linkage** (minimum distance):

| Distance | Calculation | Result |
|----------|-------------|--------|
| dist({1,2}, 3) | min(dist(1,3), dist(2,3)) = min(18, 21) | 18 |
| dist({1,2}, 4) | min(dist(1,4), dist(2,4)) = min(10, 13) | 10 |
| dist({1,2}, 5) | min(dist(1,5), dist(2,5)) = min(25, 28) | 25 |

**New proximity matrix:**

| | {1,2} | 3 | 4 | 5 |
|--|-------|---|---|---|
| **{1,2}** | 0 | 18 | 10 | 25 |
| **3** | 18 | 0 | 8 | 7 |
| **4** | 10 | 8 | 0 | 15 |
| **5** | 25 | 7 | 15 | 0 |

---

### Round 2

**Step 1:** Find smallest distance in the new matrix.

Pairs:
- 3-5 = 7 (smallest)
- 3-4 = 8
- {1,2}-4 = 10
- 4-5 = 15
- {1,2}-3 = 18
- {1,2}-5 = 25

**Smallest distance = 7** (between Student 3 and Student 5)

**Step 2:** Merge Student 3 and Student 5 into a cluster. Call it **{3,5}**

**Current clusters:** {1,2}, {3,5}, {4}

**Step 3:** Update the proximity matrix.

We need distances from {3,5} to {1,2} and to {4}.

| Distance | Calculation | Result |
|----------|-------------|--------|
| dist({3,5}, {1,2}) | min(dist(3,1), dist(3,2), dist(5,1), dist(5,2)) = min(18,21,25,28) | 18 |
| dist({3,5}, 4) | min(dist(3,4), dist(5,4)) = min(8,15) | 8 |

Also need distance from {1,2} to 4 (already have = 10)

**New proximity matrix:**

| | {1,2} | {3,5} | 4 |
|--|-------|-------|---|
| **{1,2}** | 0 | 18 | 10 |
| **{3,5}** | 18 | 0 | 8 |
| **4** | 10 | 8 | 0 |

---

### Round 3

**Step 1:** Find smallest distance in the new matrix.

Pairs:
- {3,5} to 4 = 8 (smallest)
- {1,2} to 4 = 10
- {1,2} to {3,5} = 18

**Smallest distance = 8** (between {3,5} and Student 4)

**Step 2:** Merge {3,5} and Student 4 into a cluster. Call it **{3,4,5}**

**Current clusters:** {1,2}, {3,4,5}

**Step 3:** Update the proximity matrix.

We need distance from {3,4,5} to {1,2}.

| Distance | Calculation | Result |
|----------|-------------|--------|
| dist({3,4,5}, {1,2}) | min(dist(3,1), dist(3,2), dist(4,1), dist(4,2), dist(5,1), dist(5,2)) = min(18,21,10,13,25,28) | 10 |

**New proximity matrix:**

| | {1,2} | {3,4,5} |
|--|-------|---------|
| **{1,2}** | 0 | 10 |
| **{3,4,5}** | 10 | 0 |

---

### Round 4

**Step 1:** Only two clusters left. Merge them.

**Final cluster:** {1,2,3,4,5} (all students)

---

### Summary of Merges (Agglomerative)

| Round | Merged | Distance |
|-------|--------|----------|
| 1 | Student 1 and Student 2 | 3 |
| 2 | Student 3 and Student 5 | 7 |
| 3 | Cluster {3,5} with Student 4 | 8 |
| 4 | Cluster {1,2} with Cluster {3,4,5} | 10 |

---

### How to Get Clusters from This History

**The question:** "If I want clusters where the merge distance is less than or equal to a certain threshold, how many clusters do I get?"

| If you cut at distance... | Number of clusters | Which clusters? |
|---------------------------|-------------------|-----------------|
| < 3 | 5 clusters | {1}, {2}, {3}, {4}, {5} |
| Between 3 and 7 | 4 clusters | {1,2}, {3}, {4}, {5} |
| Between 7 and 8 | 3 clusters | {1,2}, {3,5}, {4} |
| Between 8 and 10 | 2 clusters | {1,2}, {3,4,5} |
| > 10 | 1 cluster | {1,2,3,4,5} |



---

## PART 5: SUMMARY FOR YOUR EXAM

| Concept | For your data |
|---------|---------------|
| **Dataset** | 5 students with marks: 10, 7, 28, 20, 35 |
| **Proximity matrix question** | "How far apart is every pair of students by their marks?" |
| **Smallest distance** | 3 (between Student 1 and Student 2) |
| **Largest distance** | 28 (between Student 2 and Student 5) |
| **First agglomerative merge** | {1} and {2} at distance 3 |
| **First divisive split** | {1,2,4} and {3,5} at distance 28 |

---

## One Sentence Summary

> **The proximity matrix answers "how far apart is every pair of students?" and hierarchical clustering uses these distances to either repeatedly merge the closest pairs (agglomerative) or split the farthest pairs (divisive).**

---

Would you like me to also show you the calculations using **Complete Linkage** instead of Single Linkage for comparison?