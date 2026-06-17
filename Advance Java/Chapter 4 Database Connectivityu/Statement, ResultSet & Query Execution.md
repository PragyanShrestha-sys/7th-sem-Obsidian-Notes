Here's a **complete explanation** of Statement, ResultSet, and Query Execution in JDBC.

---

## The Big Picture

Once you have a database **Connection**, you need three things to work with data:

```
Connection (phone line to database)
     ↓
Statement (your voice - what you say)
     ↓
ResultSet (the reply you hear back)
```

| Component | What it does | Analogy |
|-----------|--------------|---------|
| **Statement** | Sends SQL query to database | Your voice/mouth |
| **Query Execution** | Database processes the SQL | Database's ears listening |
| **ResultSet** | Holds the data returned | Database's reply/answer |

---

## [[What is a Statement]]

**A Statement** is an object that sends SQL queries to the database for execution.

```java
Statement stmt = con.createStatement();
```

---

## What is Query Execution?

**Query Execution** is the process of sending SQL to the database and having it run.

```java
// Two main methods for execution
ResultSet rs = stmt.executeQuery("SELECT * FROM users");  // For SELECT
int count = stmt.executeUpdate("DELETE FROM users WHERE id=1");  // For INSERT/UPDATE/DELETE
```

### Execution Methods

| Method                      | What it does                  | When to use        | Returns           |
| --------------------------- | ----------------------------- | ------------------ | ----------------- |
| `executeQuery(String sql)`  | Executes SELECT query         | Reading data       | `ResultSet`       |
| `executeUpdate(String sql)` | Executes INSERT/UPDATE/DELETE | Changing data      | `int` (row count) |
| `execute(String sql)`       | Executes any SQL              | Unknown query type | `boolean`         |

---

## What is [[ResultSet]]?

**A ResultSet** is an object that holds the data returned from a SELECT query.

```java
ResultSet rs = stmt.executeQuery("SELECT * FROM students");
```

---

## Complete Flow Diagram

```
                    DATABASE
                        ↑
                        │ (executes SQL)
                        │
    ┌───────────────────┴───────────────────┐
    │                                       │
    │  Statement sends SQL                  │
    │                                       │
┌───┴───┐                               ┌───┴───┐
│Statement│ ──────────────────────────→ │Database│
└───┬───┘                               └───┬───┘
    │                                       │
    │                                       │ (returns)
    │                                       │
    │                                   ┌───┴───┐
    │                                   │ResultSet│
    │                                   └───┬───┘
    │                                       │
    └───────────────────────────────────────┘
                    │
              Your Java App
```

---

## Complete Code Example

```java
import java.sql.*;

public class StatementResultSetDemo {
    public static void main(String[] args) {
        
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password")) {
            
            // ========== 1. CREATE STATEMENT ==========
            Statement stmt = con.createStatement();
            
            // ========== 2. EXECUTE QUERY (SELECT) ==========
            System.out.println("=== SELECT Query ===");
            ResultSet rs = stmt.executeQuery("SELECT id, name, age FROM students");
            
            // ========== 3. PROCESS RESULTSET ==========
            //**`rs.next()` moves the cursor forward one row at a time, from first to last.**
            while (rs.next()) {
                int id = rs.getInt("id");           // Get by column name
                String name = rs.getString("name");
                int age = rs.getInt("age");
                
                System.out.println("ID: " + id + ", Name: " + name + ", Age: " + age);
            }
            
            // ========== 4. EXECUTE UPDATE (INSERT) ==========
            System.out.println("\n=== INSERT Query ===");
            int rowsInserted = stmt.executeUpdate(
                "INSERT INTO students (name, age) VALUES ('David', 22)"
            );
            System.out.println(rowsInserted + " row(s) inserted");
            
            // ========== 5. EXECUTE UPDATE (UPDATE) ==========
            System.out.println("\n=== UPDATE Query ===");
            int rowsUpdated = stmt.executeUpdate(
                "UPDATE students SET age = 23 WHERE name = 'David'"
            );
            System.out.println(rowsUpdated + " row(s) updated");
            
            // ========== 6. EXECUTE UPDATE (DELETE) ==========
            System.out.println("\n=== DELETE Query ===");
            int rowsDeleted = stmt.executeUpdate(
                "DELETE FROM students WHERE name = 'David'"
            );
            System.out.println(rowsDeleted + " row(s) deleted");
            
            rs.close();
            stmt.close();
            
        } catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## ResultSet Navigation Methods

| Method | What it does |
|--------|--------------|
| `next()` | Moves cursor to next row (returns true if exists) |
| `previous()` | Moves to previous row |
| `first()` | Moves to first row |
| `last()` | Moves to last row |
| `absolute(int row)` | Moves to specific row number |
| `beforeFirst()` | Moves before first row |
| `afterLast()` | Moves after last row |
| `isFirst()` | Checks if current row is first |
| `isLast()` | Checks if current row is last |

### Example: Navigating ResultSet

```java
ResultSet rs = stmt.executeQuery("SELECT * FROM students");

// Move to first row
rs.first();
System.out.println("First: " + rs.getString("name"));

// Move to last row
rs.last();
System.out.println("Last: " + rs.getString("name"));

// Move to row 3
rs.absolute(3);
System.out.println("Row 3: " + rs.getString("name"));

// Loop backward
rs.afterLast();
while (rs.previous()) {
    System.out.println(rs.getString("name"));
}
```

---

## ResultSet Get Methods (by Type)

| SQL Type | Java Get Method |
|----------|-----------------|
| `INT` | `getInt(String columnName)` |
| `VARCHAR` (String) | `getString(String columnName)` |
| `DOUBLE` | `getDouble(String columnName)` |
| `DATE` | `getDate(String columnName)` |
| `TIMESTAMP` | `getTimestamp(String columnName)` |
| `BOOLEAN` | `getBoolean(String columnName)` |
| `BLOB` (binary) | `getBlob(String columnName)` |

### Two Ways to Get Data

```java
// Method 1: By column name (readable, preferred)
String name = rs.getString("name");

// Method 2: By column index (faster but fragile)
String name = rs.getString(2);  // 2nd column

// Index starts at 1 (not 0!)
```

---

## executeUpdate() Return Value

```java
// INSERT returns number of rows inserted
int inserted = stmt.executeUpdate("INSERT INTO users (name) VALUES ('Alice')");
// inserted = 1

// UPDATE returns number of rows updated
int updated = stmt.executeUpdate("UPDATE users SET name='Bob' WHERE id=1");
// updated = 1

// DELETE returns number of rows deleted
int deleted = stmt.executeUpdate("DELETE FROM users WHERE id=999");
// deleted = 0 (no matching rows)
```

---

## Statement vs PreparedStatement

| Feature | Statement | PreparedStatement |
|---------|-----------|-------------------|
| **SQL injection risk** | High | Low (prevented) |
| **Performance** | Slower for repeated execution | Faster for repeated execution |
| **Parameters** | Must concatenate strings | Uses ? placeholders |
| **Precompiled** | No | Yes |
| **Security** | Less secure | More secure |
| **Use when** | Single execution, simple queries | Repeated execution, user input |

### Example: Statement (Vulnerable to SQL Injection)

```java
String userInput = "1 OR 1=1";
String sql = "SELECT * FROM users WHERE id = " + userInput;
// Becomes: SELECT * FROM users WHERE id = 1 OR 1=1 (returns ALL users!)
ResultSet rs = stmt.executeQuery(sql);
```

### Example: PreparedStatement (Safe)

```java
String sql = "SELECT * FROM users WHERE id = ?";
PreparedStatement pstmt = con.prepareStatement(sql);
pstmt.setInt(1, userId);  // Safe! Input treated as data, not SQL
ResultSet rs = pstmt.executeQuery();  // No parameter here
```

---

## Complete Example: CRUD Operations

```java
import java.sql.*;

public class CRUDDemo {
    private Connection con;
    
    public CRUDDemo() throws SQLException {
        con = DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/mydb", "root", "password");
    }
    
    // CREATE (INSERT)
    public void createUser(String name, int age) throws SQLException {
        Statement stmt = con.createStatement();
        String sql = "INSERT INTO users (name, age) VALUES ('" + name + "', " + age + ")";
        int rows = stmt.executeUpdate(sql);
        System.out.println(rows + " user(s) created");
        stmt.close();
    }
    
    // READ (SELECT)
    public void readUsers() throws SQLException {
        Statement stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM users");
        
        while (rs.next()) {
            System.out.println("ID: " + rs.getInt("id") + 
                             ", Name: " + rs.getString("name") + 
                             ", Age: " + rs.getInt("age"));
        }
        rs.close();
        stmt.close();
    }
    
    // UPDATE
    public void updateUser(int id, String newName) throws SQLException {
        Statement stmt = con.createStatement();
        String sql = "UPDATE users SET name = '" + newName + "' WHERE id = " + id;
        int rows = stmt.executeUpdate(sql);
        System.out.println(rows + " user(s) updated");
        stmt.close();
    }
    
    // DELETE
    public void deleteUser(int id) throws SQLException {
        Statement stmt = con.createStatement();
        String sql = "DELETE FROM users WHERE id = " + id;
        int rows = stmt.executeUpdate(sql);
        System.out.println(rows + " user(s) deleted");
        stmt.close();
    }
    
    public void close() throws SQLException {
        con.close();
    }
    
    public static void main(String[] args) {
        try {
            CRUDDemo demo = new CRUDDemo();
            demo.createUser("Alice", 25);
            demo.readUsers();
            demo.updateUser(1, "Alicia");
            demo.deleteUser(1);
            demo.close();
        } catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## Summary Table

| Component | What it is | Why needed | How to create |
|-----------|-----------|-----------|---------------|
| **Statement** | SQL sender | To execute queries | `con.createStatement()` |
| **executeQuery()** | SELECT execution | To read data | `stmt.executeQuery(sql)` |
| **executeUpdate()** | INSERT/UPDATE/DELETE | To modify data | `stmt.executeUpdate(sql)` |
| **ResultSet** | Data container | To access query results | Returned from executeQuery() |
| **next()** | Row pointer | To iterate through rows | `rs.next()` |
| **getXxx()** | Column access | To get column values | `rs.getString("name")` |

---

## The Golden Rule

> **Statement sends SQL to database, executeQuery() runs SELECT and returns ResultSet, executeUpdate() runs INSERT/UPDATE/DELETE and returns row count. ResultSet holds the returned data; use next() to move through rows and getXxx() to retrieve column values.**

**Memory trick:**
```
Statement = "I speak SQL"
executeQuery = "I ask questions" (SELECT → gets ResultSet)
executeUpdate = "I make changes" (INSERT/UPDATE/DELETE → gets row count)
ResultSet = "I hold answers"
next() = "Next answer please"
getString() = "Give me the text"
```

Would you like me to explain **PreparedStatement** (to prevent SQL injection) or **Transaction Management** next?