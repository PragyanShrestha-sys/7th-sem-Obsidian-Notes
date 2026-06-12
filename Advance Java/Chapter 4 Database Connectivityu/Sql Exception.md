Here's a **complete explanation** of SQL Exceptions in JDBC.

---

## What are SQL Exceptions?

**SQLException** is an exception class in Java that represents errors that occur while interacting with a database.

```java
public class SQLException extends java.lang.Exception {
    // Handles all database-related errors
}
```

**Analogy:** Like a "Check Engine" light in a car - tells you something went wrong with the database operation.

---

## Why are SQL Exceptions Needed?

| Problem | Without SQLException | With SQLException |
|---------|---------------------|-------------------|
| Database connection fails | Program crashes | Graceful error message |
| SQL syntax error | No feedback | Tells you exact error |
| Duplicate data entry | Wrong data state | Shows constraint violation |
| Table doesn't exist | Confusing errors | Clear "table not found" |
| Network timeout | Program hangs | Catches and handles |

**Simply put:** Database operations can fail. SQLException helps you handle those failures gracefully.

---

## Common Causes of SQLException

| Cause | Example |
|-------|---------|
| **Connection issues** | Database server down, wrong URL |
| **Authentication failure** | Wrong username/password |
| **SQL syntax error** | `SELCT * FROM users` (typo) |
| **Constraint violation** | Duplicate primary key, foreign key error |
| **Table not found** | `SELECT * FROM wrong_table` |
| **Data type mismatch** | Inserting text into number column |
| **Deadlock** | Two transactions waiting on each other |
| **Timeout** | Query takes too long |

---

## SQLException Hierarchy

```
java.lang.Object
    ↑
java.lang.Throwable
    ↑
java.lang.Exception
    ↑
java.sql.SQLException
    ↑
    ├── SQLWarning (non-fatal warning)
    ├── SQLDataException (data-related issues)
    ├── SQLIntegrityConstraintViolationException (duplicate key, foreign key)
    ├── SQLSyntaxErrorException (SQL syntax error)
    ├── SQLNonTransientConnectionException (connection failed)
    ├── SQLTimeoutException (query timed out)
    └── SQLTransactionRollbackException (transaction failed)
```
note above are the classes in the inside the lava.sql.SQLException

---

## SQLException Methods

| Method | What it returns | Example Output |
|--------|-----------------|----------------|
| `getMessage()` | Error description | "Table 'mydb.users' doesn't exist" |
| `getErrorCode()` | Database-specific error code | 1146 (MySQL table not found) |
| `getSQLState()` | Standard SQL state code | "42S02" (table not found) |
| `getNextException()` | Next exception in chain | For multiple errors |
| `printStackTrace()` | Full error trace | Complete error log |

---

## Basic Implementation

```java
import java.sql.*;

public class SQLExceptionDemo {
    public static void main(String[] args) {
        
        Connection con = null;
        Statement stmt = null;
        ResultSet rs = null;
        
        try {
            con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb",
                "root",
                "wrongpassword"  // Wrong password
            );
            
            stmt = con.createStatement();
            rs = stmt.executeQuery("SELECT * FROM users");
            
        } catch (SQLException e) {
            // Handle the exception
            System.out.println("SQL Error Occurred!");
            System.out.println("Message: " + e.getMessage());
            System.out.println("Error Code: " + e.getErrorCode());
            System.out.println("SQL State: " + e.getSQLState());
            e.printStackTrace();
            
        } finally {
            try {
                if (rs != null) rs.close();
                if (stmt != null) stmt.close();
                if (con != null) con.close();
            } catch (SQLException e) {
                System.out.println("Error closing: " + e.getMessage());
            }
        }
    }
}
```

**Output:**
```
SQL Error Occurred!
Message: Access denied for user 'root'@'localhost' (using password: YES)
Error Code: 1045
SQL State: 28000
```

---

## Handling Different Types of SQL Exceptions

```java
import java.sql.*;

public class SpecificSQLExceptionDemo {
    public static void main(String[] args) {
        
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password")) {
            
            Statement stmt = con.createStatement();
            
            // This will cause an error (table doesn't exist)
            ResultSet rs = stmt.executeQuery("SELECT * FROM non_existent_table");
            
        } catch (SQLSyntaxErrorException e) {
            System.out.println("SYNTAX ERROR: Check your SQL!");
            System.out.println("Details: " + e.getMessage());
            
        } catch (SQLIntegrityConstraintViolationException e) {
            System.out.println("CONSTRAINT ERROR: Duplicate or invalid data");
            System.out.println("Details: " + e.getMessage());
            
        } catch (SQLNonTransientConnectionException e) {
            System.out.println("CONNECTION ERROR: Cannot connect to database");
            System.out.println("Check: URL, username, password, database server");
            
        } catch (SQLTimeoutException e) {
            System.out.println("TIMEOUT ERROR: Query took too long");
            
        } catch (SQLException e) {
            System.out.println("GENERAL SQL ERROR: " + e.getMessage());
            System.out.println("Error Code: " + e.getErrorCode());
            System.out.println("SQL State: " + e.getSQLState());
        }
    }
}
```

---

## Complete Example: Robust Error Handling

```java
import java.sql.*;

public class RobustDatabaseHandler {
    
    public static void main(String[] args) {
        
        Connection con = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        
        try {
            // Attempt connection
            con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/school",
                "root",
                "password"
            );
            System.out.println("Connected successfully!");
            
            // Attempt query
            String sql = "SELECT id, name, age FROM students WHERE age > ?";
            pstmt = con.prepareStatement(sql);
            pstmt.setInt(1, 18);
            rs = pstmt.executeQuery();
            
            // Process results
            while (rs.next()) {
                System.out.println(rs.getInt("id") + ": " + 
                                   rs.getString("name") + ", " + 
                                   rs.getInt("age"));
            }
            
        } catch (SQLNonTransientConnectionException e) {
            System.err.println("FATAL: Cannot connect to database!");
            System.err.println("  - Check if MySQL is running");
            System.err.println("  - Check URL: jdbc:mysql://localhost:3306/school");
            System.err.println("  - Check username and password");
            System.err.println("Original error: " + e.getMessage());
            
        } catch (SQLSyntaxErrorException e) {
            System.err.println("SQL SYNTAX ERROR: Check your query!");
            System.err.println("Error: " + e.getMessage());
            
        } catch (SQLIntegrityConstraintViolationException e) {
            System.err.println("DATA INTEGRITY ERROR: Duplicate or invalid data");
            System.err.println("Error: " + e.getMessage());
            
        } catch (SQLTimeoutException e) {
            System.err.println("QUERY TIMEOUT: Query took too long to execute");
            
        } catch (SQLException e) {
            System.err.println("DATABASE ERROR!");
            System.err.println("  Message: " + e.getMessage());
            System.err.println("  Error Code: " + e.getErrorCode());
            System.err.println("  SQL State: " + e.getSQLState());
            
            // Check for chained exceptions
            SQLException next = e.getNextException();
            if (next != null) {
                System.err.println("  Next Error: " + next.getMessage());
            }
            
        } finally {
            // Close resources
            try {
                if (rs != null) {
                    rs.close();
                    System.out.println("ResultSet closed");
                }
                if (pstmt != null) {
                    pstmt.close();
                    System.out.println("Statement closed");
                }
                if (con != null) {
                    con.close();
                    System.out.println("Connection closed");
                }
            } catch (SQLException e) {
                System.err.println("Error closing resources: " + e.getMessage());
            }
        }
    }
}
```

---

## Common Error Codes (MySQL)

| Error Code | SQL State | Meaning |
|------------|-----------|---------|
| 1045 | 28000 | Access denied (wrong password) |
| 1049 | 42000 | Unknown database |
| 1146 | 42S02 | Table doesn't exist |
| 1062 | 23000 | Duplicate entry (primary key) |
| 1064 | 42000 | SQL syntax error |
| 1215 | 23000 | Cannot add foreign key constraint |
| 2002 | 08S01 | Can't connect to MySQL server |
| 2013 | 08S01 | Lost connection to server |

---

## SQLWarning (Non-Fatal Warnings)

```java
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM users");

// Check for warnings
SQLWarning warning = stmt.getWarnings();
while (warning != null) {
    System.out.println("Warning: " + warning.getMessage());
    warning = warning.getNextWarning();
}
```

---

## Best Practices

### ✅ DO:

```java
// 1. Catch specific exceptions first
try {
    // code
} catch (SQLSyntaxErrorException e) {
    // Handle syntax error
} catch (SQLException e) {
    // Handle other SQL errors
}

// 2. Always close resources in finally or try-with-resources
try (Connection con = DriverManager.getConnection(...);
     Statement stmt = con.createStatement();
     ResultSet rs = stmt.executeQuery(sql)) {
    // Use resources
} // Auto-closed

// 3. Log meaningful error messages
catch (SQLException e) {
    logger.error("Database error in getUser()", e);
    throw new ServiceException("Failed to fetch user", e);
}

// 4. Check error codes for specific handling
if (e.getErrorCode() == 1062) {
    System.out.println("Duplicate entry!");
}
```

### ❌ DON'T:

```java
// 1. Don't catch generic Exception only
try {
    // code
} catch (Exception e) {  // Too broad!
    // Hides other non-SQL errors
}

// 2. Don't ignore exceptions
catch (SQLException e) {
    // Empty catch block - BAD!
}

// 3. Don't just print and continue
catch (SQLException e) {
    e.printStackTrace();  // User never sees this
    // Continue as if nothing happened
}
```

---

## Summary Table

| Aspect | Description |
|--------|-------------|
| **What it is** | Exception class for database errors |
| **Why needed** | Database operations can fail; need graceful handling |
| **When thrown** | Connection fails, SQL errors, constraint violations |
| **Key methods** | `getMessage()`, `getErrorCode()`, `getSQLState()` |
| **Subclasses** | `SQLSyntaxErrorException`, `SQLIntegrityConstraintViolationException`, etc. |
| **How to handle** | try-catch, specific exception types, finally cleanup |

---

## The Golden Rule

> **SQLException is the parent exception for all database errors. Always use try-catch when executing database operations. Catch specific SQLException subclasses for granular error handling. Always close resources in finally block or use try-with-resources.**

**Memory trick:**
```
SQLException = "Database said NO"
GetMessage = "What went wrong?"
GetErrorCode = "Database's error number"
GetSQLState = "Standard error code"

TRY: Connection → Query → Process
CATCH: SQLException → Handle error
FINALLY: Close everything
```

Would you like me to explain **try-with-resources** or **connection pooling** next?