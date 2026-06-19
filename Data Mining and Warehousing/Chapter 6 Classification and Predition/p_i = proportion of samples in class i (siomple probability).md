Great question! Let me break down **\( p_i \)** in plain English:

---

## What is \( p_i \)?

**\( p_i \)** = the **fraction** (or percentage) of samples in your dataset that belong to class **i**.

---

## Simple Example

Let's say you have **10 fruits** in your dataset:

- 6 Apples
- 4 Bananas

Then:

- \( p_{apple} = 6/10 = 0.6 \) (60%)
- \( p_{banana} = 4/10 = 0.4 \) (40%)

---

## Another Example (3 classes)

You have **100 animals**:

- 50 Dogs → \( p_1 = 0.5 \)
- 30 Cats → \( p_2 = 0.3 \)
- 20 Birds → \( p_3 = 0.2 \)

Notice: **All \( p_i \) values add up to 1.0** (0.5 + 0.3 + 0.2 = 1.0)

---

## Why do we need it?

In the Entropy formula:

```
H(S) = - sum(p_i * log2(p_i))
```

We use \( p_i \) to measure **how mixed** the classes are:

- If all samples are the same class (e.g., 10/10 Apples) → \( p = 1.0 \) → Entropy = 0 (pure, no uncertainty)
- If samples are perfectly split (e.g., 5 Apples, 5 Bananas) → \( p = 0.5 \) each → Entropy = 1.0 (maximum uncertainty)

---

## In short

**\( p_i \)** = **"Out of all my data, what fraction belongs to class i?"**

Just count the samples in class i, divide by total samples. That's it!