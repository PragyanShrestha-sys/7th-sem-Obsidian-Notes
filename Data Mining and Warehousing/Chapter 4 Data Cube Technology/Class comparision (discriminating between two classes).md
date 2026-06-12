## Mining Class Comparison (Discrimination) - Explained

### What Is It?

**Class comparison / discrimination** is a data mining technique that answers the question: **"What makes Class A DIFFERENT from Class B?"**

While characterization (AOI) describes *one class*, discrimination **contrasts two or more classes** to highlight what is unique or distinctive about each.

### Simple Example First

| Question | Characterization (AOI) | Discrimination (Class Comparison) |
|----------|----------------------|-----------------------------------|
| "Describe fraud transactions" | "Fraud happens late night, high amount" | — |
| "How is fraud different from normal transactions?" | — | "Fraud = late night, high amount, new device. Normal = daytime, low amount, trusted device." |

### Concrete Illustration

**Scenario:** An e-commerce company wants to understand customer behavior.

**Class A:** Customers who churned (left)  
**Class B:** Customers who stayed

| Attribute | Churned Customers (Class A) | Stayed Customers (Class B) | Discriminating Feature |
|-----------|---------------------------|---------------------------|------------------------|
| Avg support tickets | **5.2** | 0.8 | High tickets → Churn |
| Subscription type | Mostly monthly | Mostly yearly | Yearly → Stay |
| Usage frequency | Low (<5x/month) | High (>20x/month) | Low usage → Churn |
| Age group | 18-25 | 35-50 | Young → Churn |

**The discrimination rule discovered:**
> *"Customers who churn are typically young (18-25), use monthly plans, log in less than 5 times per month, and file multiple support tickets."*

---

### What Is It Used For? (Real-World Applications)

| Domain | Use Case | Question Answered |
|--------|----------|-------------------|
| **Banking** | Loan default prediction | "How do defaulters differ from non-defaulters?" |
| **Healthcare** | Treatment response | "What distinguishes responders from non-responders?" |
| **Marketing** | Customer retention | "Why do loyal customers differ from one-time buyers?" |
| **Fraud detection** | Anomaly identification | "How do fraud patterns differ from legitimate patterns?" |
| **Manufacturing** | Quality control | "What makes defective products different from good ones?" |
| **HR** | Employee turnover | "How do leavers differ from stayers?" |

---

### General Explanation (Technical)

#### Definition
**Mining class comparison** (also called **discriminant rule mining** or **contrast mining**) is the process of extracting distinguishing features or rules that separate one target class from contrasting classes.

#### How It Works

```
                    Input: Two or more classes
                              │
                              ▼
┌─────────────────────────────────────────────────────┐
│  Class A (Target)        Class B (Contrasting)      │
│  - Fraud transactions    - Normal transactions       │
│  - Churned customers     - Loyal customers           │
│  - Responders to drug    - Non-responders            │
└─────────────────────────────────────────────────────┘
                              │
                              ▼
                    Compare attribute patterns
                              │
                              ▼
┌─────────────────────────────────────────────────────┐
│  Discriminating Rules Discovered:                   │
│                                                     │
│  "Class A has Property X, Class B does NOT"         │
│  "Class A has Value Y, Class B has Value Z"         │
└─────────────────────────────────────────────────────┘
```

#### Key Output Format: Discriminant Rules

**Rule template:** *"Class A has [description] whereas Class B has [different description]"*

**Example rules:**
- IF time BETWEEN 1AM-4AM AND amount > $500 THEN Fraud (80% of cases) vs. Normal (2% of cases)
- IF subscription = monthly AND usage < 5x/month THEN Churn (75%) vs. Loyal (5%)

#### Comparison Metrics Used

| Metric | What It Means |
|--------|---------------|
| **Discriminance power** | How well an attribute separates classes |
| **Prevalence ratio** | % in Class A ÷ % in Class B |
| **Mutual information** | Statistical dependency between attribute and class |

---

### Summary Table: Characterization vs. Discrimination

| Aspect | Characterization (AOI) | Discrimination (Class Comparison) |
|--------|----------------------|-----------------------------------|
| **Number of classes** | One target class | Two or more classes |
| **Question answered** | "What does Class A look like?" | "How do Class A and B differ?" |
| **Output** | General description | Contrast rules / distinguishing features |
| **Analogy** | Drawing a portrait | Drawing a side-by-side comparison |
| **Key phrase** | "Typically has..." | "Has X, unlike Y which has Z..." |

---

### Bottom Line

> **Class comparison mining tells you what makes one group SPECIAL or DIFFERENT compared to another group.** It's not just describing — it's **contrasting** to find the unique signature of each class.

Without discrimination mining, you might know what fraud looks like, but you wouldn't know what makes fraud *different* from normal transactions. That difference is often more valuable for building detection systems.

---
## [[What is a class]]

