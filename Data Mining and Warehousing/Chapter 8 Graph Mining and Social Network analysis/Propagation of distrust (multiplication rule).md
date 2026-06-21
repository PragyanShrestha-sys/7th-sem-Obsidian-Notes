Here is a **complete, from-scratch explanation** of **Propagation of Distrust** in a network.

note: maile ni ramro sanga padheko chaina 

---
## Part 1: What Is Distrust?

In a trust network, **distrust** is the negative counterpart of trust.

| Term | Meaning | Edge Sign |
|------|---------|-----------|
| **Trust** | A believes B will act in A's best interest | (+) |
| **Distrust** | A believes B will act against A's interest | (-) |
| **Unknown** | No direct opinion | (no edge) |

**Example:**
```
Alice → Bob (+)   (Alice trusts Bob)
Alice → Carol (-) (Alice distrusts Carol)
```

---
## Part 2: Why Propagate Distrust?

### The Same Problem as Trust
Most node pairs have no direct edge. We need to infer whether A should **distrust** C based on known relationships.
### The Core Insight
Distrust propagates **differently** from trust. It follows a **sign multiplication rule**.

> *"Trust and distrust multiply like positive and negative numbers."*

---
## Part 3: The Fundamental Rules of Distrust Propagation

### The Sign Multiplication Table

| A → B        | B → C        | A → C (inferred) |
| ------------ | ------------ | ---------------- |
| Trust (+)    | Trust (+)    | Trust (+)        |
| Trust (+)    | Distrust (-) | Distrust (-)     |
| Distrust (-) | Trust (+)    | Distrust (-)     |
| Distrust (-) | Distrust (-) | Trust (+)        |

## Part 5: Atomic Propagation of Distrust

Just like trust, distrust propagation can be **atomic** (one step, two known edges → one inferred edge).
### The Four Types (with Distrust)

| Type | Known | Inferred | Example |
|------|-------|----------|---------|
| **Direct propagation** | A→B (+), B→C (-) | A→C (-) | Friend's enemy is my enemy |
| **Trust coupling** | A→C (-), B→C (-) | A↔B (+) | Two people who distrust the same person should trust each other |
| **Co-citation** | A→B (-), A→C (-) | B↔C (+) | Two people distrusted by the same person are similar (allies) |
| **Transpose** | A→B (-) | B→A (-) (if symmetric) | Distrust is often mutual |

---

## Part 6: Real-World Examples

### Example 1: Direct Propagation (Trust + Distrust = Distrust)

**Scenario:**
- Alice trusts Bob
- Bob distrusts Carol

**Inference:** Alice should distrust Carol

**Real life:** "My good friend Bob hates Carol. I trust Bob's judgment, so I probably hate Carol too."

---

### Example 2: Direct Propagation (Distrust + Distrust = Trust)

**Scenario:**
- Alice distrusts Bob
- Bob distrusts Carol

**Inference:** Alice should trust Carol

**Real life:** "The enemy of my enemy is my friend." If Alice and Bob are enemies, and Bob hates Carol, then Alice and Carol are natural allies.

---

### Example 3: Trust Coupling with Distrust

**Scenario:**
- Alice distrusts David
- Bob distrusts David

**Inference:** Alice and Bob should trust each other

**Real life:** "We both hate the same person. We must be on the same side."

---

### Example 4: Co-citation with Distrust

**Scenario:**
- David distrusts Alice
- David distrusts Bob

**Inference:** Alice and Bob are similar (likely trust each other)

**Real life:** "If David hates both Alice and Bob, then Alice and Bob are probably allies."

---

## Part 7: Numerical Example with Trust Scores

If trust/distrust is represented as a **score from -1 to +1**:

| Score | Meaning |
|-------|---------|
| +1.0 | Strong trust |
| +0.3 | Weak trust |
| 0 | Neutral / unknown |
| -0.3 | Weak distrust |
| -1.0 | Strong distrust |

### Propagation Formula (Same as Multiplication)

```
trust(A, C) = trust(A, B) × trust(B, C)
```

### Worked Example

**Known:**
- trust(A, B) = +0.9 (strong trust)
- trust(B, C) = -0.7 (moderate distrust)

**Calculation:**
```
trust(A, C) = (+0.9) × (-0.7) = -0.63
```

**Result:** A distrusts C with moderate strength (-0.63)

---

### Another Example

**Known:**
- trust(A, B) = -0.8 (strong distrust)
- trust(B, C) = -0.6 (moderate distrust)

**Calculation:**
```
trust(A, C) = (-0.8) × (-0.6) = +0.48
```

**Result:** A trusts C with moderate strength (+0.48)

---

## Part 8: Distrust Propagation vs Trust Propagation

| Aspect | Trust Propagation | Distrust Propagation |
|--------|-------------------|----------------------|
| **Base rule** | (+) × (+) = (+) | Follows sign multiplication |
| **Handles negatives?** | No | Yes |
| **Folk saying** | "Friend of friend is friend" | "Enemy of enemy is friend" |
| **Complexity** | Simple | Requires sign tracking |
| **Real-world use** | Recommendations, referrals | Fraud detection, conflict prediction |

---

## Part 9: Limitations and Challenges

| Challenge | Explanation |
|-----------|-------------|
| **Oscillation** | In cycles, distrust can flip back and forth repeatedly |
| **Convergence** | May never stabilize in signed networks |
| **Transitivity breakdown** | "Enemy of my enemy" is not always true in real life |
| **Context matters** | Political vs personal vs professional distrust differ |
| **Data sparsity** | Distrust edges are rarer than trust edges in most networks |

---

## Part 10: Summary Table

| Rule | Known | Inferred | Folk Saying |
|------|-------|----------|-------------|
| 1 | Trust + Trust | Trust | Friend of friend is friend |
| 2 | Trust + Distrust | Distrust | Friend of enemy is enemy |
| 3 | Distrust + Trust | Distrust | Enemy of friend is enemy |
| 4 | Distrust + Distrust | Trust | Enemy of enemy is friend |

---

## Part 11: Complete Real-World Example

### Scenario: Political Alliances (Three Countries)

**Known relationships:**
- Country A → Country B: Trust (+) (allies)
- Country B → Country C: Distrust (-) (enemies)

**Atomic propagation:**
- A → B (+), B → C (-) → A → C (-)

**Inference:** A should distrust C (enemy of my friend is my enemy)

**Real-world parallel:** Cold War alliances:
- USA → UK (+) (allies)
- UK → USSR (-) (enemies)
- Inference: USA → USSR (-) (enemies) — historically accurate

---

### Another Example: Complicated Alliance

**Known:**
- Country X → Country Y: Distrust (-) (enemies)
- Country Y → Country Z: Distrust (-) (enemies)

**Atomic propagation:**
- X → Y (-), Y → Z (-) → X → Z (+)

**Inference:** X should trust Z (enemy of my enemy is my friend)

**Real-world parallel:**
- USA → USSR (-) (Cold War enemies)
- USSR → China (-) (Sino-Soviet split)
- Inference: USA → China (+) (rapprochement) — historically accurate (Nixon went to China)

---

## Your One-Sentence Takeaway

> *"Distrust propagates by multiplying signs: trust (+) times distrust (-) gives distrust (-); distrust (-) times distrust (-) gives trust (+); following the folk wisdom: friend of enemy is enemy, enemy of enemy is friend."*

---

## Quick Reference Card

```
Multiplication Rule for Trust/Distrust Propagation:

(+) × (+) = (+)
(+) × (-) = (-)
(-) × (+) = (-)
(-) × (-) = (+)
```

---

Would you like me to provide **practice problems** with numerical scores or **iterative propagation of distrust** (multiple hops) next?