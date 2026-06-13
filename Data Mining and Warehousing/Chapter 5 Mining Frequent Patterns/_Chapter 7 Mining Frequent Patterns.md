In data mining, **mining frequent patterns** means discovering sets of items (or events, subsequences, or structures) that appear together in a dataset with a frequency greater than or equal to a user-specified threshold (called _minimum support_).

Here’s a breakdown:

- **Patterns** – combinations of items (e.g., {bread, milk, eggs} in a grocery transaction).
- **Frequent** – the pattern occurs in at least a minimum number (or percentage) of records in the dataset.
- **Goal** – find all patterns whose occurrence frequency meets the threshold.
---
## [[Market Basket Analysis]]

**Market basket analysis** is a data mining technique used by retailers to understand the purchase behavior of customers. It answers the question: _"What items are customers likely to buy together?"_

The classic example is the **"beer and diapers"** story (whether true or not, it illustrates the concept): a store discovered that men who bought diapers on Thursday evenings also frequently bought beer. By putting diapers and beer near each other, they increased sales of both.

---

### [[Types of Association Rules]]

Association rules in data mining are =="if-then" statements that uncover hidden relationships, correlations, or co-occurrences among variables in large datasets==. They seek to answer the question: _"If a customer buys item X, what is the likelihood they will also buy item Y?"_ 

| Think of it as…                         | Rule Type          |
| :-------------------------------------- | :----------------- |
| "Buying this OR that item"              | Boolean            |
| "Age, price, temperature ranges"        | Quantitative       |
| "Only purchase behavior matters"        | Single-dimensional |
| "Age AND income AND purchase"           | Multidimensional   |
| "Sometimes general, sometimes specific" | Multilevel         |

---
### [[Finding Frequent Itemset]]

1. Aprori algorithm 
2. FP Growth


