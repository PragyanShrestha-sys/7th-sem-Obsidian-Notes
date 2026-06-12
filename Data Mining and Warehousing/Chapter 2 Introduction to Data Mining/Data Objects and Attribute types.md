## Data Objects

A **data object** (also called a record, instance, sample, or entity) is a single unit of information that we want to analyze.

Think of a spreadsheet or database table:
- **Each row** is a data object.
- **Each column** is an attribute.
### Examples of Data Objects:

| Domain | Data Object | Attributes |
| :--- | :--- | :--- |
| Customer database | A specific customer (e.g., John Doe) | Age, Income, City, Purchase History |
| Medical records | A patient | Blood pressure, Temperature, Diagnosis |
| Sales transaction | A single purchase receipt | Date, Items bought, Total amount |
| Student records | One student | Name, GPA, Major, Year |

### Terminology Note:
- **Database row** = Data object
- **Spreadsheet row** = Data object
- **Data mining term** = "Object" or "Instance"

---

## [[Attribute Types]]
An **attribute** (also called a feature, variable, or field) is a property or characteristic of a data object.

| Attribute Type | Order? | Arithmetic?   | Examples                         |
| :------------- | :----- | :------------ | :------------------------------- |
| **Nominal**    | No     | No            | ID numbers, colors, gender       |
| **Ordinal**    | Yes    | No            | Grades, rankings, sizes (S/M/L)  |
| **Interval**   | Yes    | + , -         | Temperature (°C), calendar years |
| **Ratio**      | Yes    | + , - , × , ÷ | Age, income, weight, height      |

---
## Summary (Memory Aid)

| Attribute | Key phrase | Example |
| :--- | :--- | :--- |
| **Nominal** | "Name only" | Color = Red |
| **Ordinal** | "Order, no difference" | Rank = 1st, 2nd, 3rd |
| **Interval** | "Difference matters, ratio doesn't" | Temp 20°C vs 40°C |
| **Ratio** | "True zero, ratios matter" | Weight 20kg vs 40kg |

**In one sentence:** *Data objects are the rows (individual items you study), and attributes are the columns (their properties), which come in nominal (names), ordinal (ordered categories), interval (differences), and ratio (true zero) types.*