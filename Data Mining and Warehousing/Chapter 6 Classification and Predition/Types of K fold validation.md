## Part 8: Types of K-Fold Cross-Validation

### Standard K-Fold
What we've been describing. Works well for most cases.

### Stratified K-Fold
**Problem it solves:** In classification problems with imbalanced classes (say 90% "not spam", 10% "spam"), random folds might have folds with 0% spam.

**Solution:** Force each fold to have the SAME percentage of each class as the original dataset.

**Example:** If your dataset is 90% not spam and 10% spam, then each of the 5 folds will also be 90% not spam and 10% spam.

**When to use:** Always for classification problems, especially with imbalanced classes.

### Leave-One-Out (LOO)
**K = number of samples** (if you have 100 samples, K=100)

Each experiment:
- Train on 99 samples
- Test on 1 sample
- Repeat 100 times

**Pros:** Maximum use of data, lowest bias  
**Cons:** Extremely slow, high variance, can overfit  

**When to use:** Very small datasets (less than 100 samples)

### Repeated K-Fold
Run K-Fold multiple times with different shuffles.

**Example:** 5x10-fold CV means:
- Do 10-fold cross-validation
- Repeat that entire process 5 times with different random shuffles
- Average all 50 results

**When to use:** When you need very stable performance estimates

### Time Series Split
**Problem it solves:** In time series data (stock prices, weather, sales), you cannot randomly shuffle. Future data cannot be used to predict the past.

**Solution:** Respect time order. Train on early data, test on later data.

**Example with 100 days of data:**
- Experiment 1: Train on days 1-80, Test on days 81-90
- Experiment 2: Train on days 1-85, Test on days 86-95
- Experiment 3: Train on days 1-90, Test on days 91-100

**When to use:** Any time your data has a time component (forecasting problems)

---
