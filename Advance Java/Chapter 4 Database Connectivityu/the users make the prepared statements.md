**The user (developer) creates PreparedStatements.** They are NOT predefined by Java.

---

## Short Answer

**You (the developer) create PreparedStatements by writing your own SQL with `?` placeholders.**

```java
// YOU write this SQL with placeholders
PreparedStatement pstmt = con.prepareStatement(
    "INSERT INTO users (name, age) VALUES (?, ?)"  // ← YOU write this!
);
```

---

## Who Creates What?

| Who | Creates | Example |
|-----|---------|---------|
| **Java** (predefined) | The `PreparedStatement` class itself | `java.sql.PreparedStatement` (the interface) |
| **You (developer)** | The actual SQL statement inside it | `"INSERT INTO users VALUES (?, ?)"` |

**Analogy:** Java gives you the **mold** (PreparedStatement class). You fill it with your own **shape** (your SQL).

---

## Step by Step

```java
// Step 1: Java provides the PreparedStatement CLASS (predefined)
// This is built into Java - you don't write this
public interface PreparedStatement extends Statement {
    void setString(int pos, String value);
    void setInt(int pos, int value);
    // ... other methods
}

// Step 2: YOU create an instance with YOUR SQL
PreparedStatement pstmt = con.prepareStatement(
    "SELECT * FROM students WHERE age > ?"  // ← YOUR custom SQL
);

// Step 3: YOU set YOUR values
pstmt.setInt(1, 18);  // YOUR condition

// Step 4: YOU execute
ResultSet rs = pstmt.executeQuery();  // YOUR results
```

---

## Multiple Examples (All Created by User)

```java
// Example 1: Your INSERT statement
PreparedStatement pstmt1 = con.prepareStatement(
    "INSERT INTO products (name, price) VALUES (?, ?)"
);

// Example 2: Your SELECT statement
PreparedStatement pstmt2 = con.prepareStatement(
    "SELECT * FROM employees WHERE department = ? AND salary > ?"
);

// Example 3: Your UPDATE statement
PreparedStatement pstmt3 = con.prepareStatement(
    "UPDATE students SET grade = ? WHERE id = ?"
);

// Example 4: Your DELETE statement
PreparedStatement pstmt4 = con.prepareStatement(
    "DELETE FROM logs WHERE date < ?"
);
```

**Every SQL with `?` is written by YOU!**

---

## The Golden Rule

> **Java provides the PreparedStatement CLASS. YOU provide the SQL statement with `?` placeholders. YOU create the PreparedStatement object with your custom SQL.**

**Memory trick:**
```
Java gives:        PreparedStatement (empty form)
You provide:       SQL with ? (the template)
You fill:          Values via setXxx()
You execute:       The final query

Predefined = The class itself
User-created = The actual SQL and values
```