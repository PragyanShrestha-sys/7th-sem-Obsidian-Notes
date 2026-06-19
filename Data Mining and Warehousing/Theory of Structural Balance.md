## Part 2: Theory of Structural Balance

### Origin
Developed by **Fritz Heider** (1940s) and formalized by **Dorwin Cartwright** and **Frank Harary** (1950s).

### Core Idea
> *People seek consistency in their relationships. Unbalanced configurations create psychological tension that motivates change.*

### The Mathematical Definition

**A signed triangle is balanced if it contains an even number of negative edges (0 or 2).**

| Triangle  | Negatives | Balanced? | Product |
| --------- | --------- | --------- | ------- |
| (+, +, +) | 0         | ✅         | +       |
| (+, -, -) | 2         | ✅         | +       |
| (+, +, -) | 1         | ❌         | -       |
| (-, -, -) | 3         | ❌         | -       |

### The Logic Behind Balance

| Pattern   | Folk Saying                        | Why Balanced                    |
| --------- | ---------------------------------- | ------------------------------- |
| (+, +, +) | "Friend of my friend is my friend" | Consistent                      |
| (+, -, -) | "Enemy of my enemy is my friend"   | Consistent                      |
| (+, +, -) | "Friend of my friend is my enemy"  | **Contradiction**               |
| (-, -, -) | "Enemy of my enemy is my enemy"    | Contradiction (by product rule) |

### Example of Unbalance (+, +, -)

```
      Alice (+) Bob
        |       |
        |       |
       (+)     (+)
        |       |
        └─ Carol ─┘
           (No edge? Wait, triangle needs all three edges)

Correct triangle:
      Alice
       / \
    (+)   (-)
     /     \
    Bob (+) Carol
```

**Interpretation:**
- Alice is friends with Bob
- Alice is friends with Carol
- Bob and Carol are enemies

**Tension:** Alice is caught in the middle. She cannot please both. Something must change.

### Possible Resolutions to Unbalance

| Change                                    | New Triangle | Result   |
| ----------------------------------------- | ------------ | -------- |
| Bob and Carol become friends              | (+, +, +)    | Balanced |
| Alice picks Bob, becomes enemy with Carol | (+, -, -)    | Balanced |
| Alice picks Carol, becomes enemy with Bob | (+, -, -)    | Balanced |

### Balance at Network Level

A **complete signed network** is balanced if:
> It is possible to partition nodes into two groups such that all positive edges are **within** groups and all negative edges are **between** groups.

**Visual:**
```
Group 1: {A, B, C}    Group 2: {D, E, F}
- All internal edges: positive (+)
- All cross-group edges: negative (-)
```

This is the **"two factions" theorem**.

### Real Example of Structural Balance

**Cold War Era:**
- USA and USSR: Negative (enemies)
- USA and UK: Positive (allies)
- USSR and UK: Negative (enemies)

Triangle: (-, +, -) → 2 negatives → ✅ Balanced

---
