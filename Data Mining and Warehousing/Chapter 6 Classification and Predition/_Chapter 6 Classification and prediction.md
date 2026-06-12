
## [[Introduction to Classification and Prediction]]

In **Data Mining** and **Data Warehousing**, **Classification** and **Prediction** are two major types of data analysis tasks used to extract meaningful patterns from data. They are both forms of **supervised learning**, meaning they rely on labeled historical data to build models.

---
## [[Learning (Trainning) and Testing of classificaiton]]

**Training:** Using **labeled data** in an algorithm to make the model understand the relationship between features and class labels.

**Testing:** Using **known data** (which has labels) but feeding it into the model **without the labels** to check the model's accuracy, simulating real-life use.

---
## [[ID3 Algorithm for attribute selection]]


---
## [[Bayesian classification]]
Bayesian Classification calculates: "Given these attributes (features), what is the probability that this record belongs to each possible class?"

---
## [[Laplace Smoothing]]

**Laplace smoothing ensures no probability is ever zero.**
**Laplace smoothing adds 1 to every feature count to prevent zero probabilities, allowing Naïve Bayes to handle unseen values.**

---

## [[Classification by Back Propagation]]
Inputting data, observing output, and adjusting weights until you get a satisfactory output

note: neural network 
## Your Understanding (Exactly Correct)

text

INPUT ──► [× WEIGHT] ──► [+ BIAS] ──► [ACTIVATION FUNCTION] ──► OUTPUT

That's **all** a single neuron does. Nothing more.

---
## [[Rule Based Classifier ((Decision tree rules, Rules Coverage and accuracy, effecient rule classifier) )]]
**A rule-based classifier uses IF-THEN rules (often from decision trees) to make predictions; coverage tells you how many cases a rule applies to, accuracy tells you how often it's right; and efficient rule classifiers organize rules (through ordering, trees, pruning, or indexing) to find matching rules quickly without checking them all.**

---

## [[Support Vector Machine]]

---
## [[Performance Metrics (Precision, Recall, Accuracy, F-measure]]

---
## [[Issues in Classification]]


1. Overfitting: Model memorized training data, fails on new data
2. Underfitting: Model too simple, never learned pattern
3. Imbalanced data: Model ignores rare but important class
4. High dimensions: Too many features cause sparseness
5. Noisy data: Errors in labels or values confuse model
6. Non-linear: Classes can't be separated by straight line
7. Feature scale: Large-range features dominate distance-based models
8. Multiclass: Binary models need adaptation for many classes
9. Concept drift: Patterns change over time
10. Cost sensitivity: False positive vs false negative have different costs


---
## [[Overfitting and Underfitting]]

Overfitting occurs when a model learns the **training data too well**, including its **noise, outliers, and random fluctuations**, rather than the underlying true pattern. As a result, the model becomes overly complex and performs excellently on training data but **poorly on new, unseen data** (test/validation data).
Underfitting occurs when a model is **too simple** to capture the underlying structure of the data. It fails to learn even the training data well, resulting in **high error on both training and test data**.

---
## [[Kfold Cross Validation]]

 **K-Fold Cross-Validation builds and tests K different models, each time using a different subset of data for testing and the rest for training, then averages the results to give you a reliable estimate of real-world performance without wasting any data.**

---
## [[Compairing 2 classifiers(models) Mc Nemar's test]]
