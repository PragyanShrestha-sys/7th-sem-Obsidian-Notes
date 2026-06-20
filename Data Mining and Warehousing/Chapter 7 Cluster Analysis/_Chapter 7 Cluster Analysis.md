## [[Introduction]]
**Cluster analysis is exactly that: a grouping process that places similar data points together.**

To add a little more precision to your concise definition:
- **"Similar"** is measured mathematically (e.g., by distance - points that are close together are considered similar).
- **The key distinction** from everyday grouping is that clustering is **automatic and unsupervised** the algorithm discovers the groups on its own, without being told what to look for or given any labels.
So in short:
> **Clustering = Automatic grouping of unlabeled data based on similarity**

---
## [[Types of Data in Cluster analysis]]

## Overview: The Five Main Data Types

|#|Data Type|Nature|Example Attributes|
|---|---|---|---|
|1|**Interval-Scaled**|Continuous numeric|Age, Income, Temperature|
|2|**Binary**|Two states (0/1)|Yes/No, Male/Female, Has/Doesn't Have|
|3|**Nominal**|Unordered categories|Color, Country, Product Type|
|4|**Ordinal**|Ordered categories|Rank, Rating, Size (S/M/L)|
|5|**Mixed**|Combination of above|Most real-world datasets|

---
## [[Similarity and Dissimilarity Between objects]]


>so what were basically doing is quantifing or doing mathematical calulations for numercal data representing the similarities between the different objects by using their attributes from database

> _"Quantifying or doing mathematical calculations for numerical data representing the similarities between different objects by using their attributes from database"_

**This is precisely what cluster analysis does.**

|Your words|What it means technically|
|---|---|
|"Quantifying"|Converting "alikeness" into a number (0 to 1 or 0 to ∞)|
|"Mathematical calculations"|Distance formulas (Euclidean, Manhattan, Jaccard, etc.)|
|"Using attributes"|Each attribute becomes a dimension in the calculation|
|"From database"|The rows/records/objects in your data warehouse|

---

## [[Clustering Techniques]]

There are three main types of Clustering Techiques 
1. Partitioning
2. Hierarchial 
3. Density Based

---
## [[Outlier Analysis]]
