![[Pasted image 20260514173846.png]]

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

**Optional:** Trust can have **weights** (e.g., 0.8 for "highly trust", 0.3 for "slightly trust")

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

## Part 4: [[The Four Types of Atomic Propagation]]

All four types follow the same principle: **two known edges → one inferred edge**.

The difference is **which nodes are connected** in the known edges.

## Part 5: Comparison Table of All Four Types

| Type                   | Known Edges | Inferred Edge | Pattern Name  | Shape          |
| ---------------------- | ----------- | ------------- | ------------- | -------------- |
| **Direct propagation** | A→B, B→C    | A→C           | Linear chain  | A→B→C          |
| **Trust coupling**     | A→C, B→C    | A↔B           | Common target | V (target)     |
| **Co-citation**        | A→B, A→C    | B↔C           | Common source | V (source)     |
| **Transpose trust**    | A→B         | B→A           | Reversal      | A↔B (if valid) |

---

## Part 6: [[Complete Real-World Example]]


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