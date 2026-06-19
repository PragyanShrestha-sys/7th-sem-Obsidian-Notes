
## Part 1: What Are We Trying to Do?

We have a network (graph) with some nodes and some edges. But many edges are missing.

**Goal:** Predict whether a missing edge should exist, and if it should be positive or negative.

**Example:** Should Facebook recommend Alice and Bob as friends? (positive link) Or should it flag them as potential enemies? (negative link)

---
## Part 2: Two Different Questions

This is the most important distinction.

| Question               | What it means                                    | Example                                    |
| ---------------------- | ------------------------------------------------ | ------------------------------------------ |
| **Does a link exist?** | Should there be any relationship at all?         | Should Alice and Bob be connected?         |
| **What is the sign?**  | Is the relationship friendly (+) or hostile (-)? | If connected, are they friends or enemies? |


**These are separate problems.** You cannot answer sign without first knowing a link exists.

---
## Part 3: Predicting Whether a Link Exists

### The Core Idea

> *Nodes that are "close" in the network are more likely to become connected.*

### Why This Works

**Triadic closure:** If Alice and Bob share a common friend Carol, they are likely to become friends.

---

## Part 4: Predicting the Sign (Positive or Negative)

### The Core Idea

> *Once we know a link exists, balance theory tells us whether it should be positive or negative.*

### Balance Theory (Multiplication Rule)

| Path signs | Result sign | Folk saying                |
| ---------- | ----------- | -------------------------- |
| (+) × (+)  | (+)         | Friend of friend is friend |
| (+) × (-)  | (-)         | Friend of enemy is enemy   |
| (-) × (+)  | (-)         | Enemy of friend is enemy   |
| (-) × (-)  | (+)         | Enemy of enemy is friend   |

### How It Is Used

1. Find a path between A and B (usually length 2)
2. Multiply the signs along the path
3. The result is the predicted sign

### Example

```
A → C (+)
C → B (-)
(+) × (-) = (-) → predict A→B is negative (distrust)
```

---

## Part 5: The Complete Two-Step Process

| Step | Question                  | Method                                          | Output     |
| ---- | ------------------------- | ----------------------------------------------- | ---------- |
| 1    | Does a link exist?        | Common neighbors (or Jaccard, etc.) + threshold | Yes/No     |
| 2    | If yes, what is the sign? | Multiplication rule (balance theory)            | (+) or (-) |

### Complete Example

**Step 1 — Link existence:**
- A and B have 4 common friends
- Threshold = 3
- → Predict: **Link exists**

**Step 2 — Sign prediction:**
- Path: A → C (+), C → B (+)
- (+) × (+) = (+)
- → Predict: **Positive link (friendship)**

**Final prediction:** A and B should be friends.

---

## Part 6: Summary Table

| What we predict | Method | Example |
|-----------------|--------|---------|
| Does a link exist? | Common neighbors, Jaccard, Adamic-Adar, Preferential attachment, Shortest path | Score ≥ threshold → yes |
| Is the link positive or negative? | Multiplication rule (balance theory) | (+) × (-) = (-) → negative |

---

## Part 7: One-Sentence Takeaway

> *"Link existence is predicted by proximity measures like common neighbors; link sign is predicted separately by balance theory's multiplication rule — they are two different steps, not alternatives."*

---

## Quick Reference

```
Step 1 (Existence): Common neighbors, Jaccard, Adamic-Adar → "Should A and B be connected?"
Step 2 (Sign): Multiplication rule → "If connected, is it (+) or (-)?"
```