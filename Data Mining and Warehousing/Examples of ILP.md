## Clean Real-Life Numerical Example: Learning "Parent" and "Grandparent"

Let's use a simpler relationship: **Learning what "grandparent" means.**

### Step 1: Background Knowledge (Facts)

**Family graph:**

```
           alice (F)
              |
           bob (M)
              |
         carol (F)
              |
         david (M)
```

**Facts stored in the database:**

| Fact ID | Predicate | Arguments |
|---------|-----------|-----------|
| F1 | `parent` | (alice, bob) |
| F2 | `parent` | (bob, carol) |
| F3 | `parent` | (carol, david) |
| F4 | `male` | (bob) |
| F5 | `male` | (david) |
| F6 | `female` | (alice) |
| F7 | `female` | (carol) |

### Step 2: Examples Provided to ILP

**Positive examples** (true `grandparent` relationships):

| Example | True? |
|---------|-------|
| P1: `grandparent(alice, carol)` | Yes |
| P2: `grandparent(alice, david)` | Yes |
| P3: `grandparent(bob, david)` | Yes |

**Negative examples** (false `grandparent` relationships):

| Example | True? |
|---------|-------|
| N1: `grandparent(alice, bob)` | No (bob is child, not grandchild) |
| N2: `grandparent(bob, carol)` | No (bob is parent, not grandparent) |
| N3: `grandparent(carol, david)` | No (carol is parent, not grandparent) |

### Step 3: What ILP Does (Numerical Walkthrough)

ILP starts with a **very general rule** and specializes it until it covers all positives and no negatives.

#### Initial rule (too general):
```
grandparent(X, Y) :- true.
```
This says "everyone is grandparent of everyone" — covers all positives ✅ but also covers all negatives ❌

#### Step 1 — Add first condition:
Try: `grandparent(X, Y) :- parent(X, Z).`

| Example | Covered? | Notes |
|---------|----------|-------|
| P1: (alice, carol) | ✅ Yes (alice parent of bob) | Good |
| N1: (alice, bob) | ✅ Yes (alice parent of bob) | ❌ Still covers negative |

Still covers negatives — need more conditions.

#### Step 2 — Add second condition:
Try: `grandparent(X, Y) :- parent(X, Z), parent(Z, Y).`

Test each example against this rule:

**Positive P1: `grandparent(alice, carol)`**
- `parent(alice, Z)` → Z can be `bob`
- `parent(bob, carol)` → Yes, Z=bob works
- **Result:** P1 covered ✅

**Positive P2: `grandparent(alice, david)`**
- `parent(alice, Z)` → Z can be `bob`
- `parent(bob, david)` → Is this true? No! (bob is parent of carol, not david)
- Try Z=c? `parent(alice, carol)` — No, alice is not parent of carol
- **Result:** P2 not covered ❌

Problem: P2 fails because our family tree is only 3 generations deep? Let me fix.

Actually, in the tree: alice → bob → carol → david
For `grandparent(alice, david)`:
- Need Z such that: `parent(alice, Z)` and `parent(Z, david)`
- `parent(alice, Z)` → Z = bob
- `parent(bob, david)` → False (bob is parent of carol, not david)

So P2 is **not** a grandparent in this tree. Let me correct the family tree to make P2 true.

**Corrected family tree:**

```
alice (F)
   |
  bob (M)
   | \
   |  \
carol (F) david (M)  (bob is parent of both)
```

**Facts:**
- `parent(alice, bob)`
- `parent(bob, carol)`
- `parent(bob, david)`

Now test again:

**P1: `grandparent(alice, carol)`** ✅ (alice → bob → carol)
**P2: `grandparent(alice, david)`** ✅ (alice → bob → david)

**Negative N1: `grandparent(alice, bob)`** ❌ (needs two parent steps, only one exists)

Rule works: `grandparent(X, Y) :- parent(X, Z), parent(Z, Y).`

### Step 4: ILP Output

**Final learned rule:**
```
grandparent(X, Y) :- parent(X, Z), parent(Z, Y).
```

**In English:** *X is grandparent of Y if there exists a Z such that X is parent of Z and Z is parent of Y.*

### Step 5: Numerical Scoring of Rule Quality

ILP typically uses measures like:

| Metric | Formula | For our rule |
|--------|---------|--------------|
| **Coverage** | Number of positives covered | 3/3 = 1.0 |
| **Accuracy** | (Positives covered + Negatives rejected) / Total | (3+2)/5 = 1.0 |
| **False positive rate** | Negatives covered / Total negatives | 0/2 = 0 |

---

## Real Graph Mining Example: Fraud Detection

### Scenario
Learn a rule to identify **fraudulent transactions** in a payment network.

**Background facts (graph edges):**

| Fact | Meaning |
|------|---------|
| `transaction(acc1, acc2, amount)` | Payment from acc1 to acc2 |
| `shares_phone(acc1, acc2)` | Accounts share phone number |
| `shares_address(acc1, acc2)` | Accounts share address |
| `past_fraud(acc)` | Account previously fraudulent |

**Positive examples (fraud):**
- `fraud(acc5)` = true
- `fraud(acc7)` = true
- `fraud(acc12)` = true

**Negative examples (not fraud):**
- `fraud(acc2)` = false
- `fraud(acc9)` = false

### ILP Learns Rule Like:

```
fraud(A) :- 
    transaction(A, B, amount), 
    shares_phone(A, B), 
    past_fraud(B).
```

**In English:** *An account A is fraudulent if it makes a transaction to account B, they share a phone number, and B is known to be fraudulent.*

### Numerical Performance

| Rule Condition | Positives covered | Negatives covered | Score |
|----------------|-------------------|-------------------|-------|
| None (default) | 3/3 | 5/5 | Poor |
| `past_fraud(B)` only | 2/3 | 1/5 | Better |
| `past_fraud(B)` + `shares_phone(A,B)` | 3/3 | 0/5 | Perfect |

---
