Here’s a short, clear explanation of each term in the context of frequent pattern mining:

---

### 1. Itemset
A **collection of one or more items**.
- **Example:** {bread, milk, eggs}
- **k-itemset** = an itemset with *k* items (e.g., {bread, milk} is a 2-itemset).

---

### 2. Support Count (Frequency)
The **number of transactions** that contain a particular itemset.
- **Example:** If {bread, milk} appears in 4 out of 10 transactions → support count = 4.

---

### 3. Support
The **fraction** (or percentage) of transactions that contain an itemset.  
Formula:  
\[
\text{Support}(X) = \frac{\text{Support Count of } X}{\text{Total Number of Transactions}}
\]
- **Example:** If {bread, milk} appears in 4 out of 10 transactions → support = 0.4 (or 40%).

---

### 4. Frequent Itemset
An itemset whose **support is ≥ a user-defined minimum support threshold** (called *minsup*).
- **Example:** If minsup = 30% and {bread, milk} has support = 40%, then it is frequent.  
- **Purpose:** Only frequent itemsets are considered for generating association rules.

---

### 5. Closed Itemset
An itemset for which **no proper superset has the same support count**.  
- **Example:**  
  - {bread} appears in 5 transactions.  
  - {bread, milk} also appears in exactly those same 5 transactions.  
  - Then {bread} is **not closed** (because its superset {bread, milk} has identical support).  
  - {bread, milk} is closed (no superset with same support).  
- **Why use it?** Closed itemsets drastically reduce the number of patterns while preserving all information about support (unlike maximal itemsets). Most efficient mining algorithms (e.g., CLOSET, CHARM) mine closed frequent itemsets.

---

### Quick Comparison Table

| Term | Definition | Example (total 10 transactions) |
| :--- | :--- | :--- |
| **Itemset** | Set of items | {milk, eggs} |
| **Support count** | # transactions containing itemset | 4 transactions |
| **Support** | Fraction (count / total) | 4/10 = 0.4 (40%) |
| **Frequent itemset** | Support ≥ minsup (e.g., 30%) | Yes (40% ≥ 30%) |
| **Closed itemset** | No superset with same support | {milk, eggs} has count 4; {milk, eggs, bread} has count 3 → closed |

---

### Memory Trick
- **Itemset** = the *what* (set of items)
- **Support count** = the *raw number* (# transactions)
- **Support** = the *normalized number* (percentage)
- **Frequent itemset** = *common enough* (passes threshold)
- **Closed itemset** = *maximal pattern for a given support level* (no larger set is equally common)