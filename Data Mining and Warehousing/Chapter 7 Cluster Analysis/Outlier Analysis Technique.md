
---

# PART 5: OUTLIER DETECTION METHODS

## Method 1: Statistical (Z-Score)

**For normally distributed data**

| Step | Action |
|------|--------|
| 1 | Calculate mean (μ) and standard deviation (σ) |
| 2 | For each point, calculate Z = \|x - μ\| / σ |
| 3 | If Z > 3 (or 2), point is outlier |

**Rule of thumb:**

| Z-score | Interpretation |
|---------|----------------|
| Z < 2 | Normal |
| 2 ≤ Z < 3 | Suspicious |
| Z ≥ 3 | Outlier |

**Example:** Data: [10, 12, 11, 13, 10, **50**, 12, 11]

| Step | Calculation |
|------|-------------|
| Mean | (10+12+11+13+10+50+12+11)/8 = 129/8 = 16.125 |
| Std Dev | ≈ 13.0 |
| Z for 50 | \|50-16.125\|/13 = 33.875/13 = 2.61 |
| Conclusion | Z=2.61 → Suspicious (borderline outlier) |

---

## Method 2: IQR (Interquartile Range)

**For any distribution (no normality assumption)**

| Step | Action |
|------|--------|
| 1 | Sort data |
| 2 | Find Q1 (25th percentile) and Q3 (75th percentile) |
| 3 | Calculate IQR = Q3 - Q1 |
| 4 | Lower bound = Q1 - 1.5 × IQR |
| 5 | Upper bound = Q3 + 1.5 × IQR |
| 6 | Any point outside bounds is outlier |

**Example:** Data: [10, 12, 11, 13, 10, 50, 12, 11]

| Step | Calculation |
|------|-------------|
| Sorted | [10, 10, 11, 11, 12, 12, 13, 50] |
| Q1 | (10+11)/2 = 10.5 |
| Q3 | (12+13)/2 = 12.5 |
| IQR | 12.5 - 10.5 = 2.0 |
| Lower bound | 10.5 - 1.5×2 = 10.5 - 3 = 7.5 |
| Upper bound | 12.5 + 1.5×2 = 12.5 + 3 = 15.5 |
| Outlier? | 50 > 15.5 → **Outlier** |

---

## Method 3: Distance-Based (k-Nearest Neighbor)

**A point is an outlier if it is far from its k nearest neighbors**

| Step | Action |
|------|--------|
| 1 | Choose k (e.g., k=5) |
| 2 | For each point, find distance to k-th nearest neighbor |
| 3 | Sort distances descending |
| 4 | Points with largest distances are outliers |

**Example with 2D points (ε = 2.0 from DBSCAN example):**

| Point | Distance to 4th nearest neighbor | Outlier? |
|-------|--------------------------------|----------|
| A-H | ~1.5 | No |
| I-L | ~1.5 | No |
| M | 8.5 | ✅ Yes (large distance) |
| N | 7.1 | ✅ Yes |
| O | 7.1 | ✅ Yes |

---

## Method 4: Density-Based (DBSCAN)

**Noise points in DBSCAN are outliers**

As we learned: Any point that is:
- Not a core point
- Not within ε of any core point

→ Labeled as **NOISE** (outlier)

**From DBSCAN example:**

| Points | Status |
|--------|--------|
| A-L | In clusters (not outliers) |
| M, N, O | **Noise (outliers)** |

---

## Method 5: Clustering-Based

**Small clusters or points far from cluster centers are outliers**

| Method | How it identifies outliers |
|--------|---------------------------|
| **K-Means** | Points far from their cluster centroid |
| **Hierarchical** | Points that join clusters very late (at large distances) |

---

# PART 6: COMPARISON OF DETECTION METHODS

| Method | Best for | Weakness |
|--------|----------|----------|
| **Z-Score** | Normal distribution | Fails for skewed data |
| **IQR** | Any distribution | Not sensitive to local outliers |
| **Distance-based** | Any shape data | Computationally expensive |
| **Density-based (DBSCAN)** | Irregular shapes | Needs parameter tuning |
| **Clustering-based** | When already clustering | May miss small clusters of outliers |

---

[[numerical of outlier analysis]]
