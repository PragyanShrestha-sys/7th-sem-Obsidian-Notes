Here's a **complete explanation** of RowSet Interface and its types.

---
![[Pasted image 20260606155500.png]]

## What is RowSet?

**RowSet** is a wrapper around ResultSet that adds more features like scrollability, updatability, and disconnected operation.

```
ResultSet (Basic)              RowSet (Advanced)
    │                               │
    ├── Connected to DB              ├── Can work disconnected
    ├── Cannot be serialized         ├── Can be serialized (aru format ma                                             change garne)
    ├── Cannot be passed remotely    ├── Can be passed over network
    └── Limited features             └── More features (sort, filter)
```

**Analogy:** ResultSet is like a **live phone call** (must stay connected). RowSet is like a **recorded message** (can use offline).

---

## Why is RowSet Needed?

| Problem with ResultSet | Solution with RowSet |
|-----------------------|---------------------|
| Must maintain database connection | Can work disconnected |
| Cannot be sent over network | Serializable (can be sent remotely) |
| Cannot sort/filter data | Built-in sorting and filtering |
| Limited scrollability | Full scrollable support |
| Can't be modified offline | Offline updates possible |
| One-way only (forward) | Full navigation |

---

## Types of RowSet

| Type | Full Name | Connection | Use Case |
|------|-----------|------------|----------|
| **JdbcRowSet** | Connected RowSet | Always connected | Simple wrapper for ResultSet |
| **CachedRowSet** | Disconnected RowSet | Disconnects after loading | Offline work |
| **WebRowSet** | XML RowSet | Disconnected | XML exchange |
| **JoinRowSet** | Join RowSet | Disconnected | Join multiple RowSets |
| **FilteredRowSet** | Filtered RowSet | Disconnected | Filter data |

---

## RowSet Hierarchy

```
RowSet (Interface)
    │
    ├── JdbcRowSet (Connected)
    │
    └── CachedRowSet (Disconnected)
            │
            ├── WebRowSet (XML support)
            ├── JoinRowSet (Join capability)
            └── FilteredRowSet (Filter capability)
```

---

## 1. JdbcRowSet (Connected RowSet)

**What it is:** [[A connected, scrollable, updatable wrapper around ResultSet. ]]

### Characteristics

| Feature | Support |
|---------|---------|
| Connection | Always connected |
| Scrollable | ✅ Yes |
| Updatable | ✅ Yes |
| Serializable | ❌ No |
| Use case | Replacing ResultSet |

### Implementation

ntoe: **RowSetFactory exists ONLY to create different types of RowSet objects.**

```java
import javax.sql.rowset.*;
import java.sql.*;

public class JdbcRowSetDemo {
    public static void main(String[] args) {
        
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password")) {
            
            // Create JdbcRowSet
            RowSetFactory factory = RowSetProvider.newFactory();
            JdbcRowSet jrs = factory.createJdbcRowSet();
            
            // Set connection and query
            jrs.setUrl("jdbc:mysql://localhost:3306/mydb");
            jrs.setUsername("root");
            jrs.setPassword("password");
            jrs.setCommand("SELECT id, name, age FROM students");
            jrs.execute();
            
            // Navigate freely (scrollable)
            System.out.println("=== Forward ===");
            while (jrs.next()) {
                System.out.println(jrs.getString("name"));
            }
            
            System.out.println("\n=== Backward ===");
            while (jrs.previous()) {
                System.out.println(jrs.getString("name"));
            }
            
            // Update data
            jrs.absolute(1);
            jrs.updateString("name", "Updated Name");
            jrs.updateRow();
            System.out.println("\nRow updated!");
            
            jrs.close();
            
        } catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 2. CachedRowSet (Disconnected RowSet)

**What it is:** A RowSet that disconnects from database after loading data, allowing offline work.

### Characteristics

| Feature | Support |
|---------|---------|
| Connection | Disconnects after load |
| Scrollable | ✅ Yes |
| Updatable | ✅ Yes (offline) |
| Serializable | ✅ Yes |
| Use case | Offline work, network transfer |

### Implementation

```java
import javax.sql.rowset.*;
import java.sql.*;

public class CachedRowSetDemo {
    public static void main(String[] args) {
        
        try {
            // Create CachedRowSet
            RowSetFactory factory = RowSetProvider.newFactory();
            CachedRowSet crs = factory.createCachedRowSet();
            
            // Set connection and query
            crs.setUrl("jdbc:mysql://localhost:3306/mydb");
            crs.setUsername("root");
            crs.setPassword("password");
            crs.setCommand("SELECT id, name, age FROM students");
            crs.execute();
            
            // Data is now loaded - can close connection!
            System.out.println("Data loaded. Connection can be closed.");
            
            // Work offline (no database connection needed)
            System.out.println("=== Offline Data ===");
            crs.beforeFirst();
            while (crs.next()) {
                System.out.println("ID: " + crs.getInt("id") + 
                                   ", Name: " + crs.getString("name"));
            }
            
            // Modify offline
            crs.absolute(1);
            crs.updateString("name", "Modified Offline");
            crs.updateRow();
            
            // Reconnect and sync changes back
            crs.acceptChanges();  // Pushes changes to database
            System.out.println("\nChanges synchronized to database!");
            
            crs.close();
            
        } catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 3. WebRowSet (XML RowSet)

**What it is:** A CachedRowSet with XML support (can read/write data as XML).

### Characteristics

| Feature | Support |
|---------|---------|
| Base | CachedRowSet |
| XML support | ✅ Yes (read/write XML) |
| Disconnected | ✅ Yes |
| Use case | Web services, data exchange |

### Implementation

```java
import javax.sql.rowset.*;
import java.io.*;

public class WebRowSetDemo {
    public static void main(String[] args) {
        
        try {
            // Create WebRowSet
            RowSetFactory factory = RowSetProvider.newFactory();
            WebRowSet wrs = factory.createWebRowSet();
            
            // Load data
            wrs.setUrl("jdbc:mysql://localhost:3306/mydb");
            wrs.setUsername("root");
            wrs.setPassword("password");
            wrs.setCommand("SELECT id, name, age FROM students");
            wrs.execute();
            
            // Write to XML file
            FileOutputStream fos = new FileOutputStream("students.xml");
            wrs.writeXml(fos);
            System.out.println("Data exported to students.xml");
            fos.close();
            
            // Read from XML file
            WebRowSet wrs2 = factory.createWebRowSet();
            FileInputStream fis = new FileInputStream("students.xml");
            wrs2.readXml(fis);
            fis.close();
            
            System.out.println("\n=== Data from XML ===");
            while (wrs2.next()) {
                System.out.println(wrs2.getString("name"));
            }
            
            wrs.close();
            wrs2.close();
            
        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**Generated XML:**
```xml
<?xml version="1.0"?>
<webRowSet xmlns="http://java.sun.com/xml/ns/jdbc">
  <properties>
    <command>SELECT id, name, age FROM students</command>
  </properties>
  <data>
    <currentRow>
      <columnValue>1</columnValue>
      <columnValue>Alice</columnValue>
      <columnValue>20</columnValue>
    </currentRow>
    <currentRow>
      <columnValue>2</columnValue>
      <columnValue>Bob</columnValue>
      <columnValue>21</columnValue>
    </currentRow>
  </data>
</webRowSet>
```

---

## 4. JoinRowSet

**What it is:** A RowSet that can combine (join) multiple RowSets without connecting to database.

### Characteristics

| Feature | Support |
|---------|---------|
| Base | CachedRowSet |
| Join capability | ✅ Yes |
| Use case | Combining multiple data sources |

### Implementation

```java
import javax.sql.rowset.*;
import java.sql.*;

public class JoinRowSetDemo {
    public static void main(String[] args) {
        
        try {
            RowSetFactory factory = RowSetProvider.newFactory();
            
            // Create first CachedRowSet (Students)
            CachedRowSet students = factory.createCachedRowSet();
            students.setUrl("jdbc:mysql://localhost:3306/mydb");
            students.setUsername("root");
            students.setPassword("password");
            students.setCommand("SELECT id, name FROM students");
            students.execute();
            
            // Create second CachedRowSet (Scores)
            CachedRowSet scores = factory.createCachedRowSet();
            scores.setUrl("jdbc:mysql://localhost:3306/mydb");
            scores.setUsername("root");
            scores.setPassword("password");
            scores.setCommand("SELECT student_id, subject, marks FROM scores");
            scores.execute();
            
            // Create JoinRowSet
            JoinRowSet joinRS = factory.createJoinRowSet();
            
            // Add both RowSets and specify join column
            joinRS.addRowSet(students, "id");
            joinRS.addRowSet(scores, "student_id");
            
            // Result is joined data
            System.out.println("=== Joined Data ===");
            while (joinRS.next()) {
                System.out.println("Student: " + joinRS.getString("name") +
                                   ", Subject: " + joinRS.getString("subject") +
                                   ", Marks: " + joinRS.getInt("marks"));
            }
            
        } catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 5. FilteredRowSet

**What it is:** A RowSet that can filter data without using WHERE clause in SQL.

### Characteristics

| Feature | Support |
|---------|---------|
| Base | CachedRowSet |
| Filter capability | ✅ Yes (Predicate interface) |
| Use case | Dynamic filtering |

### Implementation

```java
import javax.sql.rowset.*;
import java.sql.*;

// Custom filter
class AgeFilter implements Predicate {
    private int minAge;
    private int maxAge;
    
    public AgeFilter(int min, int max) {
        this.minAge = min;
        this.maxAge = max;
    }
    
    @Override
    public boolean evaluate(RowSet rs) {
        try {
            int age = ((FilteredRowSet) rs).getInt("age");
            return age >= minAge && age <= maxAge;
        } catch (SQLException e) {
            return false;
        }
    }
    
    @Override
    public boolean evaluate(Object value, int column) { return true; }
    
    @Override
    public boolean evaluate(Object value, String columnName) { return true; }
}

public class FilteredRowSetDemo {
    public static void main(String[] args) {
        
        try {
            // Create FilteredRowSet
            RowSetFactory factory = RowSetProvider.newFactory();
            FilteredRowSet frs = factory.createFilteredRowSet();
            
            // Load data
            frs.setUrl("jdbc:mysql://localhost:3306/mydb");
            frs.setUsername("root");
            frs.setPassword("password");
            frs.setCommand("SELECT id, name, age FROM students");
            frs.execute();
            
            // Apply filter (only students age 20-22)
            frs.setFilter(new AgeFilter(20, 22));
            
            System.out.println("=== Students aged 20-22 ===");
            frs.beforeFirst();
            while (frs.next()) {
                System.out.println(frs.getString("name") + " - " + frs.getInt("age"));
            }
            
            // Remove filter
            frs.setFilter(null);
            
            System.out.println("\n=== All Students ===");
            frs.beforeFirst();
            while (frs.next()) {
                System.out.println(frs.getString("name") + " - " + frs.getInt("age"));
            }
            
            frs.close();
            
        } catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## RowSet Types Comparison

| Feature | JdbcRowSet | CachedRowSet | WebRowSet | JoinRowSet | FilteredRowSet |
|---------|-----------|--------------|-----------|------------|----------------|
| **Connection** | Always | Disconnected | Disconnected | Disconnected | Disconnected |
| **Scrollable** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| **Updatable** | ✅ Yes | ✅ Yes | ✅ Yes | ❌ No | ✅ Yes |
| **Serializable** | ❌ No | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| **XML Support** | ❌ No | ❌ No | ✅ Yes | ❌ No | ❌ No |
| **Join Capability** | ❌ No | ❌ No | ❌ No | ✅ Yes | ❌ No |
| **Filter Capability** | ❌ No | ❌ No | ❌ No | ❌ No | ✅ Yes |
| **Use Case** | ResultSet replacement | Offline work | Web services | Combining data | Dynamic filtering |

---

## Quick Reference

### Creating RowSet (Java 7+)

```java
RowSetFactory factory = RowSetProvider.newFactory();

JdbcRowSet jrs = factory.createJdbcRowSet();
CachedRowSet crs = factory.createCachedRowSet();
WebRowSet wrs = factory.createWebRowSet();
JoinRowSet jrs = factory.createJoinRowSet();
FilteredRowSet frs = factory.createFilteredRowSet();
```

### Common Methods

| Method | Description |
|--------|-------------|
| `setUrl(String url)` | Set database URL |
| `setUsername(String user)` | Set username |
| `setPassword(String pass)` | Set password |
| `setCommand(String sql)` | Set SQL command |
| `execute()` | Execute query |
| `acceptChanges()` | Push changes to DB |
| `writeXml(OutputStream os)` | Write as XML |
| `readXml(InputStream is)` | Read from XML |
| `setFilter(Predicate p)` | Apply filter |

---

## RowSet vs ResultSet

| Feature | ResultSet | RowSet |
|---------|-----------|--------|
| **Connection** | Always connected | Can be disconnected |
| **Scrollable** | Optional (must specify) | Always scrollable |
| **Updatable** | Optional (must specify) | Always updatable |
| **Serializable** | ❌ No | ✅ Yes (CachedRowSet) |
| **Pass over network** | ❌ No | ✅ Yes |
| **Sort/Filter** | ❌ No (via SQL) | ✅ Yes (programmatic) |
| **XML Support** | ❌ No | ✅ Yes (WebRowSet) |
| **Memory** | Low | Higher (caches data) |

---

## The Golden Rule

> **Use ResultSet for simple, connected operations. Use JdbcRowSet when you need scrollability. Use CachedRowSet when you need disconnected operation or network transfer. Use WebRowSet for XML data exchange. Use JoinRowSet to combine multiple datasets. Use FilteredRowSet for dynamic filtering without changing SQL.**

**Memory trick:**
```
JdbcRowSet = ResultSet with scroll (connected)
CachedRowSet = Work offline (disconnected)
WebRowSet = XML data exchange
JoinRowSet = Combine multiple RowSets
FilteredRowSet = Dynamic filtering

RowSet = ResultSet + Extra Features
```