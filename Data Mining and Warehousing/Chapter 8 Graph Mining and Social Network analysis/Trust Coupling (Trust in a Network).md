## What is Trust in a Network?

In a network, **trust** is a directed edge from one node (trustor) to another node (trustee) indicating a positive expectation.

| Term         | Meaning                                      |
| ------------ | -------------------------------------------- |
| **Trust**    | "A believes B will act in A's interest"      |
| **Distrust** | "A believes B will act against A's interest" |
| **Unknown**  | No direct relationship or opinion            |

**Representation:**
- **Positive edge (+):** Trust
- **Negative edge (-):** Distrust
- **No edge:** Unknown
**Example (online rating system):**

text

User A → User B (+5)  "A strongly trusts B"
User C → User D (-3)  "C distrusts D"

---
## Part 2: Why Propagate Trust?

### The Problem

In most real networks, the graph is **sparse** — most node pairs have no direct edge.
### The Solution
If A trusts B, and B trusts C, then **A should have some level of trust in C** — even without a direct relationship.

**Real-world analogy:**

> "My friend recommends a mechanic. I've never met the mechanic, but I trust my friend, so I trust the mechanic."

### Applications

| Domain                    | Use of Trust Propagation                         |
| ------------------------- | ------------------------------------------------ |
| E-commerce (eBay, Amazon) | "Seller has 5-star rating from people you trust" |
| Social media              | "Your friend liked this comment"                 |
| Recommendation systems    | "People you trust liked this movie"              |
| Blockchain/DeFi           | Reputation networks, lending without collateral  |
| Cybersecurity             | Trust-based access control                       |

---

There are 3 ways of [[propagating trust and distrust]] in a network ig



---
