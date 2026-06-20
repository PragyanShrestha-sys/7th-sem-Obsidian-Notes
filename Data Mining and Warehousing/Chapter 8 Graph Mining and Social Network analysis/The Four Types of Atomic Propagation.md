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
