
An **attribute** (also called a feature, variable, or field) is a property or characteristic of a data object.

Attributes are classified into **3 main types**, plus a special fourth type:

### 1. Nominal Attributes (Categorical - No Order)

- **Definition:** Labels or names only. No mathematical meaning. Cannot be compared as "greater than" or "less than."
- **Operations allowed:** Equality (= , ≠)
- **Examples:**
  - Eye color (Brown, Blue, Green)
  - Gender (Male, Female)
  - Student ID (101, 102, 103) — these are just labels, not numbers

### 2. Ordinal Attributes (Categorical - With Order)

- **Definition:** Categories that have a meaningful order or ranking, but the exact difference between values is unknown.
- **Operations allowed:** Equality and comparison (< , >)
- **Examples:**
  - Customer satisfaction (Low, Medium, High)
  - Grades (A, B, C, D, F)
  - Military rank (Private, Sergeant, Lieutenant)

### 3. Numeric Attributes (Quantitative)

Numeric attributes are further divided into two sub-types:

| Sub-type     | Definition                               | Operations    | Example                                                                                                                                                                              |
| :----------- | :--------------------------------------- | :------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Interval** | No true zero. Ratios not meaningful.     | + , -         | - Numeric data with **equal, measurable gaps** between values, but **NO true zero point** (zero is just a position on the scale, meaning the absence of the property doesn't exist). |
| **Ratio**    | True zero exists. Ratios are meaningful. | + , - , × , ÷ | Numeric data with **equal gaps AND a true, meaningful zero** (where zero means "none" of that thing exists).                                                                         |

### 4. Binary Attributes (Special Case of Nominal)

- **Definition:** Only two possible values.
- **Examples:**
  - Yes / No
  - True / False
  - 0 / 1
  - Smoker / Non-smoker

---

## Quick Comparison Table

| Attribute Type | Order? | Arithmetic?   | Examples                         |
| :------------- | :----- | :------------ | :------------------------------- |
| **Nominal**    | No     | No            | ID numbers, colors, gender       |
| **Ordinal**    | Yes    | No            | Grades, rankings, sizes (S/M/L)  |
| **Interval**   | Yes    | + , -         | Temperature (°C), calendar years |
| **Ratio**      | Yes    | + , - , × , ÷ | Age, income, weight, height      |

---

## Why Does Attribute Type Matter?

The attribute type determines:

1.  **Which operations are allowed** (You cannot calculate "average" eye color — that makes no sense!)
2.  **Which similarity/distance measures to use** (Euclidean distance works for numeric, not for nominal)
3.  **Which data mining algorithms apply** (Decision trees handle all types; linear regression needs numeric)

### Example of Incorrect Use:

| Wrong | Why? |
| :--- | :--- |
| Average of zip codes | Zip codes are nominal labels, not numeric values |
| Gender1 > Gender2 | Gender is nominal, no ordering allowed |
| "Twice as hot" in °C | Celsius is interval, no true zero (0°C doesn't mean no heat) |
