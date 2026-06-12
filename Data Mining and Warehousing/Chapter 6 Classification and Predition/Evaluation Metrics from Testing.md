After testing, we measure performance using metrics derived from the **confusion matrix**:

| Metric                   | Formula                             | Interpretation                                  |
| ------------------------ | ----------------------------------- | ----------------------------------------------- |
| **Accuracy**             | (TP+TN) / Total                     | Overall correctness                             |
| **Precision**            | TP / (TP+FP)                        | When model predicts "Yes", how often it's right |
| **Recall (Sensitivity)** | TP / (TP+FN)                        | Of all actual "Yes", how many were caught       |
| **F1-Score**             | Harmonic mean of precision & recall | Balance between precision and recall            |

*(TP=True Positive, TN=True Negative, FP=False Positive, FN=False Negative)*