Here is the **same numerical example** solved using a **distance matrix** approach.

---

# DATASET (15 Points)

| Point | X | Y |
|-------|---|---|
| A | 1 | 1 |
| B | 1 | 2 |
| C | 2 | 1 |
| D | 2 | 2 |
| E | 3 | 3 |
| F | 3 | 4 |
| G | 4 | 3 |
| H | 4 | 4 |
| I | 8 | 8 |
| J | 8 | 9 |
| K | 9 | 8 |
| L | 9 | 9 |
| M | 15 | 15 |
| N | 20 | 20 |
| O | 25 | 25 |

**Parameters:** ε = 2.0, MinPts = 4

---

## STEP 1: Build the Distance Matrix

**Formula:** Euclidean distance = √[(X₁-X₂)² + (Y₁-Y₂)²]

### Distance Matrix (All 15×15 distances)

| | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **A** | 0 | 1.0 | 1.0 | 1.4 | 2.8 | 3.6 | 3.6 | 4.2 | 9.9 | 10.6 | 10.6 | 11.3 | 19.8 | 26.9 | 33.9 |
| **B** | 1.0 | 0 | 1.4 | 1.0 | 2.2 | 3.0 | 3.2 | 3.6 | 9.2 | 9.9 | 10.0 | 10.6 | 19.1 | 26.2 | 33.2 |
| **C** | 1.0 | 1.4 | 0 | 1.0 | 2.2 | 3.2 | 2.8 | 3.6 | 9.2 | 10.0 | 9.9 | 10.6 | 19.1 | 26.2 | 33.2 |
| **D** | 1.4 | 1.0 | 1.0 | 0 | 1.4 | 2.2 | 2.2 | 2.8 | 8.5 | 9.2 | 9.2 | 9.9 | 18.4 | 25.5 | 32.5 |
| **E** | 2.8 | 2.2 | 2.2 | 1.4 | 0 | 1.0 | 1.0 | 1.4 | 7.1 | 7.8 | 7.8 | 8.5 | 17.0 | 24.0 | 31.1 |
| **F** | 3.6 | 3.0 | 3.2 | 2.2 | 1.0 | 0 | 1.4 | 1.0 | 6.4 | 7.1 | 7.1 | 7.8 | 16.4 | 23.4 | 30.5 |
| **G** | 3.6 | 3.2 | 2.8 | 2.2 | 1.0 | 1.4 | 0 | 1.0 | 6.4 | 7.1 | 7.1 | 7.8 | 16.4 | 23.4 | 30.5 |
| **H** | 4.2 | 3.6 | 3.6 | 2.8 | 1.4 | 1.0 | 1.0 | 0 | 5.7 | 6.4 | 6.4 | 7.1 | 15.6 | 22.6 | 29.7 |
| **I** | 9.9 | 9.2 | 9.2 | 8.5 | 7.1 | 6.4 | 6.4 | 5.7 | 0 | 1.0 | 1.0 | 1.4 | 9.9 | 17.0 | 24.0 |
| **J** | 10.6 | 9.9 | 10.0 | 9.2 | 7.8 | 7.1 | 7.1 | 6.4 | 1.0 | 0 | 1.4 | 1.0 | 9.2 | 16.4 | 23.4 |
| **K** | 10.6 | 10.0 | 9.9 | 9.2 | 7.8 | 7.1 | 7.1 | 6.4 | 1.0 | 1.4 | 0 | 1.0 | 9.2 | 16.4 | 23.4 |
| **L** | 11.3 | 10.6 | 10.6 | 9.9 | 8.5 | 7.8 | 7.8 | 7.1 | 1.4 | 1.0 | 1.0 | 0 | 8.5 | 15.6 | 22.6 |
| **M** | 19.8 | 19.1 | 19.1 | 18.4 | 17.0 | 16.4 | 16.4 | 15.6 | 9.9 | 9.2 | 9.2 | 8.5 | 0 | 7.1 | 14.1 |
| **N** | 26.9 | 26.2 | 26.2 | 25.5 | 24.0 | 23.4 | 23.4 | 22.6 | 17.0 | 16.4 | 16.4 | 15.6 | 7.1 | 0 | 7.1 |
| **O** | 33.9 | 33.2 | 33.2 | 32.5 | 31.1 | 30.5 | 30.5 | 29.7 | 24.0 | 23.4 | 23.4 | 22.6 | 14.1 | 7.1 | 0 |

---

## STEP 2: For Each Point, Count Neighbors Within ε = 2.0

Using the distance matrix, find all points with distance ≤ 2.0 (including itself):

| Point | Neighbors within ε=2.0 | Count | Core? (≥4) |
|-------|------------------------|-------|-------------|
| **A** | A(0), B(1.0), C(1.0), D(1.4) | 4 | ✅ **Core** |
| **B** | B(0), A(1.0), C(1.4), D(1.0) | 4 | ✅ **Core** |
| **C** | C(0), A(1.0), B(1.4), D(1.0) | 4 | ✅ **Core** |
| **D** | D(0), A(1.4), B(1.0), C(1.0), **E(1.4)** | 5 | ✅ **Core** |
| **E** | E(0), D(1.4), F(1.0), G(1.0), H(1.4) | 5 | ✅ **Core** |
| **F** | F(0), E(1.0), G(1.4), H(1.0) | 4 | ✅ **Core** |
| **G** | G(0), E(1.0), F(1.4), H(1.0) | 4 | ✅ **Core** |
| **H** | H(0), E(1.4), F(1.0), G(1.0) | 4 | ✅ **Core** |
| **I** | I(0), J(1.0), K(1.0), L(1.4) | 4 | ✅ **Core** |
| **J** | J(0), I(1.0), K(1.4), L(1.0) | 4 | ✅ **Core** |
| **K** | K(0), I(1.0), J(1.4), L(1.0) | 4 | ✅ **Core** |
| **L** | L(0), I(1.4), J(1.0), K(1.0) | 4 | ✅ **Core** |
| **M** | M(0) only | 1 | ❌ No |
| **N** | N(0) only | 1 | ❌ No |
| **O** | O(0) only | 1 | ❌ No |

---

## STEP 3: Identify Core Points

| Core Points | Non-Core Points |
|-------------|-----------------|
| A, B, C, D, E, F, G, H, I, J, K, L | M, N, O |

---

## STEP 4: Form Clusters by Connecting Core Points

Check which core points are within ε=2.0 of each other:

### From the distance matrix:

| Connection | Distance | Connected? |
|------------|----------|------------|
| D to E | 1.4 (≤2.0) | ✅ Yes |
| H to I | 5.7 (>2.0) | ❌ No |
| L to M | 8.5 (>2.0) | ❌ No |

**Cluster 1:** Start with A. A connects to B,C,D. D connects to E. E connects to F,G,H.  
**Result:** {A, B, C, D, E, F, G, H} are all connected.

**Cluster 2:** Start with I. I connects to J,K,L.  
**Result:** {I, J, K, L} are all connected.

**No connection between Cluster 1 and Cluster 2** (H to I = 5.7 > 2.0)

**No core points in M,N,O**

---

## STEP 5: Add Border Points

Check if any non-core point is within ε=2.0 of any core point:

| Non-core | Distance to nearest core | Within ε=2.0? |
|----------|-------------------------|---------------|
| M | to L = 8.5 | ❌ No |
| N | to M = 7.1 | ❌ No (M is not core anyway) |
| N | to L = 15.6 | ❌ No |
| O | to N = 7.1 | ❌ No |

**No border points.**

---

## STEP 6: Label Noise Points

Points not in any cluster: **M, N, O** → **NOISE**

---

## STEP 7: Final Result

| Cluster | Points |
|---------|--------|
| **Cluster 1** | A, B, C, D, E, F, G, H |
| **Cluster 2** | I, J, K, L |
| **Noise** | M, N, O |

---

## STEP 8: Summary of Why Each Point Is Classified

| Point | Count within ε | Core? | In Cluster? | Why |
|-------|----------------|-------|-------------|-----|
| A | 4 | Yes | Cluster 1 | Has 4 neighbors |
| B | 4 | Yes | Cluster 1 | Has 4 neighbors |
| C | 4 | Yes | Cluster 1 | Has 4 neighbors |
| D | 5 | Yes | Cluster 1 | Has 5 neighbors |
| E | 5 | Yes | Cluster 1 | Has 5 neighbors |
| F | 4 | Yes | Cluster 1 | Has 4 neighbors |
| G | 4 | Yes | Cluster 1 | Has 4 neighbors |
| H | 4 | Yes | Cluster 1 | Has 4 neighbors |
| I | 4 | Yes | Cluster 2 | Has 4 neighbors |
| J | 4 | Yes | Cluster 2 | Has 4 neighbors |
| K | 4 | Yes | Cluster 2 | Has 4 neighbors |
| L | 4 | Yes | Cluster 2 | Has 4 neighbors |
| M | 1 | No | Noise | Only 1 neighbor, far from cores |
| N | 1 | No | Noise | Only 1 neighbor, far from cores |
| O | 1 | No | Noise | Only 1 neighbor, far from cores |

---

## STEP 9: One Sentence Summary

> **Using the distance matrix with ε=2.0 and MinPts=4, points A-H formed Cluster 1 (connected through D-E), points I-L formed Cluster 2, and points M,N,O were isolated with fewer than 4 neighbors, making them noise.**