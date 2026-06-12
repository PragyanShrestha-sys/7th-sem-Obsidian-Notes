In the context of **Data Mining and Data Warehousing**, **Cluster Analysis** (or simply **Clustering**) is a technique used to group a set of objects (like data points, rows, or records) so that:

- **Objects within the same group (cluster)** are **highly similar** to each other (high intra-cluster similarity).
- **Objects in different groups** are **highly dissimilar** (low inter-cluster similarity).

It is a primary method of **unsupervised learning** — meaning there is no predefined class label or target variable. The algorithm discovers hidden patterns or natural groupings in the data without prior knowledge of what those groups should be.

---

## Key Concepts in Cluster Analysis

| Term | Meaning |
|------|---------|
| **Similarity/Distance** | Clusters are formed based on a distance metric (e.g., Euclidean, Manhattan). Smaller distance = more similar. |
| **Centroid** | The center point of a cluster (often the mean of its points). |
| **Outlier** | A data point that does not fit well into any cluster. |
| **Feature space** | The multi-dimensional space defined by the attributes (columns) of the dataset. |

---

## Common Applications in Data Warehousing & Mining

| Domain | Example |
|--------|---------|
| **Customer segmentation** | Grouping customers by purchasing behavior to target marketing campaigns. |
| **Document clustering** | Organizing news articles or research papers by topic. |
| **Anomaly detection** | Finding fraud or network intrusions (outliers don't belong to clusters). |
| **Image segmentation** | Grouping pixels in an image for object recognition. |
| **Biological data** | Grouping genes with similar expression patterns. |

