
**Data cube computation = Pre-calculating all possible GROUP BY queries and storing the answers for instant lookup later.**

## What is Data Cube Computation? (In One Paragraph)

**It's just pre-calculating all the "GROUP BY" answers ahead of time.**

Imagine you have a sales table. Instead of waiting for someone to ask "What are total sales by city?" and then calculating it, you just calculate *every possible question* in advance and store the answers.

- Every possible combination of dimensions (Product, City, Time) gets its SUM calculated and saved.
- When a user asks a question, you just look up the pre-calculated answer instantly.

That's it. Computation = pre-calculating all the answers.

---

## Base Cuboid vs Apex Cuboid (The Two Extremes)

Think of a cuboid as one specific "GROUP BY" result. The cube has many cuboids (different groupings). The **base** and **apex** are the two ends of the spectrum.

|                     | **Base Cuboid**                                             | **Apex Cuboid**                    |
| :------------------ | :---------------------------------------------------------- | :--------------------------------- |
| **Also called**     | The base cell                                               | The apex cell (or "all" cell)      |
| **Level of detail** | Most detailed                                               | Most summarized                    |
| **What it shows**   | One number for *every single combination* of all dimensions | One single number for *everything* |
| **GROUP BY**        | `GROUP BY Product, City, Date`                              | No GROUP BY (just `SUM(Sales)`)    |
| **Number of rows**  | Many rows (one for each unique combination)                 | Exactly 1 row                      |

### Simple Example

Raw sales data (just 4 transactions):

| Product | City | Date | Sales |
|:---|:---|:---|:---|
| Laptop | NYC | Jan | $100 |
| Mouse | LA | Jan | $20 |
| Laptop | LA | Feb | $80 |
| Mouse | NYC | Feb | $30 |

**Base Cuboid** (most detailed — every combination):

| Product | City | Date | Total Sales |
|:---|:---|:---|:---|
| Laptop | NYC | Jan | $100 |
| Mouse | LA | Jan | $20 |
| Laptop | LA | Feb | $80 |
| Mouse | NYC | Feb | $30 |

**Apex Cuboid** (most summarized — just one number):

| Total Sales |
|:---|
| $230 |

### The Visual Analogy

Imagine a pyramid:

```
                    🧊 APEX CUBOID
                   (1 number: total sales)
                  /     |     \
                🧊       🧊       🧊
           (by City) (by Product) (by Date)
           /    |      |    |      |    \
         🧊     🧊     🧊     🧊     🧊     🧊
      (by City    (by City   (by Product  (by Product
       & Date)     & Product)  & Date)     & Date)
           \      |      |      |      /
                 🧊 BASE CUBOID
           (most detailed: by City, Product, Date)
```

- **Top (Apex)** = 1 cell. Most abstract.
- **Bottom (Base)** = Many cells. Most concrete.
- **Everything in between** = Other cuboids (like "by City only" or "by Product and Date").

### One Sentence Summary

| Term | Simple Meaning |
|:---|:---|
| **Data Cube Computation** | Pre-calculating every possible GROUP BY answer from your data |
| **Base Cuboid** | The most detailed level (every combination of all dimensions) |
| **Apex Cuboid** | The most summarized level (just the grand total, one number) |

