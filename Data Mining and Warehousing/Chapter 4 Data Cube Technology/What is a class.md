## What "Class" Means in Data Mining

In data mining, a **class** is simply **a group or category of data that shares a common characteristic you care about**.
### Simple Definition

> A **class** = A set of data instances that belong to the same category or label.

### Everyday Examples

| Domain | Different Classes |
|--------|------------------|
| Email | "Spam" class vs. "Not Spam" class |
| Banking | "Fraud" class vs. "Legitimate" class |
| Medical | "Has disease" class vs. "Healthy" class |
| Marketing | "Churned customer" class vs. "Loyal customer" class |
| Loans | "Defaulter" class vs. "Payer" class |
| Retail | "High value" class vs. "Low value" customer |

### Visual Representation

```
                    ALL CUSTOMERS
                          │
            ┌─────────────┼─────────────┐
            ▼             ▼             ▼
        Class A        Class B        Class C
      "Churned"       "Loyal"      "New"
         │              │             │
    25,000 rows     60,000 rows    15,000 rows
```

### In the Context of AOI and Class Comparison

| Technique | How "Class" is Used |
|-----------|--------------------|
| **Characterization (AOI)** | Describes ONE class: "What do churned customers look like?" |
| **Discrimination (Class Comparison)** | Compares TWO+ classes: "How are churned customers DIFFERENT from loyal ones?" |

### Key Point

> You (the analyst) **define what the classes are** based on your business question. The data mining technique then discovers patterns within or between those classes.

**Example:** If you ask "Describe fraudulent transactions" — YOU have defined:
- **Target class** = Fraud (all transactions marked as fraud)
- The algorithm just summarizes what those rows have in common