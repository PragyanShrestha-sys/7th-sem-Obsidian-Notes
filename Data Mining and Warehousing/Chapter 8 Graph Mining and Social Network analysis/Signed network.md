Here's a **complete, detailed explanation** of Signed Networks, covering both major theories and their conflict.

---

## Part 1: What Is a Signed Network? (Refresher)

> **A signed network is a graph where each edge has a positive (+) or negative (-) sign representing the type of relationship between two nodes.**

| Sign | Meaning |
|------|---------|
| **+** | Friendship, trust, alliance, like, support |
| **-** | Enmity, distrust, opposition, dislike, conflict |

**Example:**
```
Alice (+) Bob  (friends)
Alice (-) Carol (enemies)
Bob (?) Carol  (unknown)
```

---
## [[Theory of Structural Balance]]
## [[Theory of Status]]

---
## Part 4: The Conflict Between Balance and Status

### The Core Disagreement

| Aspect | Balance Theory | Status Theory |
|--------|----------------|---------------|
| **Focus** | Undirected triangles | Directed edges |
| **Key principle** | Consistency (even negatives) | Hierarchy (status flow) |
| **What drives sign** | Psychological comfort | Social rank |
| **Predicts** | Friend/enemy patterns | Deference/rivalry patterns |

### The Famous Conflict: The "Friend of My Enemy"

Consider this directed configuration:

```
A → B (+): A respects B
A ← C (-): C dislikes A (or negative in opposite direction)
What about B and C?
```

| Theory      | Prediction for B→C                                                                         | Reasoning                              |
| ----------- | ------------------------------------------------------------------------------------------ | -------------------------------------- |
| **Balance** | B should be negative toward C (friend of my enemy is my enemy)                             | Psychological consistency              |
| **Status**  | Depends on status ranks. If C has higher status than B, edge could be positive (deference) | Hierarchy determines sign, not balance |

### Concrete Conflict Example

**Scenario:**
- A = Junior employee
- B = Senior employee (mentor to A)
- C = VP from another department

**Given:**
- A → B (+) (A respects mentor)
- A ← C (-) (VP dislikes A — perhaps negative from A's perspective)

**Question:** What is B → C?

| Theory | Prediction | Why |
|--------|------------|-----|
| **Balance** | B → C negative (friend of my friend? Wait: A is friend of B? Actually A→B positive. C is enemy of A. So B should dislike C) | Consistency |
| **Status** | B → C positive (B has lower status than C, so B defers to C) | Hierarchy |

**Same situation → Opposite predictions!**

### Another Classic Conflict: The Cycle of Three

Consider a directed 3-cycle:

```
A → B (+)
B → C (+)
C → A (+)
All positive in one direction around the cycle.
```

| Theory      | Interpretation                                                              | Balanced?          |
| ----------- | --------------------------------------------------------------------------- | ------------------ |
| **Balance** | Cannot evaluate (requires undirected)                                       | N/A                |
| **Status**  | Impossible (cannot all have higher status than the next — cycle has no top) | Violates hierarchy |

### Empirical Findings

Research (Leskovec, Huttenlocher, Kleinberg 2010) on real signed networks (Epinions, Slashdot, Wikipedia) found:

| Finding | Implication |
|---------|-------------|
| Balance theory predicts some edges well | Especially in social/friend networks |
| Status theory predicts others better | Especially in hierarchical/deference networks |
| Neither dominates universally | Context matters |

### When Each Theory Works Best

| Network Type                   | Better Theory | Reason                                        |
| ------------------------------ | ------------- | --------------------------------------------- |
| Undirected social friendships  | Balance       | People seek consistent friend/enemy relations |
| Directed trust/advice networks | Status        | Reflects hierarchy and deference              |
| Political alliances            | Both (mixed)  | Balance for enmity, status for alliances      |
| Online ratings (like/dislike)  | Balance       | Users express consistent opinions             |

---

## Part 5: Resolving the Conflict — Modern Approaches

### 1. **Hybrid Models**
Combine both theories with weights:
- Some edges follow balance
- Others follow status
- Learn which applies from data

### 2. **Context-Dependent Predictions**
If the network has clear hierarchy (e.g., workplace), use status.  
If flat and social (e.g., Facebook friends), use balance.

### 3. **Signed Directed Balance**
Extended balance theory to directed edges:
- A triangle is balanced if product of signs along any cycle is positive
- Incorporates direction + sign

### 4. **Machine Learning Approach**
Train a classifier on:
- Balance-based features (number of balanced/unbalanced triangles)
- Status-based features (status differences, directed paths)
- Let the model decide which matters more

---

## Part 6: Summary Comparison Table

| Aspect | Structural Balance | Status |
|--------|-------------------|--------|
| **Origin** | Heider (1940s) | White (1980s) |
| **Graph type** | Undirected | Directed |
| **Edge meaning** | Friend/Enemy | Deference/Rivalry |
| **Key principle** | Even number of negatives | Status hierarchy |
| **Predicts** | Consistency | Rank-ordered respect |
| **Folk rule** | "Friend of friend is friend" | "Respect those above you" |
| **Real example** | Social cliques | Corporate hierarchy |
| **Conflict with other** | Predicts (+, -, -) as balanced | May reverse this prediction |

---

## Your One-Sentence Takeaway

> *"Structural Balance says networks seek psychological consistency (even number of negatives per triangle), while Status Theory says networks reflect social hierarchy (positive edges flow upward) — and these theories conflict when predicting real signed networks, requiring context or hybrid models to resolve."*

---

## Quick Reference Card

| Term               | Definition                                                           |
| ------------------ | -------------------------------------------------------------------- |
| **Signed network** | Graph with + and - edges                                             |
| **Balance**        | Even negatives per triangle = stable                                 |
| **Unbalance**      | Odd negatives per triangle = tension                                 |
| **Status**         | Positive edges point from low→high status                            |
| **Conflict**       | Balance and status make opposite predictions in some directed cycles |

---

Would you like me to provide **mathematical formulas** for computing balance scores or **real dataset examples** (Epinions, Slashdot) showing where each theory wins?