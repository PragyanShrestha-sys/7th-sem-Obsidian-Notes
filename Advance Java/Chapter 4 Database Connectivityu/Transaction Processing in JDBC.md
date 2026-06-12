Here's a **complete explanation** of Transaction Processing in JDBC.

---

## What is Transaction Processing?

**A transaction** is a group of database operations that must execute together as a single unit - either ALL succeed or NONE take effect.

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

## Transaction Methods in JDBC

| Method | What it does |
|--------|--------------|
| `setAutoCommit(false)` | Disables auto-commit (starts transaction) |
| `commit()` | Saves all changes permanently |
| `rollback()` | Undoes all changes since last commit |
| `setSavepoint(String name)` | Creates a savepoint to rollback to |
| `releaseSavepoint(Savepoint sp)` | Removes a savepoint |
| `getAutoCommit()` | Checks if auto-commit is enabled |

---

## How Transaction is Implemented

### Step 1: Disable Auto-Commit

```java
con.setAutoCommit(false);  // Transaction starts here
```

### Step 2: Execute Multiple Operations

```java
// All these are part of one transaction
stmt.executeUpdate("INSERT INTO accounts VALUES (1, 'Alice', 1000)");
stmt.executeUpdate("INSERT INTO accounts VALUES (2, 'Bob', 500)");
stmt.executeUpdate("UPDATE accounts SET balance = balance - 200 WHERE id = 1");
stmt.executeUpdate("UPDATE accounts SET balance = balance + 200 WHERE id = 2");
```

### Step 3: Commit or Rollback

```java
// If all successful
con.commit();  // Save everything

// If error occurs
con.rollback();  // Undo everything
```

---

## Complete Example: Bank Transfer

```java
import java.sql.*;

public class TransactionDemo {
    public static void main(String[] args) {
        
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/bank", "root", "password")) {
            
            // ===== 1. Start Transaction =====
            con.setAutoCommit(false);
            System.out.println("Transaction started");
            
            try {
                // ===== 2. Execute Operations =====
                Statement stmt = con.createStatement();
                
                // Check balances
                ResultSet rs = stmt.executeQuery("SELECT balance FROM accounts WHERE id = 1");
                rs.next();
                double balance1 = rs.getDouble("balance");
                rs.close();
                
                if (balance1 < 500) {
                    throw new SQLException("Insufficient funds!");
                }
                
                // Debit from account 1
                int rows = stmt.executeUpdate("UPDATE accounts SET balance = balance - 500 WHERE id = 1");
                System.out.println("Debited 500 from Account 1");
                
                // Credit to account 2
                rows = stmt.executeUpdate("UPDATE accounts SET balance = balance + 500 WHERE id = 2");
                System.out.println("Credited 500 to Account 2");
                
                // Insert transaction record
                rows = stmt.executeUpdate("INSERT INTO transactions (from_id, to_id, amount) VALUES (1, 2, 500)");
                System.out.println("Transaction recorded");
                
                // ===== 3. Commit if all successful =====
                con.commit();
                System.out.println("\n✅ Transaction COMMITTED successfully!");
                System.out.println("Money transferred!");
                
            } catch (SQLException e) {
                // ===== 4. Rollback if any error =====
                con.rollback();
                System.out.println("\n❌ Transaction ROLLED BACK!");
                System.out.println("Error: " + e.getMessage());
                System.out.println("No changes were made to the database.");
            }
            
        } catch (SQLException e) {
            System.out.println("Connection error: " + e.getMessage());
        }
    }
}
```

---
## [[Real-World Example Order Processing]]

---

## [[Savepoints (Partial Rollback)]]

---

## Transaction Methods Summary

| Method | Description | When to use |
|--------|-------------|-------------|
| `setAutoCommit(false)` | Disables auto-commit | Start of transaction |
| `commit()` | Saves all changes | After all operations succeed |
| `rollback()` | Undoes all changes | After any operation fails |
| `rollback(Savepoint sp)` | Undoes to savepoint | Partial rollback |
| `setSavepoint(String name)` | Creates checkpoint | Before critical operation |
| `releaseSavepoint(Savepoint sp)` | Removes savepoint | After savepoint not needed |
| `getAutoCommit()` | Checks auto-commit status | Debugging |

---

## Transaction Flow Diagram

```
                    setAutoCommit(false)
                           │
                           ▼
              ┌────────────────────────┐
              │   Transaction Starts    │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │   Operation 1 (INSERT)  │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │   Operation 2 (UPDATE)  │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │   Operation 3 (DELETE)  │
              └────────────┬───────────┘
                           │
              ┌────────────┴────────────┐
              │                         │
              ▼                         ▼
      All Success?                    Any Error?
              │                         │
              ▼                         ▼
         commit()                   rollback()
              │                         │
              ▼                         ▼
    Changes Saved ✓            All Changes Undone ✗
```

---

## [[Auto-Commit vs Transaction]]
| Aspect                  | Auto-Commit ON         | Auto-Commit OFF             |
| ----------------------- | ---------------------- | --------------------------- |
| **Default**             | Yes (default)          | No (must set manually)      |
| **Each SQL**            | Immediate commit       | Added to transaction        |
| **Rollback**            | Not possible           | Possible                    |
| **Multiple operations** | Independent            | Together as unit            |
| **Use case**            | Simple, single queries | Multiple related operations |

## [[Batch Update with Transaction]]

## Transaction Isolation Levels

| Level | Prevents Dirty Read | Prevents Non-Repeatable Read | Prevents Phantom Read |
|-------|--------------------|----------------------------|---------------------|
| `TRANSACTION_READ_UNCOMMITTED` | ❌ No | ❌ No | ❌ No |
| `TRANSACTION_READ_COMMITTED` | ✅ Yes | ❌ No | ❌ No |
| `TRANSACTION_REPEATABLE_READ` | ✅ Yes | ✅ Yes | ❌ No |
| `TRANSACTION_SERIALIZABLE` | ✅ Yes | ✅ Yes | ✅ Yes |

```java
// Set isolation level
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);
```

## [[Common Transaction Patterns]]


## Quick Reference

| Method | Purpose |
|--------|---------|
| `setAutoCommit(false)` | Start transaction |
| `commit()` | Save changes |
| `rollback()` | Undo changes |
| `setSavepoint("name")` | Create checkpoint |
| `rollback(sp)` | Undo to checkpoint |

---

## The Golden Rule

> **A transaction groups multiple database operations into a single unit. Use `setAutoCommit(false)` to start, `commit()` on success, `rollback()` on failure. This ensures data consistency - all changes save or none do.**

**Memory trick:**
```
AutoCommit ON = Each operation stands alone
AutoCommit OFF = Multiple operations as one team

setAutoCommit(false) = "Prepare for teamwork"
commit() = "Team succeeded - save everything"
rollback() = "Team failed - undo everything"

"All or nothing" = Transaction
```