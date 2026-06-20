
| **Feature**                            | **K-Means**                                                                                                        | **K-Medoids**                                                                                   |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| **What is the "center" of a cluster?** | Uses a **mean** (average) point. This "centroid" is often an imaginary point that may not be an actual data point. | Uses a **medoid**—an **actual data point** from the dataset that is the most centrally located. |
| **How does it handle noise/outliers?** | **Poorly.** A single extreme outlier can pull the average far away and mess up the whole cluster.                  | **Very well.** Since it picks a real data point, outliers have much less effect on the center.  |
| **How does it find the center?**       | Euclidian distance formula                                                                                         | manhattan distance formula                                                                      |
| **Complexity / Speed**                 | **Faster** and more efficient for large datasets.                                                                  | **Slower** because it has to check multiple candidate points to find the best medoid.           |

