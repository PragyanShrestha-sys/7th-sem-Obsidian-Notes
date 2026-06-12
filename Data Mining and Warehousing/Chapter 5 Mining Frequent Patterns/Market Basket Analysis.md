**Market basket analysis** is a data mining technique used by retailers to understand the purchase behavior of customers. It answers the question: *"What items are customers likely to buy together?"*

The classic example is the **"beer and diapers"** story (whether true or not, it illustrates the concept): a store discovered that men who bought diapers on Thursday evenings also frequently bought beer. By putting diapers and beer near each other, they increased sales of both.

[[Some Terms]]

Here’s a detailed breakdown.

---

### The Core Concept (Association Rules)

Market basket analysis works by finding **frequent patterns** (as we just discussed) and turning them into **association rules**.

- **Input:** A database of transactions (each transaction is a list of items one customer bought in a single visit).
- **Output:** Rules of the form **$X \rightarrow Y$** (If a customer buys X, they are likely to also buy Y).

**Example Rule:**
> {Bread, Butter} $\rightarrow$ {Milk}
> *Interpretation:* "Customers who buy bread and butter together also buy milk in 75% of such cases."


### Key Metrics for a Rule

Not every co-occurrence is useful. We use three main metrics to evaluate a rule $X \rightarrow Y$:

| Metric         | What it means                                                                                     | Formula (simplified)                                    | Example for {Bread} → {Milk}                                                                   |
| :------------- | :------------------------------------------------------------------------------------------------ | :------------------------------------------------------ | :--------------------------------------------------------------------------------------------- |
| **Support**    | How **common** is this itemset? <br> (Bread & Milk together)                                      | (Transactions with both X and Y) / (Total transactions) | 200/1000 = 20% <br> *20% of all baskets contain bread and milk.*                               |
| **Confidence** | How **reliable** is the rule? <br> (When X is bought, how often is Y also bought?)                | (Support of X & Y) / (Support of X)                     | 200/300 ≈ 66.7% <br> *When bread is bought, milk is bought 66.7% of the time.*                 |
| **Lift**       | How much **more likely** is Y to be bought because of X? <br> (Lift > 1 means a real association) | (Confidence of X→Y) / (Support of Y)                    | 0.667 / 0.4 = 1.67 <br> *People who buy bread are 1.67x more likely to buy milk than average.* |

> **Important:** A rule with high confidence but lift near 1 is not interesting (e.g., {Bread} → {Milk} if everyone buys milk anyway). Lift > 1 is the key to finding a real cross-selling opportunity.

---

### A Real-World Example

**Store:** Small grocery
**Transactions (simplified):**

| Transaction ID | Items Bought              |
| :------------- | :------------------------ |
| T1             | Bread, Milk, Eggs         |
| T2             | Bread, Butter, Milk       |
| T3             | Bread, Butter, Eggs       |
| T4             | Milk, Eggs                |
| T5             | Bread, Butter, Milk, Eggs |
| T6             | Bread, Milk               |

**Goal:** Find interesting rules.

From these 6 transactions:
- {Bread} appears in 5 trans → Support = 5/6 = 83%
- {Butter} appears in 3 trans → Support = 3/6 = 50%
- {Bread, Butter} appears in 3 trans → Support = 3/6 = 50%

**Rule:** {Bread} $\rightarrow$ {Butter}
- **Support** = 3/6 = **50%** (Bread & Butter together in half of all baskets)
- **Confidence** = (Support Bread+Butter) / (Support Bread) = 0.5 / 0.83 = **60%** (When bread is bought, butter is bought 60% of the time)
- **Lift** = Confidence / (Support Butter) = 0.6 / 0.5 = **1.2** (Bread buyers are 20% more likely to buy butter than the average customer – a mild positive association)

**Rule:** {Bread} $\rightarrow$ {Milk}
- Confidence = (4/6) / (5/6) = 80%
- Lift = 0.8 / (5/6 ≈ 0.833) = **0.96** (Lift < 1 → Actually, bread buyers are *slightly less* likely to buy milk than average. No positive association!)

The manager would use the Butter rule for product placement, but ignore the Milk rule.

---

### Practical Uses in Business

1.  **Product Placement (Cross-selling):**
    - Place commonly associated items near each other (e.g., chips near salsa).
    - Use "people who bought this also bought..." recommendations on e-commerce sites.

2.  **Promotions & Bundling:**
    - Offer a discount on a bundle (e.g., bread + butter + jam for $X).
    - Send targeted coupons (e.g., if someone buys a tent, send a coupon for flashlights).

3.  **Store Layout Optimization:**
    - High-association items can be placed at opposite ends of the store to encourage browsing through other aisles.
    - Essential items (milk, bread) are often placed far apart so customers pass more products.

4.  **Inventory Management:**
    - If {grill, charcoal} → {lighter fluid} has high confidence, ensure lighter fluid is always in stock during summer.

### Limitations

- **Spurious patterns:** With large data, some rules appear statistically significant by chance.
- **Doesn't imply causation:** Rule {motion sickness medicine} → {baby diapers} might simply reflect parents traveling with a baby; the medicine doesn't *cause* diaper buying.
- **Large number of rules:** For thousands of items, you can get millions of rules – must filter with support/lift thresholds.

### Summary

| | |
| :--- | :--- |
| **Goal** | Find items frequently bought together |
| **Output** | Association rules (X → Y) |
| **Key metrics** | Support (commonness), Confidence (reliability), Lift (real association) |
| **Classic example** | {Bread, Butter} → {Milk} |
| **Main use** | Cross-selling, recommendations, layout, promotions |

In short: **Market basket analysis** is the practical application of frequent pattern mining to retail transactions, using **lift** to discover meaningful product associations that boost sales.

