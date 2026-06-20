
## What Is Beam Search? (Detailed Definition)

**Beam Search** is a [[heuristic]] search algorithm that explores a graph by expanding only the **most promising nodes** at each depth level, where "most promising" means the top **k** nodes according to a scoring function.

**Beam width (k)** = the maximum number of nodes kept at each level.

**Trade-off:**
- Small k → faster, less memory, but may miss the optimal solution
- Large k → slower, more memory, closer to optimal

---
## Why Is Beam Search Used?

| Problem                                              | Why Beam Search?                                                                               |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Exponential explosion(search space thulo huncha)** | Many problems (like graph mining) have massive search spaces. Exhaustive search is impossible. |
| **Memory constraints**                               | BFS stores all nodes at a level — infeasible for large graphs.                                 |
| **Speed requirements**                               | Need a "good enough" solution quickly, not necessarily optimal.                                |
| **Real-time systems**                                | Speech recognition, machine translation, route planning — must decide fast.                    |

**Common applications:**
- Speech recognition (finding most likely word sequence)
- Machine translation (choosing best translation path)
- Graph mining (growing frequent subgraphs)
- Pathfinding in large maps
- Decoding in neural networks (e.g., beam search for text generation)

---
## How Is It Used? (Step-by-Step Process)

## Real-Life Numerical Example: Planning a Vacation Trip

### Scenario

You are planning a **5-day vacation** starting from New York. Each day you choose a city to visit. You want to maximize "enjoyment score" but cannot explore all possible paths (millions).
**Data:**

| Day          | Possible cities                                     |
| ------------ | --------------------------------------------------- |
| 1 (from NYC) | Boston (B): 80, Washington (W): 90, Chicago (C): 70 |
| 2            | From B: Montreal(85), NYC(60), Philly(75)           |
| 2            | From W: Richmond(70), Atlanta(95), Nashville(80)    |
| 2            | From C: Detroit(65), StLouis(75), Indianapolis(70)  |

**Goal:** Find the best 3-day trip (Days 1-2 are enough to illustrate).
**Beam width (k) = 2**

**Beam width (k = 2)** means that at each step (each day), you only keep the **top 2 most promising partial trips** (highest total enjoyment so far), instead of keeping all possible paths.

---
### Step-by-Step Execution

#### Day 0 (Start)
```
Frontier = [NYC (score 0)]
```

---

#### Day 1 — Expand

Expand NYC → generate all possible Day 1 cities:

| Path             | Score |
| ---------------- | ----- |
| NYC → Boston     | 80    |
| NYC → Washington | 90    |
| NYC → Chicago    | 70    |

**All candidates:** [B:80, W:90, C:70]

**Sort by score (highest first):** [W:90, B:80, C:70]

**Keep top k=2:** [W:90, B:80]

**Frontier after Day 1:** 
- Path A: NYC → Washington (score 90)
- Path B: NYC → Boston (score 80)

(Discard Chicago with score 70)

---

#### Day 2 — Expand from both kept nodes

**From Washington (Path A, score 90):**

| Path            | Total Score   |
| --------------- | ------------- |
| NYC→W→Richmond  | 90 + 70 = 160 |
| NYC→W→Atlanta   | 90 + 95 = 185 |
| NYC→W→Nashville | 90 + 80 = 170 |

**From Boston (Path B, score 80):**

| Path           | Total Score   |
| -------------- | ------------- |
| NYC→B→Montreal | 80 + 85 = 165 |
| NYC→B→NYC      | 80 + 60 = 140 |
| NYC→B→Philly   | 80 + 75 = 155 |

**All candidates:** 
- W→Atlanta: 185
- W→Nashville: 170
- B→Montreal: 165
- W→Richmond: 160
- B→Philly: 155
- B→NYC: 140

**Sort by score:** [185, 170, 165, 160, 155, 140]

**Keep top k=2:** 
- Path 1: NYC → Washington → Atlanta (score 185)
- Path 2: NYC → Washington → Nashville (score 170)

---

### Final Result

| Beam Search (k=2)         | Best possible path (exhaustive search) |
| ------------------------- | -------------------------------------- |
| NYC→W→Atlanta (score 185) | NYC→W→Atlanta (score 185)              |

In this case, Beam Search found the **optimal** path. If we had used k=1 (greedy):
- Day 1 chose Washington (best)
- Day 2 would only explore from Washington
- Still would find Atlanta (185) — also optimal here

---

## What If Beam Search Misses the Optimum?

Let me add a counterexample:

Suppose at Day 2:
- From Washington: Atlanta (95), Miami (94)
- From Boston: Orlando (99) — very high

With k=2:
- Day 1: Washington (90), Boston (80) — both kept
- Day 2: From Washington → Atlanta (185), from Boston → Orlando (179) — both in top 2

With k=1 (greedy):
- Day 1: Only Washington (drops Boston)
- Day 2: Sees Atlanta and Miami, never sees Orlando → **Misses optimal**

**Beam Search with k=2** would keep both and find Orlando.

| k value | Finds optimal? | Memory used |
|---------|---------------|-------------|
| 1 (greedy) | Not always | Very low |
| 2 | More often | Low |
| 10 | Very often | Medium |
| ∞ (BFS) | Always | Huge |

---

## Why Beam Search in Graph Mining?

In **frequent subgraph mining**:

| Step | Beam Search role |
|------|------------------|
| Start | Single node (small subgraph) |
| Expand | Add one edge at a time (all possibilities) |
| Score | Frequency of subgraph in database |
| Keep | Top k most frequent subgraphs |
| Repeat | Grow only the promising ones |

**Without beam search:** Number of possible subgraphs grows exponentially → impossible.

**With beam search:** You explore only the promising patterns.

---

## Summary Table

| Aspect | Detail |
|--------|--------|
| **Type** | Heuristic search |
| **Input** | Graph, start node, scoring function, beam width k |
| **Output** | Path or subgraph (often not guaranteed optimal) |
| **Key parameter** | Beam width (k) |
| **Advantage** | Memory efficient, fast, finds good solutions |
| **Disadvantage** | Can miss optimal if k too small |
| **Used in graph mining for** | Growing candidate subgraphs step by step |

---

## Your One-Sentence Takeaway

> *"Beam Search keeps only the top k most promising partial solutions at each step, trading perfect optimality for massive speed and memory savings — essential for huge search spaces like subgraph mining."*

