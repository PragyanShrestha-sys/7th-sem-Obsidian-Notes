Great question. You already understand **data cube computation** (pre-calculating all GROUP BY answers). Now **cube materialization** answers a different question:

> "After I compute these answers, which ones do I actually *save* to disk?"

---
2. Computational & Materialization Types

These refer to how much of the data cube (all possible combinations of dimensions and calculations) is actually pre-calculated and stored:

- **Full Cubes:** Computes and stores all possible aggregate combinations for all dimensions. It offers the fastest querying speed, but requires massive storage space. 

- **Iceberg Cubes:** Only computes and stores aggregations that meet a specific minimum threshold (such as a minimum sales or volume). This significantly reduces the memory and storage required for large, sparse datasets. 

- **Closed Cubes:** Only stores "closed cells" where an aggregation's value is different from all of its descendant cells. This cuts down redundant data while retaining all necessary analytical insights. 

- **Cube Shells:** Only pre-computes combinations for a small, predefined set of dimensions (e.g., up to three at a time). Less common dimension combinations are computed on the fly as needed.

----
## Cube Materialization = The Decision of What to Store

**Materialization** just means "make permanent" — saving the computed results to disk so they persist and can be queried later.

Think of it like this:

| Term                | Analogy                                                           |
| :------------------ | :---------------------------------------------------------------- |
| **Computation**     | Cooking the food                                                  |
| **Materialization** | Deciding which dishes to put in the fridge vs which to throw away |

You *computed* every possible GROUP BY result. But storing *all* of them might be impossible (too much disk space). So you must choose.

---

## The Three Materialization Strategies

### 1. No Materialization (Compute Nothing)

| Aspect                 | Explanation                                      |
| :--------------------- | :----------------------------------------------- |
| **What you store**     | Only the raw base data                           |
| **What you save**      | Nothing pre-calculated                           |
| **When query arrives** | Compute the GROUP BY from scratch using raw data |
| **Pros**               | Saves disk space                                 |
| **Cons**               | Queries are very slow                            |

This is like having ingredients but never pre-cooking anything. Every meal starts from zero.

### 2. Full Materialization (Compute Everything, Save Everything)

| Aspect                 | Explanation                                                         |
| :--------------------- | :------------------------------------------------------------------ |
| **What you store**     | Every single cuboid (every possible GROUP BY result)                |
| **What you save**      | [[The base cuboid + all 2D cuboids + all 1D cuboids + apex cuboid]] |
| **When query arrives** | Just look up the pre-calculated answer instantly                    |
| **Pros**               | Extremely fast queries                                              |
| **Cons**               | Massive disk space (exponential growth with dimensions)             |

This is like cooking every possible dish and putting it all in the fridge. Queries are instant, but your fridge overflows quickly.

### 3. Partial Materialization (The Sweet Spot — Most Common)

| Aspect                 | Explanation                                                                       |
| :--------------------- | :-------------------------------------------------------------------------------- |
| **What you store**     | Only *some* of the cuboids                                                        |
| **What you save**      | A strategic subset (e.g., only the most useful ones)                              |
| **When query arrives** | If answer is stored → instant lookup. If not → compute from nearest stored cuboid |
| **Pros**               | Balance between speed and storage                                                 |
| **Cons**               | Some queries may be slightly slower (but not as slow as full recompute)           |

This is like cooking the most popular dishes ahead of time. For less common orders, you cook quickly from pre-chopped ingredients.

---

## Simple Example: 3 Dimensions (Product, City, Time)

| Materialization | What Gets Stored                                                                                           |
| :-------------- | :--------------------------------------------------------------------------------------------------------- |
| **No**          | Nothing pre-calculated. Only raw data.                                                                     |
| **Full**        | All 8 cuboids (base, all 2-D, all 1-D, apex)                                                               |
| **Partial**     | Maybe only 3 cuboids: (Product, City), (City, Time), and Apex. The rest are computed on-demand from these. |

---

## Popular Partial Materialization Methods

| Method | Simple Explanation |
|:---|:---|
| **Iceberg Cube** | Only store cells that meet a minimum threshold (e.g., only store GROUP BY results where total sales > $1000). The rest are too small to matter. |
| **Shell Cube** | Pre-compute for only a few dimensions. Add more dimensions on-the-fly when needed. |
| **Greedy Selection** | Analyze which queries users ask most often, and only materialize those cuboids. |

---

## One Sentence Summary

> **Cube materialization = The strategy deciding which pre-calculated GROUP BY answers to permanently save (all, none, or some), balancing query speed against disk space.**

| | Computation | Materialization |
|:---|:---|:---|
| **What is it?** | The act of calculating | The decision of saving |
| **Question it answers** | "How do I get the numbers?" | "Which numbers do I keep?" |
| **Analogy** | Cooking | Refrigerating |

---
---

## [[Types of Cubes ]]
## Quick Overview

| Method           | Core Idea                                        | Storage Size          | Query Speed             |
| ---------------- | ------------------------------------------------ | --------------------- | ----------------------- |
| **Full Cube**    | Store everything                                 | Massive (2^n cuboids) | Fastest                 |
| **Iceberg Cube** | Store only "big enough" cells                    | Much smaller          | Fast (for stored cells) |
| **Closed Cube**  | Store only unique, non-redundant cells           | Smaller than full     | Fast                    |
| **Shell Cube**   | Store only a few dimensions, compute rest on fly | Smallest              | Moderate to Fast        |