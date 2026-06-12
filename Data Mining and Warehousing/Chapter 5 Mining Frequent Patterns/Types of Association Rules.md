[[simple explanation for mero confusions]]

note: Multi level bhaneko abstration matra ho 



---

## 1. Boolean Association Rule
Deals with **presence or absence** of items (binary: 0 or 1).

- **Form:** `X → Y` where X and Y are itemsets
- **Example:** `{Bread, Milk} → {Butter}`  
  (If customer buys *bread* AND *milk*, they also buy *butter*)
- **Data type:** Categorical/binary
- **Typical use:** Market basket analysis

> *This is the classic, simplest type of association rule.*

---

## 2. Quantitative Association Rule
Deals with **numeric (quantitative) attributes** that are dynamically **partitioned into intervals**.

- **Form:** `(age, 30–40) ∧ (income, 50k–70k) → (buys, luxury_car)`
- **Example:** `(Age = 30..40) ∧ (Income = High) → (Buys = SUV)`
- **Data type:** Numeric (age, income, temperature, price)
- **Challenge:** Must decide how to discretize numbers (equal width, clustering, etc.)
- **Typical use:** Customer segmentation, sensor data analysis

> *Unlike Boolean rules (binary), quantitative rules handle continuous values.*

---

## 3. Single-Dimensional Association Rule
References **a single dimension** (i.e., one predicate or attribute).

- **Dimension** = an attribute like `buys`, `visits`, `clicks`
- **Form:** `buys(X, item1) ∧ buys(X, item2) → buys(X, item3)`
- **Example:** `buys(customer, bread) ∧ buys(customer, milk) → buys(customer, eggs)`
- **Key point:** Only one dimension (`buys`) appears throughout the rule.

> *Most market basket analysis uses single-dimensional rules.*

---

## 4. Multidimensional Association Rule
References **multiple dimensions** (two or more distinct predicates/attributes).

- **Form:** `dimension1 = value1 ∧ dimension2 = value2 → dimension3 = value3`
- **Example:** `(Age = Young) ∧ (Marital = Single) → (buys = Sports_Car)`
  - Dimensions: `Age`, `Marital`, `buys`
- **Can be:** Mixed (categorical + quantitative)
- **Typical use:** Customer profiling, recommendation systems

> *Single-dimensional = same attribute repeated. Multidimensional = different attributes.*

---

## 5. Multilevel Association Rule (Hierarchical)
Rules discovered at **different levels of abstraction** using a **concept hierarchy**.

**Example hierarchy:**
```
Clothing → Outerwear → Jackets
          → Innerwear → Shirts
Electronics → Computers → Laptops
           → Mobiles → Smartphones
```

**Rules at different levels:**

| Level | Rule |
| :--- | :--- |
| **Low (specific)** | `{Leather_Jacket} → {Designer_Jeans}` |
| **Medium** | `{Jackets} → {Jeans}` |
| **High (general)** | `{Clothing} → {Denim_Products}` |

**Key concepts:**
- **Uniform support** – Same min_support for all levels
- **Reduced support** – Lower min_support for deeper levels
- **Group-based** – Roll up items to higher concepts

> *Helps find both specific and general patterns. Avoids missing rare but valid rules at lower levels.*

---

## Comparison Summary Table

| Rule Type        | Data Type   | Number of Dimensions | Key Feature                  | Example                                    |
| :--------------- | :---------- | :------------------- | :--------------------------- | :----------------------------------------- |
| **Boolean**      | Binary      | Any (1 or more)      | Presence/absence only        | `{Bread} → {Milk}`                         |
| **Quantitative** | Numeric     | Any                  | Dynamically binned numbers   | `(Age=20..30) → (Buys=Phone)`              |
| **Single-Dim**   | Categorical | 1                    | Only one predicate           | `buys(X, a) → buys(X, b)`                  |
| **Multi-Dim**    | Mixed       | ≥ 2                  | Multiple distinct attributes | `(Age=Old) ∧ (Income=Low) → (Health=High)` |
| **Multilevel**   | Categorical | Any                  | Different abstraction levels | `{Clothing} → {Footwear}`                  |

---



