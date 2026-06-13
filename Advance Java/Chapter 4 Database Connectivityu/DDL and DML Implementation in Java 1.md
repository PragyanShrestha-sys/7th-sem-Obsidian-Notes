Below are short, focused Java examples showing **DDL** (Data Definition Language) and **DML** (Data Manipulation Language) using JDBC.

---

## 1. DDL Example (Create Table)

```java
import java.sql.*;

public class DDLExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/testdb";
        String user = "root";
        String password = "password";
//note yo '+' string concatination because double quote bhayera string rakheko 
        String createTableSQL = "CREATE TABLE users ("
                + "id INT PRIMARY KEY AUTO_INCREMENT, "
                + "name VARCHAR(50), "
                + "email VARCHAR(100))";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement()) {
            
            stmt.execute(createTableSQL);
            System.out.println("Table created successfully.");
            
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 2. DML Examples (INSERT, UPDATE, DELETE, SELECT)

### INSERT

```java
String insertSQL = "INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com')";
stmt.executeUpdate(insertSQL);
```

### UPDATE

```java
String updateSQL = "UPDATE users SET email = 'newemail@example.com' WHERE name = 'Alice'";
stmt.executeUpdate(updateSQL);
```

### DELETE

```java
String deleteSQL = "DELETE FROM users WHERE name = 'Alice'";
stmt.executeUpdate(deleteSQL);
```

### SELECT (Query)

```java
String selectSQL = "SELECT * FROM users";
ResultSet rs = stmt.executeQuery(selectSQL);

while (rs.next()) {
    int id = rs.getInt("id");
    String name = rs.getString("name");
    String email = rs.getString("email");
    System.out.println(id + " | " + name + " | " + email);
}
```

---

## 3. Full DML Example with PreparedStatement (Recommended)

```java
import java.sql.*;

public class DMLExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/testdb";
        String user = "root";
        String password = "password";

        String insertSQL = "INSERT INTO users (name, email) VALUES (?, ?)";
        String selectSQL = "SELECT * FROM users WHERE id = ?";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             PreparedStatement pstmtInsert = conn.prepareStatement(insertSQL);
             PreparedStatement pstmtSelect = conn.prepareStatement(selectSQL)) {

            // INSERT
            pstmtInsert.setString(1, "Bob");
            pstmtInsert.setString(2, "bob@example.com");
            int rows = pstmtInsert.executeUpdate();
            System.out.println(rows + " row(s) inserted.");

            // SELECT
            pstmtSelect.setInt(1, 1);
            ResultSet rs = pstmtSelect.executeQuery();
            if (rs.next()) {
                System.out.println("Name: " + rs.getString("name"));
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

## Key Differences (Quick Recap)

| Feature | DDL | DML |
|---------|-----|-----|
| **Commands** | CREATE, ALTER, DROP, TRUNCATE | INSERT, UPDATE, DELETE, SELECT |
| **JDBC Method** | `execute()` | `executeUpdate()` (INSERT/UPDATE/DELETE)<br>`executeQuery()` (SELECT) |
| **Auto-commit** | Usually auto-committed | Can be controlled via `conn.setAutoCommit(false)` + `commit()` |
| **Purpose** | Define/modify schema | Manage data inside tables |

---

Let me know if you'd like a working example with connection pooling or transaction handling!