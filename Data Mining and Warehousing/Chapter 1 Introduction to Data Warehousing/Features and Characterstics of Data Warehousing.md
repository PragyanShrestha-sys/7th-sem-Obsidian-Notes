Here’s a clear explanation of the **four key traits of a data warehouse** (often called the basic characteristics from Bill Inmon, the "father of data warehousing"):

---

## 1. Subject-Oriented

**Meaning:** Data is organized around **major business subjects** (customers, products, sales, inventory), not around specific applications or transactions.

| Operational DB (Application-Oriented) | Data Warehouse (Subject-Oriented) |
|----------------------------------------|------------------------------------|
| Organized by processes (order entry, invoicing, inventory updates) | Organized by subjects (customers, products, sales) |
| Optimized for fast individual transactions | Optimized for analysis across a subject |

**Example:** Instead of separate tables for "web orders," "store orders," and "call center orders," the warehouse has a single **"Sales"** subject that combines all order types.

---

## 2. Integrated

**Meaning:** Data from **multiple, disparate sources** is cleaned, transformed, and made **consistent** in naming, formats, units, and codes.

**Problems solved:**

| Inconsistent Source Data                 | After Integration                              |
| ---------------------------------------- | ---------------------------------------------- |
| M = Male, Male = 1, male = M             | All become "M"                                 |
| Date: DD/MM/YY vs MM/DD/YYYY             | All become YYYY-MM-DD                          |
| Currency: USD, EUR, GBP                  | All converted to a single currency (e.g., USD) |
| Customer ID: 123 in CRM, CUST-123 in ERP | Standardized ID format                         |

**Result:** A **single version of the truth** – everyone answers the same way when asked, "How many customers do we have?"

---

## 3. Time-Variant

**Meaning:** The warehouse stores **historical data** over long periods (years), with timestamps, to track changes and trends over time.

| Operational System | Data Warehouse |
|--------------------|----------------|
| Stores current state only (e.g., current customer address) | Stores address history with effective dates |
| Often overwrites or deletes old data | Never overwrites – adds new rows with timestamps |
| Typical retention: days or weeks | Typical retention: years or decades |

**Example:** You can run a query like, *"What was Customer X's address on Jan 1, 2020?"* – impossible in most operational systems, easy in a warehouse.

---

## 4. Non-Volatile

**Meaning:** Once data is loaded into the warehouse, it is **read-only** – no updates, deletes, or frequent changes.

| Volatile (Operational DB) | Non-Volatile (Data Warehouse) |
|---------------------------|-------------------------------|
| INSERT, UPDATE, DELETE frequently | INSERT only (batch loads) |
| Data changes constantly (e.g., inventory count) | Data is static and historical |
| Optimized for write operations | Optimized for read/query operations |

**Key Operations:**
- **Load** – Bulk insert new data (e.g., nightly ETL)
- **Query** – SELECT statements for reporting/analytics
- **No** direct UPDATE or DELETE of historical records

**Benefit:** Predictable, stable, fast query performance – no locks or competing writes.

---

## Summary Table

| Trait                | In One Sentence                    | Operational DB (Opposite)               |
| -------------------- | ---------------------------------- | --------------------------------------- |
| **Subject-Oriented** | Organized around business subjects | Organized around applications/processes |
| **Integrated**       | Consistent formats and definitions | Inconsistent across sources             |
| **Time-Variant**     | Stores history with timestamps     | Stores only current state               |
| **Non-Volatile**     | Read-only after load               | Frequent updates and deletes            |

---

## Memory Aid (First Letters)

**S**ubject-oriented  
**I**ntegrated  
**T**ime-variant  
**N**on-volatile

> **SIT N** – "Data *sits in* the warehouse, stable and historical."