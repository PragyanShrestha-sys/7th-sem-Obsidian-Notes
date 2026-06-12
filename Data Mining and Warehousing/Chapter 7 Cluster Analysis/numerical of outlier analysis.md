# PART 8: NUMERICAL WORKED EXAMPLE

## Dataset: Employee Salaries

| Employee | Salary ($) |
|----------|------------|
| 1 | 45,000 |
| 2 | 48,000 |
| 3 | 47,000 |
| 4 | 46,000 |
| 5 | 49,000 |
| 6 | 47,500 |
| 7 | 46,500 |
| 8 | 48,500 |
| 9 | 44,000 |
| 10 | **200,000** |

---

## Method 1: Z-Score

| Step | Calculation |
|------|-------------|
| Mean | (sum of all except outlier)/9 = 421,500/9 = 46,833 |
| Standard deviation | ≈ 1,700 |
| Z for 200,000 | (200,000 - 46,833)/1,700 = 153,167/1,700 = 90 |
| Conclusion | Z >> 3 → **Strong outlier** |

---

## Method 2: IQR

| Step | Calculation |
|------|-------------|
| Sorted | 44k,45k,46k,46.5k,47k,47.5k,48k,48.5k,49k,200k |
| Q1 | 46,000 |
| Q3 | 48,500 |
| IQR | 48,500 - 46,000 = 2,500 |
| Upper bound | 48,500 + 1.5×2,500 = 48,500 + 3,750 = 52,250 |
| 200,000 > 52,250 | → **Outlier** |

---

## Decision

| Question | Answer |
|----------|--------|
| Is it an error? | Probably not (CEO salary?) |
| Is it genuine? | Possibly (CEO vs regular employees) |
| Action | **Keep but analyze separately** or use robust methods |

---

# PART 9: OUTLIERS IN CLUSTERING (Review)

## How Different Algorithms Handle Outliers

| Algorithm | Treatment of outliers |
|-----------|----------------------|
| **K-Means** | Forces into some cluster, distorts centroid |
| **Hierarchical** | Forces into some cluster, distorts merges |
| **DBSCAN** | Labels as NOISE (best handling) ✅ |

## Why DBSCAN is Best for Outliers

| Feature | Benefit |
|---------|---------|
| Noise label | Outliers identified explicitly |
| Does not distort clusters | Outliers not forced into clusters |
| No need to pre-remove | Handles organically |

---
