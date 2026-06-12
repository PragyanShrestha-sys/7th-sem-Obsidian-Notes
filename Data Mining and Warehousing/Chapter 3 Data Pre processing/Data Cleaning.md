**Data cleaning** (also called **data cleansing** or **scrubbing**) is the most critical step in data preprocessing. It focuses on **detecting and correcting (or removing) errors, inconsistencies, and inaccuracies** in raw data to ensure reliability before storage in a data warehouse or use in data mining.

The motto of data cleaning is: *"Bad data in, bad insights out"* — so cleaning directly impacts the quality of every downstream decision.

---

## Main Tasks in Data Cleaning

| Problem                      | Description                                         | Example                                                 | Cleaning Method                                            |
| ---------------------------- | --------------------------------------------------- | ------------------------------------------------------- | ---------------------------------------------------------- |
| **Missing values**           | Data fields that are empty, NULL, or unknown        | Phone number: `NULL`                                    | Fill with mean/median, predict value, or delete row/column |
| **Noise (errors)**           | Random or systematic errors in measured values      | Temperature: `999°C`                                    | Smooth (binning, regression), cluster, or manually correct |
| **Inconsistent data format** | Same entity represented in different formats        | `"NY"`, `"New York"`, `"new york"`                      | Standardize (e.g., all to `"New York"`)                    |
| **Duplicates**               | Identical or near-identical records for same entity | Two customer rows with same email but different address | Merge records after confirming match                       |
| **Outliers**                 | Values far outside normal range                     | Age: `200` years                                        | Cap, floor, remove, or treat separately                    |
| **Invalid values**           | Data violating domain rules                         | Birth date: `2050-01-01`                                | Set to NULL or reject record                               |

## Real-World Example

**Raw dirty data:**

| Customer_ID | Name       | City      | Age | Signup_Date |
|-------------|------------|-----------|-----|-------------|
| 101         | Ana        | NYC       | 25  | 2024-01-15  |
| 101         | A. Smith   | New York  | -5  | 15/01/2024  |
| 102         | Bob        | NULL      | 30  | 2023-13-40  |

**After cleaning:**

| Customer_ID | Name   | City       | Age | Signup_Date |
|-------------|--------|------------|-----|-------------|
| 101         | Ana    | New York   | 25  | 2024-01-15  |
| 102         | Bob    | Unknown    | 30  | NULL        |

* What happened:  
  - Duplicate `101` merged → Name & City standardized.  
  - Age `-5` → replaced with median (25).  
  - NULL city → `"Unknown"`.  
  - Invalid signup date → NULL.

---

## Bottom Line

Data cleaning is **not one-size-fits-all**. Domain knowledge is essential (e.g., missing salary might mean unemployed, not an error). A good rule: **clean enough to make data usable, not perfect to the point of bias or overfitting** — but never skip it.