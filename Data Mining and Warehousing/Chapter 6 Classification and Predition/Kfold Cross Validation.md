
[[why we need kfold cross validation]]

## Part 3: Introducing K-Fold Cross-Validation

### The core idea

Instead of splitting once, split many times and average the results.

**Each data point gets to be:**
- Training data (multiple times)
- Testing data (exactly once)

### How it works in plain English

1. Shuffle your data randomly
2. Divide it into K equal groups (called "folds")
3. Run K experiments:
   - In experiment 1: Use fold 1 for testing, all other folds for training
   - In experiment 2: Use fold 2 for testing, all other folds for training
   - In experiment 3: Use fold 3 for testing, all other folds for training
   - ... and so on for all K folds
4. Calculate the average performance across all K experiments

---

## Part 4: Step-by-Step Example

Let's walk through a concrete example with **100 emails** and **K = 5**.

### Step 1: Shuffle

Randomly reorder your 100 emails. This ensures that each fold gets a mix of easy and hard examples.

**Before shuffle:** Email #1, #2, #3, ..., #100  
**After shuffle:** Email #42, #17, #89, #3, ..., #56 (random order)

### Step 2: Divide into 5 folds

Each fold gets 20 emails (100 ÷ 5 = 20):

| Fold Number | Contains emails |
|-------------|-----------------|
| Fold 1 | Shuffled emails #1 to #20 |
| Fold 2 | Shuffled emails #21 to #40 |
| Fold 3 | Shuffled emails #41 to #60 |
| Fold 4 | Shuffled emails #61 to #80 |
| Fold 5 | Shuffled emails #81 to #100 |

### Step 3: Run 5 experiments

#### Experiment 1 (Fold 1 as test)

| Role | Folds used | Number of emails |
|------|------------|------------------|
| Training | Folds 2, 3, 4, 5 | 80 emails |
| Testing | Fold 1 | 20 emails |

What happens:
- Train your model on the 80 emails (folds 2-5)
- Test it on the 20 emails (fold 1)
- Record the accuracy (let's say 82%)

#### Experiment 2 (Fold 2 as test)

| Role | Folds used | Number of emails |
|------|------------|------------------|
| Training | Folds 1, 3, 4, 5 | 80 emails |
| Testing | Fold 2 | 20 emails |

What happens:
- Train a NEW model on these 80 emails (different from experiment 1)
- Test on fold 2's 20 emails
- Record the accuracy (let's say 79%)

#### Experiment 3 (Fold 3 as test)

| Role | Folds used | Number of emails |
|------|------------|------------------|
| Training | Folds 1, 2, 4, 5 | 80 emails |
| Testing | Fold 3 | 20 emails |

Record accuracy (let's say 81%)

#### Experiment 4 (Fold 4 as test)

| Role | Folds used | Number of emails |
|------|------------|------------------|
| Training | Folds 1, 2, 3, 5 | 80 emails |
| Testing | Fold 4 | 20 emails |

Record accuracy (let's say 80%)

#### Experiment 5 (Fold 5 as test)

| Role | Folds used | Number of emails |
|------|------------|------------------|
| Training | Folds 1, 2, 3, 4 | 80 emails |
| Testing | Fold 5 | 20 emails |

Record accuracy (let's say 78%)

### Step 4: Calculate the final result

Average the 5 accuracy scores:

(82 + 79 + 81 + 80 + 78) ÷ 5 = **80%**

**Final result:** Your model has an estimated accuracy of 80% on new, unseen emails.

---

## Part 5: What Just Happened?

### Every email was used for both training and testing

Let's track a single email that ended up in Fold 1:

| Experiment | Was this email used for training or testing? |
|------------|----------------------------------------------|
| Experiment 1 | **TESTING** (because fold 1 was the test set) |
| Experiment 2 | **TRAINING** (fold 1 was part of training) |
| Experiment 3 | **TRAINING** (fold 1 was part of training) |
| Experiment 4 | **TRAINING** (fold 1 was part of training) |
| Experiment 5 | **TRAINING** (fold 1 was part of training) |

This email was:
- Tested exactly once
- Trained on 4 times

**Every email gets treated exactly the same way** (just switch "fold 1" with whichever fold it belongs to).

---

## Part 6: Why K-Fold is Better

### Advantage 1: No wasted data

Every single email gets used for training (in K-1 experiments) AND for testing (in 1 experiment). No data is wasted.

### Advantage 2: More reliable estimate

Instead of one performance number, you get K numbers. The average is more reliable than any single split.

The variation between experiments (78% to 82% in our example) tells you how stable your model is. If the numbers varied wildly (say 60% to 95%), that would indicate a problem.

### Advantage 3: Less luck-dependent

With a single split, your result depends entirely on which 20 emails randomly ended up in the test set. With K-Fold, you test on ALL emails (each gets a turn), so the result is much more representative.

### Advantage 4: Detects overfitting

By comparing performance across folds, you can spot problems:

| What you see | What it means |
|--------------|---------------|
| High accuracy on all folds | Model is good ✅ |
| One fold much worse than others | That fold might have unusual data, or model is unstable |
| Training accuracy much higher than test accuracy | Model is overfitting (memorizing, not learning) |
| Training and test accuracy both low | Model is underfitting (too simple to learn patterns) |

---

## Part 7: Choosing the Value of K

| K value | What it means | Pros | Cons | Best for |
|---------|---------------|------|------|----------|
| K=3 | 3 folds (67% train, 33% test each round) | Fast, less computation | Higher bias, less reliable | Very large datasets (>100K samples) |
| K=5 | 5 folds (80% train, 20% test) | Good balance | Moderate computation | Most common default |
| K=10 | 10 folds (90% train, 10% test) | More reliable, lower bias | More computation (10x training) | Medium-sized datasets |
| K=N (LOO) | Each sample is its own fold | Maximum use of data | Extremely slow, can overfit | Very small datasets (<100 samples) |

**Rule of thumb:** Start with K=5 or K=10. These work well for most problems.

---

## [[Types of K fold validation]]


---

## Part 10: Practical Example Walkthrough

Let's say you're building a model to predict house prices. You have 500 house records.

**Step 1:** Decide on K=5 (will give you 5 experiments)

**Step 2:** Shuffle the 500 records randomly

**Step 3:** Split into 5 folds of 100 records each

**Step 4:** Run 5 experiments

| Experiment | Training (400 records) | Testing (100 records) | Result (RMSE) |
|------------|----------------------|----------------------|---------------|
| 1 | Folds 2,3,4,5 | Fold 1 | $25,000 |
| 2 | Folds 1,3,4,5 | Fold 2 | $24,500 |
| 3 | Folds 1,2,4,5 | Fold 3 | $26,000 |
| 4 | Folds 1,2,3,5 | Fold 4 | $25,500 |
| 5 | Folds 1,2,3,4 | Fold 5 | $24,800 |

**Step 5:** Calculate average and standard deviation

Average RMSE = (25000 + 24500 + 26000 + 25500 + 24800) ÷ 5 = **$25,160**

Standard deviation ≈ $600

**Interpretation:** 
- On average, your model predicts house prices within about $25,000
- The low standard deviation ($600) means performance is consistent across different data splits

**Step 6:** Now that you trust the estimate, train your final model on ALL 500 records

**Step 7:** Deploy that final model to predict prices for new houses

---

## Part 11: Summary Table

| Concept | Simple Explanation |
|---------|-------------------|
| **K-Fold CV** | Split data into K groups, test on each group once, average results |
| **Purpose** | Estimate how well your model will perform on new data |
| **Training set per fold** | K-1 folds (most of the data) |
| **Testing set per fold** | 1 fold (a small portion) |
| **Number of experiments** | K |
| **Final result** | Average of K results |
| **When to use** | Small to medium datasets, model comparison, tuning parameters |
| **When NOT to use** | Very large datasets (just use simple split), time series (use Time Series Split) |

---

## Part 12: One-Sentence Takeaway

> **K-Fold Cross-Validation builds and tests K different models, each time using a different subset of data for testing and the rest for training, then averages the results to give you a reliable estimate of real-world performance without wasting any data.**



### Correct Process:

|Iteration|Fold 1 (20 samples)|Fold 2 (20)|Fold 3 (20)|Fold 4 (20)|Fold 5 (20)|
|---|---|---|---|---|---|
|**Round 1**|**TEST** ✅|TRAIN|TRAIN|TRAIN|TRAIN|
|**Round 2**|TRAIN|**TEST** ✅|TRAIN|TRAIN|TRAIN|
|**Round 3**|TRAIN|TRAIN|**TEST** ✅|TRAIN|TRAIN|
|**Round 4**|TRAIN|TRAIN|TRAIN|**TEST** ✅|TRAIN|
|**Round 5**|TRAIN|TRAIN|TRAIN|TRAIN|**TEST** ✅|