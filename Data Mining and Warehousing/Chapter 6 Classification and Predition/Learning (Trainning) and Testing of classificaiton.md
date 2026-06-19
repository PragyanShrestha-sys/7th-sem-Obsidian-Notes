In the context of **classification** (and supervised learning in general), the process of building and evaluating a model is divided into two distinct and sequential phases: **Learning (Training)** and **Testing**. These phases ensure that the model not only learns from past data but also generalizes well to new, unseen data.

## 1. Learning (Training) Phase

The **learning phase** is where the classification algorithm builds the model. The input is a pre-labeled dataset called the **training set**.

### Steps in the Learning Phase:

1.  **Prepare the Training Data:**
    - A set of records (instances) is provided.
    - Each record has multiple **attributes (features)** and a special attribute called the **class label** (e.g., "Spam" or "Not Spam").
    - *Example for email filtering:*
        - Features: `[word_freq_free, word_freq_viagra, contains_link, time_sent]`
        - Class Label: `[Spam]` or `[Not Spam]`

2.  **Algorithm Execution:**
    - A classification algorithm (e.g., Decision Tree, SVM, k-NN) analyzes the training data.
    - It identifies patterns, relationships, and rules that map the input features to the class label.
    - For instance, a Decision Tree might learn the rule: `IF contains_link = Yes AND word_freq_free > 0.05 THEN Class = Spam`.

3.  **Model Creation:**
    - The output of the learning phase is a **classifier model** (a mathematical function, a set of rules, or a structure like a tree).
    - This model encapsulates all the patterns learned from the training data.

### Key Requirement for Training Data:
- The class labels must be **correct and reliable** (often provided by human experts or historical records).
- The training set should be **representative** of the real-world data the model will encounter later.

---

## 2. Testing (Evaluation) Phase

The **testing phase** determines how well the learned model will perform on **new, unseen data**. It uses a separate dataset called the **test set**.

### Steps in the Testing Phase:

1.  **Prepare the Test Data:**
    - A separate set of records is used, **never seen by the model** during training.
    - Like the training set, the test set also contains the true class labels, but the model is **not allowed to see them** until after it makes predictions.
    - Crucially, test data must have the same feature structure but is **not used** in building the model.

2.  **Apply the Model:**
    - The trained classifier model is fed the test records **without** their actual class labels.
    - The model predicts a class label for each test record using the patterns it learned.

3.  **Compare Predictions to Truth:**
    - After the model makes predictions, the true class labels are revealed.
    - The predictions are compared to the true labels to see how many were correct.

### Example:

| Test Record | True Class | Model Prediction | Correct? |
|-------------|------------|------------------|-----------|
| Email A | Spam | Spam | ✅ Yes |
| Email B | Not Spam | Spam | ❌ No |
| Email C | Not Spam | Not Spam | ✅ Yes |

- **Accuracy** = (Number of correct predictions) / (Total test records) = 2/3 = 66.7%

---

## Why Split Data into Training and Testing?

Using the **same data** for both learning and testing is a fatal mistake (called **overfitting**). Here's why:

| Scenario                                 | What Happens                                                                             | Problem                                               |
| ---------------------------------------- | ---------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| **Train on all data, test on same data** | Model simply memorizes the training examples (like learning answers to an exam by rote). | Fails on new, unseen data (poor generalization).      |
| **Separate training & test sets**        | Model learns general patterns from training, then is tested on unseen data.              | Gives a realistic estimate of real-world performance. |

> **Analogy:**  
> - **Training** = Studying for an exam using a textbook (learning concepts).  
> - **Testing** = Taking the final exam with new questions (applying concepts).  
> - If the exam questions are identical to the textbook, you've learned nothing—just memorized.

---

## Common Data Splitting Strategies

To ensure both phases are valid, the original labeled dataset is usually split as follows:

| Split Strategy | Description |
|----------------|-------------|
| **Holdout Method** | Randomly split data into two sets: e.g., 70% Training, 30% Testing. Simple and common. |
| **k-Fold Cross-Validation** | Split data into k equal parts (folds). Train on k-1 folds, test on the remaining one; repeat k times. More robust for small datasets. |
| **Stratified Sampling** | Ensures each split has the same percentage of each class label (important for imbalanced data). |

---

## Visual Summary

```text
                    Entire Labeled Dataset
                           │
            ┌──────────────┴──────────────┐
            │                             │
      Training Set (70%)             Test Set (30%)
            │                             │
            ▼                             │
      +------------------+                 │
      │   LEARNING PHASE │                 │
      │  (Model learns   │                 │
      │   patterns)      │                 │
      +------------------+                 │
            │                             │
            ▼                             │
      +------------------+                 │
      │   TRAINED MODEL  │                 │
      +------------------+                 │
            │                             │
            └──────────────┬──────────────┘
                           │
                           ▼
                  +------------------+
                  │   TESTING PHASE  │
                  │ (Model predicts  │
                  │  on unseen data) │
                  +------------------+
                           │
                           ▼
                  +------------------+
                  │ Compare Predict- │
                  │ ions vs True     │
                  │ Labels → Metrics │
                  +------------------+
```

![[Pasted image 20260505124435.png]]

---

## [[Evaluation Metrics from Testing]]


---

## Summary

| Phase | Purpose | Input | Output |
|-------|---------|-------|--------|
| **Learning (Training)** | Build model by learning patterns from labeled data | Training set (features + known classes) | Trained classifier model |
| **Testing (Evaluation)** | Estimate real-world performance on unseen data | Test set (features only, then compare predictions to hidden true classes) | Performance metrics (accuracy, precision, recall, etc.) |

> **Key principle:** Never test on the data you trained on. Always keep training and testing data strictly separate to ensure your classification model truly *learns* and does not simply *memorize*.

---
## [[Classification by decision tree induction]]
