## What is JDBC?

**JDBC** = **Java Database Connectivity**
It's a Java API that allows Java programs to connect and interact with databases.

```
Java Program → JDBC → Database (MySQL, Oracle, PostgreSQL)
```

---

## What is it Used For?

| Operation | JDBC Method |
|-----------|-------------|
| Connect to database | `DriverManager.getConnection()` |
| Execute SQL queries | `Statement.executeQuery()` |
| Insert/Update/Delete data | `Statement.executeUpdate()` |
| Retrieve results | `ResultSet.get...()` |

**Real-world examples:** Login systems, banking apps, inventory management, student records.

---

## JDBC Architecture (4 Layers)

```
┌─────────────────────────────────────────────────────────────┐
│                    YOUR JAVA APPLICATION                    │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    JDBC API (java.sql)                      │
│         (DriverManager, Connection, Statement, ResultSet)   │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   JDBC Driver Manager                       │
│              (Manages available database drivers)           │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   Database Driver                           │
│         (MySQL Driver, Oracle Driver, PostgreSQL Driver)    │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      DATABASE                               │
│                 (MySQL, Oracle, PostgreSQL)                 │
└─────────────────────────────────────────────────────────────┘
```

![[Pasted image 20260613062039.png]]

### 1. JDBC API (`java.sql`)
The **standard Java interface** for database-independent connectivity.  
Provides core classes/interfaces:  
- `DriverManager`  
- `Connection`  
- `Statement` / `PreparedStatement`  
- `ResultSet`  

### 2. JDBC Driver Manager  
**Routes requests** between your Java app and the correct database driver.  
- Maintains a list of registered drivers  
- Uses a **connection URL** to pick the right driver  
- Calls: `Class.forName("driverClass")` (old way) or automatic discovery (modern)

### 3. Database Driver  
**Vendor-specific implementation** of the JDBC API.  
- Translates JDBC calls into native database protocol  
- Examples:  
  - `mysql-connector-java` (MySQL)  
  - `ojdbc` (Oracle)  
  - `postgresql` (PostgreSQL)

### 4. Database  
The actual **DBMS** storing data (MySQL, Oracle, PostgreSQL, etc.).  
- Executes SQL queries sent via the driver  
- Returns results back through the same chain

> **Flow:** Java App → JDBC API → DriverManager → Vendor Driver → Actual Database
---
## The 4 Main Components

| Component         | What it does                                   |
| ----------------- | ---------------------------------------------- |
| **DriverManager** | Loads and manages database drivers             |
| **Connection**    | Represents connection to database              |
| **Statement**     | Executes SQL queries                           |
| **ResultSet**     | Stores results of SELECT query                 |
| **Sql Exception** | Handles the Errors that occour in the database |

---

## Simple Example (How it's Used)

```java
import java.sql.*;

public class JDBCDemo {
    public static void main(String[] args) {
        
        try {
            // 1. Load driver (optional in modern JDBC)
            Class.forName("com.mysql.cj.jdbc.Driver");
            
            // 2. Establish connection
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", 
                "username", 
                "password"
            );
            
            // 3. Create statement
            Statement stmt = con.createStatement();
            
            // 4. Execute query
            ResultSet rs = stmt.executeQuery("SELECT * FROM users");
            
            // 5. Process results
            while (rs.next()) {
                System.out.println(rs.getString("name"));
                System.out.println(rs.getInt("age"));
            }
            
            // 6. Close connections
            rs.close();
            stmt.close();
            con.close();
            
        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---
## The 4 JDBC Driver Types

| Type   | Name                    | How it works                                  |
| ------ | ----------------------- | --------------------------------------------- |
| Type 1 | JDBC-ODBC Bridge        | Converts JDBC to ODBC method class (obsolete) |
| Type 2 | Native-API Driver       | Uses database client library                  |
| Type 3 | Network Protocol Driver | Middleware server                             |
| Type 4 | Thin Driver             | Pure Java, direct connection (most common)    |

![[Pasted image 20260613064630.png]]
![[Pasted image 20260613064637.png]]
![[Pasted image 20260613064649.png]]
![[Pasted image 20260613064702.png]]

**Type 4 is most popular** (MySQL Connector/J, PostgreSQL JDBC Driver)


## Flow Diagram (Simple)

```
Java App
    │
    │ 1. Call DriverManager.getConnection()
    ▼
Driver Manager
    │
    │ 2. Finds appropriate driver
    ▼
Database Driver
    │
    │ 3. Creates physical connection
    ▼
Database
    │
    │ 4. Executes SQL query
    ▼
ResultSet (data returned to Java)
```

---

## Key Interfaces (java.sql package)

| Interface | Purpose |
|-----------|---------|
| `Driver` | Database driver interface |
| `Connection` | Session with database |
| `Statement` | SQL execution |
| `PreparedStatement` | Precompiled SQL (prevents SQL injection) |
| `CallableStatement` | Stored procedure execution |
| `ResultSet` | Query results |
| `ResultSetMetaData` | Result metadata (column names, types) |

---

## JDBC vs Other Approaches

| Approach | Description |
|----------|-------------|
| **JDBC** | Direct database access from Java |
| **JPA/Hibernate** | ORM (Object-Relational Mapping) |
| **Spring JDBC** | JDBC with better exception handling |

---

## Advantages of JDBC

| Advantage | Explanation |
|-----------|-------------|
| **Simple** | Easy to learn and use |
| **Database independent** | Same code works with different databases |
| **Performance** | Direct connection (no intermediate layer) |
| **Standard** | Built into Java (java.sql package) |

---

## Disadvantages

| Disadvantage | Explanation |
|--------------|-------------|
| **Boilerplate code** | Lots of try-catch-finally |
| **SQL injection risk** | If using Statement (use PreparedStatement) |
| **Manual connection management** | Must close resources |
| **Database specific** | Some syntax differences exist |

---

## The Golden Rule

> **JDBC is the bridge between Java and databases. Load the driver, get a connection, create a statement, execute the query, process the results, and close everything.**

**Memory trick:**
```
1. Load Driver
2. Get Connection
3. Create Statement
4. Execute Query
5. Process ResultSet
6. Close Everything

"Load, Connect, Statement, Execute, Process, Close"
```

Would you like me to explain **PreparedStatement** (to prevent SQL injection) or **ResultSet types** next?