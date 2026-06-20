### Scenario: A Professional Network

**Initial known trust edges:**
1. Alice → Bob (0.9) — Alice trusts Bob (colleague)
2. Bob → Carol (0.8) — Bob trusts Carol (former manager)
3. Alice → David (0.7) — Alice trusts David (vendor)
4. Alice → Eve (0.6) — Alice trusts Eve (vendor)
5. Frank → Carol (0.85) — Frank trusts Carol (mentor)

### Applying Atomic Propagation (each type separately)

| Type                                     | Known                  | Inferred    | Score                               |
| ---------------------------------------- | ---------------------- | ----------- | ----------------------------------- |
| **Direct propagation**                   | Alice→Bob, Bob→Carol   | Alice→Carol | 0.9 × 0.8 = 0.72                    |
| **Trust coupling**                       | Alice→Eve, Frank→Eve   | Alice↔Frank | 0.6 × 0.85 = 0.51 (each direction)  |
| **Co-citation**                          | Alice→David, Alice→Eve | David↔Eve   | Similarity score = 0.7 × 0.6 = 0.42 |
| **Transpose trust** (friendship context) | Alice→Bob              | Bob→Alice   | 0.9 (assuming symmetry)             |

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
