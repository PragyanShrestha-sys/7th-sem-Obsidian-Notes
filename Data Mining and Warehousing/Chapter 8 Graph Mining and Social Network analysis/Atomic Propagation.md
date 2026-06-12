![[Pasted image 20260514173846.png]]

You're right to want a clean slate. Let me explain **Atomic Propagation of Trust in a Network** from scratch, in detail, without mixing things up.

---

## Part 1: What Is a Trust Network?

A **trust network** is a directed graph where:

| Component | Meaning |
|-----------|---------|
| **Nodes** | People or entities |
| **Directed edge A → B** | "A trusts B" |
| **No edge** | No direct trust relationship |

**Example:**
```
Alice → Bob   (Alice trusts Bob)
Alice → Carol (Alice trusts Carol)
Bob → David   (Bob trusts David)
```

**Optional:** Trust can have weights (e.g., 0.8 for "highly trust", 0.3 for "slightly trust")

---

## Part 2: The Problem Atomic Propagation Solves

### The Problem

In a trust network, most node pairs have **no direct edge**. But we need to know: *Should A trust C?*

### The Solution

If we know:
- A trusts B
- B trusts C

Then we can **infer** that A should trust C — even without a direct edge.

### The Name "Atomic"

**Atomic** means:
- **One single inference step**
- Using **exactly two known edges**
- Producing **exactly one new inferred edge**
- No chaining (stop after one step)

> *"Atomic propagation = one inference from two known edges to one new edge."*

---

## Part 3: The Building Block — Simple Direct Propagation

Before the four types, understand the **basic idea**:

**Known:**
```
A → B
B → C
```

**Inferred:**
```
A → C
```

**Visual:**
```
A → B → C  (known)
↓
A → C      (inferred)
```

**This is the foundation.** The four types below are variations of this basic pattern.

---

## Part 4: The Four Types of Atomic Propagation

All four types follow the same principle: **two known edges → one inferred edge**.

The difference is **which nodes are connected** in the known edges.

---

### Type 1: Direct Propagation

**Also called:** Transitive trust, chain propagation

**Known edges:**
```
A → B  (A trusts B)
B → C  (B trusts C)
```

**Inferred edge:**
```
A → C  (A trusts C)
```

**Visual:**
```
A -----→ B -----→ C
 \               /
  \_____________/
     inferred
```

**Real example:**
- You (A) trust your friend Bob (B)
- Bob trusts seller Carol (C)
- **Inference:** You should trust Carol

**Formula (with weights):**
```
trust(A, C) = trust(A, B) × trust(B, C)
```

**Example with numbers:**
- trust(A, B) = 0.9
- trust(B, C) = 0.8
- trust(A, C) = 0.9 × 0.8 = 0.72

---

### Type 2: Trust Coupling

**Also called:** Co-citation coupling (but careful — this is different from co-citation)

**Known edges:**
```
A → C  (A trusts C)
B → C  (B trusts C)
```

**Inferred edge:**
```
A ↔ B  (A and B trust each other — bidirectional)
```

**Visual:**
```
    A       B
     \     /
      \   /
       \ /
        C
(known: A→C, B→C)
(inferred: A←→B)
```

**Real example:**
- You (A) trust your financial advisor Carol (C)
- Your colleague (B) trusts the same advisor Carol (C)
- **Inference:** You and your colleague should trust each other (on financial matters)

**Why it works:** Shared trust in a common third party creates a bond between the trustors.

**Formula (with weights):**
```
trust(A, B) = trust(A, C) × trust(B, C)
trust(B, A) = same (symmetric inference)
```

**Example with numbers:**
- trust(A, C) = 0.9
- trust(B, C) = 0.8
- trust(A, B) = 0.9 × 0.8 = 0.72

**Note:** The inferred edge is usually considered **bidirectional** (trust both ways).

---

### Type 3: Co-citation

**Also called:** Bibliographic coupling (originally from citation analysis)

**Known edges:**
```
A → B  (A trusts B)
A → C  (A trusts C)
```

**Inferred edge:**
```
B ↔ C  (B and C are similar — likely trust each other)
```

**Visual:**
```
        A
       / \
      /   \
     B     C
(known: A→B, A→C)
(inferred: B←→C)
```

**Real example:**
- You (A) trust plumber Bob (B)
- You (A) trust electrician Carol (C)
- **Inference:** Bob and Carol are likely similar in quality and reliability

**Real-world use:** Amazon's "Customers who bought from B also bought from C"

**Formula (similarity score):**
```
similarity(B, C) = trust(A, B) × trust(A, C)
```
Or aggregate over all common trustors.

**Note:** This infers **similarity**, not necessarily direct trust. In trust networks, similarity often implies reciprocal trust.

---

### Type 4: Transpose Trust

**Also called:** Trust reversal, symmetry inference

**Known edge:**
```
A → B  (A trusts B)
```

**Inferred edge:**
```
B → A  (B trusts A) — only in specific contexts
```

**Visual:**
```
A → B (known)
↑     |
|_____|
inferred (B → A)
```

**Important:** Trust is **not automatically symmetric**. Transpose is **context-dependent**.

| Context | Is transpose valid? | Example |
|---------|--------------------|---------|
| Friendship | ✅ Yes | Facebook friends |
| Collaboration | ✅ Yes | Co-authors on a paper |
| Advice/Supervision | ❌ No | Student trusts professor; professor doesn't automatically trust student |
| E-commerce | ❌ No | Buyer trusts seller; seller doesn't automatically trust buyer |

**Real example (valid):**
- A and B are friends on Facebook
- A → B (trust inferred from friendship)
- **Transpose valid:** B → A (friendship is mutual)

**Formula (when valid):**
```
trust(B, A) = trust(A, B)
```

**Formula (with decay, optional):**
```
trust(B, A) = trust(A, B) × δ
```
where δ is a symmetry factor (≤ 1)

---

## Part 5: Comparison Table of All Four Types

| Type | Known Edges | Inferred Edge | Pattern Name | Shape |
|------|-------------|---------------|--------------|-------|
| **Direct propagation** | A→B, B→C | A→C | Linear chain | A→B→C |
| **Trust coupling** | A→C, B→C | A↔B | Common target | V (target) |
| **Co-citation** | A→B, A→C | B↔C | Common source | V (source) |
| **Transpose trust** | A→B | B→A | Reversal | A↔B (if valid) |

---

## Part 6: Complete Real-World Example

### Scenario: A Professional Network

**Initial known trust edges:**
1. Alice → Bob (0.9) — Alice trusts Bob (colleague)
2. Bob → Carol (0.8) — Bob trusts Carol (former manager)
3. Alice → David (0.7) — Alice trusts David (vendor)
4. Alice → Eve (0.6) — Alice trusts Eve (vendor)
5. Frank → Carol (0.85) — Frank trusts Carol (mentor)

### Applying Atomic Propagation (each type separately)

| Type | Known | Inferred | Score |
|------|-------|----------|-------|
| **Direct propagation** | Alice→Bob, Bob→Carol | Alice→Carol | 0.9 × 0.8 = 0.72 |
| **Trust coupling** | Alice→Eve, Frank→Eve | Alice↔Frank | 0.6 × 0.85 = 0.51 (each direction) |
| **Co-citation** | Alice→David, Alice→Eve | David↔Eve | Similarity score = 0.7 × 0.6 = 0.42 |
| **Transpose trust** (friendship context) | Alice→Bob | Bob→Alice | 0.9 (assuming symmetry) |

**Result:** Alice now has 4 new inferred trust relationships from just one step of atomic propagation.

---

## Part 7: Why "Atomic" Is Important

**Atomic** means **one step only**. No repeated chaining.

| Atomic Propagation | Iterative Propagation |
|--------------------|----------------------|
| One inference step | Multiple repeated steps |
| Uses only original known edges | Uses previously inferred edges |
| Maximum path length = 2 hops | Can reach unlimited hops |
| Simple, fast, no cycles | Complex, can oscillate |
| Building block | Full system |

**Example of iterative (not atomic):**
- Step 1 (atomic): A→B, B→C → A→C
- Step 2 (iterative): Now use A→C (inferred) with C→D → A→D (second step)

Atomic propagation stops after Step 1. Iterative continues.

---

## Part 8: Summary — One Sentence Each

| Type | One Sentence |
|------|--------------|
| **Direct propagation** | *If A trusts B and B trusts C, then A trusts C.* |
| **Trust coupling** | *If A and B both trust C, then A and B trust each other.* |
| **Co-citation** | *If A trusts both B and C, then B and C are similar (likely trust each other).* |
| **Transpose trust** | *If A trusts B and the relationship is symmetric (e.g., friendship), then B trusts A.* |

---

## Part 9: Quick Reference Card

```
Direct:      A → B → C        →   A → C
Coupling:    A → C ← B        →   A ↔ B
Co-citation: A → B and A → C  →   B ↔ C
Transpose:   A → B            →   B → A (only if symmetric context)
```

---

## Part 10: The Most Important Thing to Remember

> **Atomic propagation always uses exactly two known trust edges to infer exactly one new trust edge — in a single step. The four types differ only in which nodes are connected in the known edges.**

---

This is the complete, correct, from-scratch explanation. Would you like me to provide **practice problems** or **numerical examples with calculations** to test your understanding?