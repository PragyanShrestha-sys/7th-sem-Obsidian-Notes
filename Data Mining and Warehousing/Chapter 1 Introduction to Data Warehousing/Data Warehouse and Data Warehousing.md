A data warehouse is a centralized repository that consolidates structured historical data from multiple sources to support business intelligence, analytics, and decision-making. Data warehousing is the overall process of gathering, cleaning, transforming, and managing this data (often using [[ELT]]) to provide a single, consistent version of the truth


---

## Data Warehouse vs. Data Warehousing

| Term | Definition |
|------|-------------|
| **Data Warehouse** | The *destination* – a centralized repository storing structured, historical data from many sources. |
| **Data Warehousing** | The *process* – the overall activity of gathering, cleaning, transforming, and managing data to load into the warehouse. |

---

## Why Use a Data Warehouse?

| Problem it solves                          | How                                 |
| ------------------------------------------ | ----------------------------------- |
| Data scattered across multiple systems     | Consolidates into one place         |
| Inconsistent data (different formats, IDs) | Standardizes and cleans             |
| Slow queries on operational databases      | Optimized for fast read/aggregation |
| No historical tracking                     | Stores snapshots over time          |

---

## One Sentence Summary

> **Data warehousing** is the process of extracting, cleaning, and loading data; the **data warehouse** is the final centralized repository that powers business intelligence and analytics.

---
---


### [[Features and Characterstics of Data Warehousing]]

## Data Warehouse – Key Traits

- **Subject-oriented** – Organized around key business areas (sales, customers, products)
- **Integrated** – Data from multiple sources is standardized (e.g., same date formats, currencies)
- **Time-variant** – Stores **historical data** over long periods (not just current state)
- **Non-volatile** – Data is **not** frequently changed or deleted (read-optimized)

---
Note on OLTP and OLAP


- **OLTP** = **T**ransactions → **T**oday's business (think: _T_iny, _T_ime-sensitive)

- **OLAP** = **A**nalytics → **A**nalyze history (think: _A_ggregate, _A_udience insights)

## One Sentence Summary

> **OLTP** handles thousands of small, fast transactions to _run_ the business; **OLAP** handles massive, complex queries to _understand_ the business.\

---

