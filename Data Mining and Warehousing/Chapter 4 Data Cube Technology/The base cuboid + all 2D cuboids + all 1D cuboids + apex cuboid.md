Excellent question. You already understand **base** (most detailed) and **apex** (most summarized). Now let me fill in the middle: **1-D** and **2-D cuboids**.

The "D" stands for **number of dimensions** you group by.

## The Simple Pattern

| Cuboid Type | Number of Dimensions in GROUP BY | Example GROUP BY |
|:---|:---|:---|
| **Base** | All dimensions (3-D) | `GROUP BY Product, City, Date` |
| **2-D** | Any 2 dimensions | `GROUP BY Product, City` |
| **1-D** | Any 1 dimension | `GROUP BY Product` |
| **Apex** | 0 dimensions | `SELECT SUM(Sales)` (no GROUP BY) |

Think of it as **how many grouping columns** you use.

---

## Concrete Example: 3 Dimensions (Product, City, Date)

Let me show you every cuboid with actual numbers.

### Raw Data (4 transactions)

| Product | City | Date | Sales |
|:---|:---|:---|:---|
| Laptop | NYC | Jan | $100 |
| Mouse | LA | Jan | $20 |
| Laptop | LA | Feb | $80 |
| Mouse | NYC | Feb | $30 |

---

### BASE CUBOID (3-D)
Group by **all 3 dimensions** → most detailed

| Product | City | Date | Total Sales |
|:---|:---|:---|:---|
| Laptop | NYC | Jan | $100 |
| Mouse | LA | Jan | $20 |
| Laptop | LA | Feb | $80 |
| Mouse | NYC | Feb | $30 |

---

### 2-D CUBOIDS (Group by any 2 dimensions)

There are 3 possible 2-D cuboids (choose 2 out of 3 dimensions).

**Cuboid 1: GROUP BY Product, City**

| Product | City | Total Sales |
|:---|:---|:---|
| Laptop | NYC | $100 |
| Mouse | LA | $20 |
| Laptop | LA | $80 |
| Mouse | NYC | $30 |

**Cuboid 2: GROUP BY Product, Date**

| Product | Date | Total Sales |
|:---|:---|:---|
| Laptop | Jan | $100 |
| Mouse | Jan | $20 |
| Laptop | Feb | $80 |
| Mouse | Feb | $30 |

**Cuboid 3: GROUP BY City, Date**

| City | Date | Total Sales |
|:---|:---|:---|
| NYC | Jan | $100 |
| LA | Jan | $20 |
| LA | Feb | $80 |
| NYC | Feb | $30 |

---

### 1-D CUBOIDS (Group by any 1 dimension)

There are 3 possible 1-D cuboids.

**Cuboid 4: GROUP BY Product**

| Product | Total Sales |
|:---|:---|
| Laptop | $180 ($100 + $80) |
| Mouse | $50 ($20 + $30) |

**Cuboid 5: GROUP BY City**

| City | Total Sales |
|:---|:---|
| NYC | $130 ($100 + $30) |
| LA | $100 ($20 + $80) |

**Cuboid 6: GROUP BY Date**

| Date | Total Sales |
|:---|:---|
| Jan | $120 ($100 + $20) |
| Feb | $110 ($80 + $30) |

---

### APEX CUBOID (0-D)
No GROUP BY → just one grand total

| Total Sales |
|:---|
| $230 |

---

## Visual Summary

```
                    APEX (0-D)
                   Total = $230
                        |
        ┌───────────────┼───────────────┐
        |               |               |
    1-D by          1-D by           1-D by
    Product          City             Date
    ($180,$50)      ($130,$100)      ($120,$110)
        |               |               |
    ┌───┼───┐       ┌───┼───┐       ┌───┼───┐
    |   |   |       |   |   |       |   |   |
  2-D by   2-D by  2-D by   2-D by  2-D by   2-D by
  Prod,City Prod,Date City,Date Prod,Date City,Date Prod,City
        |               |               |
        └───────────────┼───────────────┘
                        |
                    BASE (3-D)
            (Laptop,NYC,Jan)=$100
            (Mouse,LA,Jan)=$20
            (Laptop,LA,Feb)=$80
            (Mouse,NYC,Feb)=$30
```

---

## The Pattern for Any Number of Dimensions

| Cuboid Type | Number of GROUP BY columns | For 3 Dimensions, How Many? |
|:---|:---|:---|
| Base | All n dimensions (n-D) | 1 cuboid (3-D) |
| (n-1)-D | n-1 dimensions | 3 cuboids (2-D) |
| ... | ... | ... |
| 1-D | 1 dimension | 3 cuboids |
| Apex | 0 dimensions | 1 cuboid |

**Total cuboids = 2^n** (for n=3, that's 8 cuboids)

---

## One Sentence Summary

| Term | Meaning |
|:---|:---|
| **Base (3-D)** | Group by everything → most detailed |
| **2-D** | Group by any 2 dimensions |
| **1-D** | Group by any 1 dimension |
| **Apex (0-D)** | Group by nothing → just grand total |


---
NOTE: 

**You are absolutely correct to question this!** This is a very common point of confusion.

**Total Sales is NOT a dimension. It IS a [[measure]]**
what about a [[fact]]?
