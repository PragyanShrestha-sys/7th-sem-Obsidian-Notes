Here are short, focused introductions to each.

---

## 1. [[Beam Search]]

**What it is:** A heuristic graph search algorithm.

**What it does:** Explores a graph by expanding only the **top k most promising nodes** at each level (k = beam width).

**How it works (simple):**
1. Start at root
2. Generate all child nodes
3. Score them using a heuristic
4. Keep only the **k highest-scoring** nodes
5. Repeat from those nodes

**Analogy:** A manager who only interviews the top 5 candidates at each round instead of everyone.

**In graph mining:** Used to grow subgraph patterns step by step without exploding exponentially.

**One sentence:** *Beam search keeps k best candidates at each step — a practical middle-ground between greedy (k=1) and exhaustive search.*

---

## 2. [[Inductive Logic Programming (ILP)]]

**What it is:** A rule-learning algorithm that uses logic.

**What it does:** Learns **if-then rules** from relational data (facts about connections between entities).

**How it works (simple):**
1. Given: facts (e.g., `parent(alice, bob)`) + examples (`grandparent(alice, carol)` = true)
2. Search for logical rules that explain the examples
3. Output rule: `grandparent(X,Y) :- parent(X,Z), parent(Z,Y)`

**Analogy:** A detective who watches who talks to whom and writes a rule: "If A talks to B and B talks to C, then A knows C indirectly."

**In graph mining:** Discovers patterns involving graph relationships (edges) — not just node attributes.

**One sentence:** *ILP learns logical rules that describe how entities in a graph relate to each other.*

---

## Quick Comparison

| | **Beam Search** | **ILP** |
|---|----------------|---------|
| **Type** | Search algorithm | Rule learning algorithm |
| **Output** | Path or subgraph | Logical rule |
| **Key idea** | Keep top k nodes | Generalize from examples |
| **Analogy** | Hiring manager with shortlist | Detective writing case rules |
