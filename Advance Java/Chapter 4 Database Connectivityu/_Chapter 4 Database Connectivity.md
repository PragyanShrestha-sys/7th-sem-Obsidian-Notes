## [[JDBC Architecture (imp)]]

what is jdbc?
just and intermediatray between the userinterface and the database

| Role              | Analogy                                                     |
| ----------------- | ----------------------------------------------------------- |
| **Your Java App** | Customer (wants to talk to database)                        |
| **JDBC**          | Translator/Interpreter (converts Java to database language) |
| **Database**      | Foreigner (speaks its own SQL language)                     |

```
Customer (Java App) → Translator (JDBC) → Foreigner (Database)
                         ↑
                    Translates both ways!

```

---
## [[JDBC Driver Types]]

![[Pasted image 20260606102750.png]]

![[Pasted image 20260606102813.png]]

---

## [[Setting up database connection]]


---
## [[Statement, ResultSet & Query Execution]]

**"Statement contains execute query and ResultSet is used to retrieve data"**

> **"Statement is an object that holds the query"** ✅ **CORRECT**

> **"Execute are the methods inside statement"** ✅ **CORRECT**

---
## [[Sql Exception]]
![[Pasted image 20260606152002.png]]

---
## [[DDL (Data Defination Language) and DML (Data Manipulation Language)]]

**DDL** = **Data Definition Language** (Defines the structure of database)

**DML** = **Data Manipulation Language** (Manipulates the data inside tables)

```
DATABASE
    │
    ├── DDL (Structure) ──→ CREATE, ALTER, DROP, TRUNCATE, RENAME
    │                       (Creates tables, changes columns, deletes tables)
    │
    └── DML (Data) ──────→ SELECT, INSERT, UPDATE, DELETE
                            (Adds data, changes data, removes data)
```

---
## [[Prepared Statements]]

![[Pasted image 20260606153913.png]]
![[Pasted image 20260606153921.png]]

---
## [[Transaction Processing in JDBC]]

 transaction** is a group of database operations that must execute together as a single unit - either ALL succeed or NONE take effect.

```
Without Transaction:              With Transaction:
INSERT record 1 ✓                INSERT record 1 ✓
INSERT record 2 ✗ (error)        INSERT record 2 ✗ (error)
Result: Record 1 saved (bad!)    Result: ALL rolled back (good!)
```

**Analogy:** Transferring money between bank accounts. If debit succeeds but credit fails, you need to roll back. Transaction ensures both happen or neither happens.

---

## Why is Transaction Needed?

| Problem | Without Transaction | With Transaction |
|---------|--------------------|--------------------|
| **Bank transfer** | Money deducted but not added | Both or neither |
| **Order processing** | Order saved but inventory not updated | Complete or nothing |
| **Student registration** | Student added but course full | All or rollback |
| **Bulk insert** | Partial data after error | All or nothing |

**ACID Properties:**

| Property | Meaning |
|----------|---------|
| **Atomicity** | All or nothing |
| **Consistency** | Database remains valid |
| **Isolation** | Transactions don't interfere |
| **Durability** | Committed changes persist |

---
## [[RowSet Interface and Types]]


---

## Note:

![[Pasted image 20260606155130.png]]