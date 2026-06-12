# McNemar's Test: Comparing Two Classifiers

Now that you understand cross-validation, let's learn how to **statistically compare two classifiers** to see if one is truly better than the other.

---

## Part 1: The Problem We're Solving

### You have two classifiers and want to know: Is one really better?

**Example scenario:**
- Classifier A: Decision Tree (80% accuracy)
- Classifier B: Neural Network (82% accuracy)

**The question:** Is Neural Network truly better, or could this 2% difference just be due to random chance?

**You cannot just compare average accuracies** because:
- Different test sets might give different results
- The difference might not be statistically significant
- You need a proper statistical test

---

## Part 2: When to Use McNemar's Test

| Situation | Use McNemar's Test? |
|-----------|---------------------|
| Comparing two classifiers on the **same** test set | ✅ YES |
| Classifiers produce **binary outcomes** (correct/incorrect) | ✅ YES |
| You have **paired predictions** (both classifiers predict the same test samples) | ✅ YES |
| Comparing more than 2 classifiers | ❌ No (use other tests) |
| Comparing on different test sets | ❌ No |

**McNemar's test is specifically designed for paired nominal data from two classifiers.**

---

## Part 3: The Contingency Table (The Heart of McNemar's Test)

When you run two classifiers on the **same** test set of N samples, you can count four types of outcomes:

| | Classifier B: Correct | Classifier B: Wrong |
|---|---|---|
| **Classifier A: Correct** | **a** (both correct) | **b** (A correct, B wrong) |
| **Classifier A: Wrong** | **c** (A wrong, B correct) | **d** (both wrong) |

Where:
- **a + b + c + d = N** (total test samples)

### Important Insight:

| Cell | Meaning | Interpretation |
|------|---------|----------------|
| **a** | Both got it right | Agreement |
| **d** | Both got it wrong | Agreement |
| **b** | Only A got it right | **Disagreement (A wins)** |
| **c** | Only B got it right | **Disagreement (B wins)** |

**McNemar's test focuses ONLY on the disagreements (b and c).**

---

## Part 4: Intuition Behind the Test

### The logic:

- If both classifiers are **equally good**, then when they disagree:
  - A being right and B wrong (b) should happen about as often as
  - A being wrong and B right (c)

- So under the null hypothesis (no difference): **b ≈ c**

- If b is much larger than c, then A is better
- If c is much larger than b, then B is better

### Simple example:

Suppose on 100 test samples:
- b = 30 (A correct, B wrong)
- c = 10 (A wrong, B correct)

This suggests A is better because when they disagree, A wins 3 times as often as B.

But is this difference **statistically significant** or just random luck? McNemar's test answers this.

---

## Part 5: The McNemar's Test Formula

### Test statistic (chi-square form):

$$\chi^2 = \frac{(|b - c| - 1)^2}{b + c}$$

**Where:**
- b = count where A correct, B wrong
- c = count where A wrong, B correct
- The "-1" is called **continuity correction** (Yates' correction)

### Degrees of freedom = 1

### Decision rule:

| If χ² > 3.84 | Then p < 0.05 | Reject null hypothesis → Classifiers are **significantly different** |
| If χ² ≤ 3.84 | Then p ≥ 0.05 | Cannot reject null → **No significant difference** |

**Note:** 3.84 is the critical value for α = 0.05 (95% confidence)

---

## Part 6: Step-by-Step Example

### Scenario:
You compare two spam classifiers on 200 test emails.

### Step 1: Create the contingency table

After testing both classifiers on the same 200 emails:

| | B: Correct | B: Wrong | Row Total |
|---|---|---|---|
| **A: Correct** | a = 120 | **b = 30** | 150 |
| **A: Wrong** | **c = 10** | d = 40 | 50 |
| **Column Total** | 130 | 70 | 200 |

**Interpretation of the 200 tests:**
- Both correct: 120 emails
- Both wrong: 40 emails
- **Only A correct: 30 emails (b)**
- **Only B correct: 10 emails (c)**

### Step 2: Check the disagreements

- b = 30 (A wins when they disagree)
- c = 10 (B wins when they disagree)

A wins 3x more often. Seems promising for A.

### Step 3: Apply McNemar's formula

$$\chi^2 = \frac{(|30 - 10| - 1)^2}{30 + 10}$$

$$\chi^2 = \frac{(20 - 1)^2}{40}$$

$$\chi^2 = \frac{(19)^2}{40}$$

$$\chi^2 = \frac{361}{40}$$

$$\chi^2 = 9.025$$

### Step 4: Compare to critical value

- χ² = 9.025
- Critical value at 95% confidence = 3.84

**9.025 > 3.84** → Statistically significant

### Step 5: Conclusion

> **Reject the null hypothesis. Classifier A performs significantly better than Classifier B (p < 0.05).**

The 30 vs 10 disagreement difference is too large to be explained by random chance.

---

## Part 7: Example Where No Significant Difference Exists

### Scenario:
Same 200 emails, different results:

| | B: Correct | B: Wrong |
|---|---|---|
| **A: Correct** | a = 140 | **b = 18** |
| **A: Wrong** | **c = 15** | d = 27 |

### Step 1: Disagreements
- b = 18
- c = 15

### Step 2: Calculate

$$\chi^2 = \frac{(|18 - 15| - 1)^2}{18 + 15}$$

$$\chi^2 = \frac{(3 - 1)^2}{33}$$

$$\chi^2 = \frac{(2)^2}{33}$$

$$\chi^2 = \frac{4}{33}$$

$$\chi^2 = 0.121$$

### Step 3: Compare

0.121 < 3.84 → **Not statistically significant**

### Conclusion:

> **Cannot reject the null hypothesis. There is no significant difference between Classifier A and Classifier B.**

The small difference (18 vs 15) could easily happen by random chance.

---

## Part 8: How Cross-Validation Fits with McNemar's Test

### The standard workflow:

| Step | What you do |
|------|-------------|
| 1 | Split data using K-Fold Cross-Validation |
| 2 | For each fold, train both classifiers on the same training data |
| 3 | Test both classifiers on the SAME test fold |
| 4 | Record predictions for each test sample |
| 5 | After all folds, build ONE contingency table from ALL test predictions |
| 6 | Apply McNemar's test to this combined table |

### Important:

Each test sample appears exactly once across all folds (just like in K-Fold CV). So you can safely combine results from all folds into a single 2x2 table.

---

## Part 9: Complete Workflow Example

### Setup:
- Dataset: 500 samples
- K = 5 folds (each fold = 100 samples)
- Comparing: Logistic Regression (A) vs Random Forest (B)

### Step 1: Run 5-fold CV for both classifiers

| Fold | Test Samples | A correct? | B correct? | Contributes to |
|------|--------------|------------|------------|----------------|
| Fold 1 | Sample 1 | Yes | Yes | a |
| Fold 1 | Sample 2 | Yes | No | b |
| Fold 1 | Sample 3 | No | Yes | c |
| ... | ... | ... | ... | ... |

### Step 2: After all 5 folds, aggregate results

You have 500 total test predictions (each sample tested once).

Example final table:

| | B: Correct | B: Wrong |
|---|---|---|
| **A: Correct** | a = 350 | **b = 45** |
| **A: Wrong** | **c = 25** | d = 80 |

### Step 3: Apply McNemar's test

$$\chi^2 = \frac{(|45 - 25| - 1)^2}{45 + 25} = \frac{(20 - 1)^2}{70} = \frac{361}{70} = 5.16$$

5.16 > 3.84 → **Significant difference**

### Step 4: Conclusion

Logistic Regression (A) performs significantly better than Random Forest (B) on this dataset.

---

## Part 10: McNemar's Test vs Other Tests

| Test | What it compares | When to use |
|------|------------------|--------------|
| **McNemar's** | Two classifiers on same test set | Paired binary outcomes |
| **Paired t-test** | Two classifiers across multiple test sets | When you have K accuracy scores from CV |
| **Wilcoxon signed-rank** | Two classifiers across multiple test sets | Non-parametric alternative to t-test |
| **Friedman test** | Multiple classifiers | Comparing 3+ classifiers |

### Which one should you use?

| Situation | Recommended test |
|-----------|------------------|
| Comparing 2 classifiers, one test set | **McNemar's** |
| Comparing 2 classifiers, CV gives K accuracy scores | **Paired t-test** OR **McNemar's** (from combined predictions) |
| Many people recommend McNemar's over t-test because accuracy scores often violate t-test assumptions (normal distribution) | ✅ **McNemar's is safer** |

---

## Part 11: Assumptions and Limitations

### Assumptions of McNemar's Test:

| Assumption | Explanation |
|------------|-------------|
| **Paired data** | Same test samples for both classifiers |
| **Binary outcomes** | Correct/incorrect (not probability scores) |
| **Independence** | Each test sample is independent |
| **Marginal homogeneity** | What we're testing for |

### Limitations:

| Limitation | Implication |
|------------|-------------|
| **Requires large b + c** | If b + c < 25, test may not be reliable (use exact binomial test instead) |
| **Only binary** | Cannot use with multi-class directly (would need multiple tests) |
| **Only two classifiers** | Cannot compare 3+ at once |
| **Ignores magnitude of errors** | A wrong and B wrong are treated the same regardless of how wrong |

---

## Part 12: Small Sample Correction

If b + c < 25, use the **exact binomial version** instead of chi-square:

### Formula:
$$p = 2 \times \sum_{i=\min(b,c)}^{b+c} \binom{b+c}{i} (0.5)^{b+c}$$

Or simply use the **sign test**: If b + c is small, check if the smaller of (b, c) is ≤ critical value from binomial distribution.

**Rule of thumb:** If b + c < 25, be cautious with chi-square approximation.

---

## Part 13: Quick Reference Card

### McNemar's Test in 5 Steps:

| Step | Action |
|------|--------|
| 1 | Create 2x2 table from paired predictions |
| 2 | Identify b and c (disagreement counts) |
| 3 | Calculate χ² = (|b - c| - 1)² / (b + c) |
| 4 | Compare to 3.84 (for α = 0.05) |
| 5 | If χ² > 3.84 → classifiers are significantly different |

### Interpretation:

| Result | Meaning |
|--------|---------|
| b > c and χ² > 3.84 | Classifier A significantly better |
| c > b and χ² > 3.84 | Classifier B significantly better |
| χ² ≤ 3.84 | No significant difference |

---

## Part 14: Complete Example with Real Numbers

### Problem:
Compare Decision Tree (DT) vs Support Vector Machine (SVM) on 300 test samples from 10-fold CV.

### Step 1: Aggregate results across 10 folds

Total test predictions = 300

| | SVM: Correct | SVM: Wrong |
|---|---|---|
| **DT: Correct** | a = 200 | **b = 25** |
| **DT: Wrong** | **c = 45** | d = 30 |

### Step 2: Extract b and c

- b = 25 (DT correct, SVM wrong)
- c = 45 (DT wrong, SVM correct)

### Step 3: Calculate

$$\chi^2 = \frac{(|25 - 45| - 1)^2}{25 + 45}$$

$$\chi^2 = \frac{(20 - 1)^2}{70}$$

$$\chi^2 = \frac{361}{70} = 5.16$$

### Step 4: Compare

5.16 > 3.84 → Significant difference

### Step 5: Which is better?

c (45) > b (25) → **SVM wins more disagreements**

### Conclusion:

SVM performs significantly better than Decision Tree (χ² = 5.16, p < 0.05, McNemar's test).

---

## Part 15: Final Summary

| Concept | Key Point |
|---------|-----------|
| **Purpose** | Statistically compare two classifiers on same test data |
| **Data needed** | Paired correct/incorrect predictions |
| **Key insight** | Only disagreements matter (b and c) |
| **Null hypothesis** | b = c (no difference) |
| **Test statistic** | χ² = (|b-c|-1)²/(b+c) |
| **Critical value** | 3.84 for α = 0.05 |
| **Better classifier** | If b > c → A is better; if c > b → B is better |
| **Relationship to CV** | Use CV to get test predictions, then apply McNemar's |

---

## One Sentence Takeaway

> **McNemar's test tells you whether the difference between two classifiers is statistically significant by focusing only on the test samples where they disagree, using a chi-square test with 1 degree of freedom.**