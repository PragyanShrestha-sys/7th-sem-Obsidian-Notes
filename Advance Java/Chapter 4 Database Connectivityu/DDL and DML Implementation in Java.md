
```java
import java.sql.*;

public class DDLDemo {
    public static void main(String[] args) {
        
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password");
             Statement stmt = con.createStatement()) {
            
            // 1. CREATE TABLE (DDL)
            String createSQL = "CREATE TABLE IF NOT EXISTS students (" +
                               "id INT PRIMARY KEY AUTO_INCREMENT, " +
                               "name VARCHAR(50) NOT NULL, " +
                               "age INT, " +
                               "grade VARCHAR(2))";
            
            int result = stmt.executeUpdate(createSQL);
            System.out.println("Table created (returns 0 for DDL): " + result);
            
            // 2. ALTER TABLE (Add a column)
            String alterSQL = "ALTER TABLE students ADD COLUMN email VARCHAR(100)";
            stmt.executeUpdate(alterSQL);
            System.out.println("Column added successfully!");
            
            // 3. DROP TABLE (Delete table - careful!)
            // String dropSQL = "DROP TABLE students";
            // stmt.executeUpdate(dropSQL);
            // System.out.println("Table dropped");
            
        } catch (SQLException e) {
            System.out.println("DDL Error: " + e.getMessage());
        }
    }
}
```

---

## DML Implementation in Java

```java
import java.sql.*;

public class DMLDemo {
    public static void main(String[] args) {
        
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password");
             Statement stmt = con.createStatement()) {
            
            // 1. INSERT (DML - Add data)
            String insertSQL = "INSERT INTO students (name, age, grade) VALUES " +
                               "('Alice', 20, 'A'), " +
                               "('Bob', 21, 'B'), " +
                               "('Charlie', 19, 'A')";
            
            int rowsInserted = stmt.executeUpdate(insertSQL);
            System.out.println(rowsInserted + " row(s) inserted");
            
            // 2. UPDATE (DML - Modify data)
            String updateSQL = "UPDATE students SET grade = 'A+' WHERE name = 'Bob'";
            int rowsUpdated = stmt.executeUpdate(updateSQL);
            System.out.println(rowsUpdated + " row(s) updated");
            
            // 3. SELECT (DML - Read data)
            String selectSQL = "SELECT * FROM students";
            ResultSet rs = stmt.executeQuery(selectSQL);
            
            System.out.println("\n=== Student Records ===");
            while (rs.next()) {
                System.out.println("ID: " + rs.getInt("id") + 
                                   ", Name: " + rs.getString("name") +
                                   ", Age: " + rs.getInt("age") +
                                   ", Grade: " + rs.getString("grade"));
            }
            rs.close();
            
            // 4. DELETE (DML - Remove data)
            String deleteSQL = "DELETE FROM students WHERE name = 'Charlie'";
            int rowsDeleted = stmt.executeUpdate(deleteSQL);
            System.out.println("\n" + rowsDeleted + " row(s) deleted");
            
        } catch (SQLException e) {
            System.out.println("DML Error: " + e.getMessage());
        }
    }
}
```

---

## Complete Example: Both DDL and DML Together

```java
import java.sql.*;

public class DatabaseOperations {
    private Connection con;
    private Statement stmt;
    
    public void connect() throws SQLException {
        con = DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/mydb", "root", "password");
        stmt = con.createStatement();
    }
    
    // ========== DDL OPERATIONS ==========
    
    public void createProductTable() throws SQLException {
        String sql = "CREATE TABLE IF NOT EXISTS products (" +
                     "id INT PRIMARY KEY AUTO_INCREMENT, " +
                     "name VARCHAR(100) NOT NULL, " +
                     "price DECIMAL(10,2), " +
                     "quantity INT)";
        
        stmt.executeUpdate(sql);
        System.out.println("Product table created/verified");
    }
    
    public void addColumnToProducts() throws SQLException {
        try {
            String sql = "ALTER TABLE products ADD COLUMN category VARCHAR(50)";
            stmt.executeUpdate(sql);
            System.out.println("Category column added");
        } catch (SQLException e) {
            System.out.println("Column might already exist: " + e.getMessage());
        }
    }
    
    // ========== DML OPERATIONS ==========
    
    public void insertProduct(String name, double price, int quantity) throws SQLException {
        String sql = "INSERT INTO products (name, price, quantity) VALUES " +
                     "('" + name + "', " + price + ", " + quantity + ")";
        
        int rows = stmt.executeUpdate(sql);
        System.out.println(rows + " product(s) inserted");
    }
    
    public void updateProductPrice(String name, double newPrice) throws SQLException {
        String sql = "UPDATE products SET price = " + newPrice + 
                     " WHERE name = '" + name + "'";
        
        int rows = stmt.executeUpdate(sql);
        System.out.println(rows + " product(s) updated");
    }
    
    public void selectAllProducts() throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT * FROM products");
        
        System.out.println("\n=== Product List ===");
        while (rs.next()) {
            System.out.println("ID: " + rs.getInt("id") +
                             ", Name: " + rs.getString("name") +
                             ", Price: $" + rs.getDouble("price") +
                             ", Quantity: " + rs.getInt("quantity"));
        }
        rs.close();
    }
    
    public void deleteProduct(String name) throws SQLException {
        String sql = "DELETE FROM products WHERE name = '" + name + "'";
        int rows = stmt.executeUpdate(sql);
        System.out.println(rows + " product(s) deleted");
    }
    
    // ========== DDL CLEANUP ==========
    
    public void dropProductTable() throws SQLException {
        String sql = "DROP TABLE IF EXISTS products";
        stmt.executeUpdate(sql);
        System.out.println("Product table dropped");
    }
    
    public void close() throws SQLException {
        if (stmt != null) stmt.close();
        if (con != null) con.close();
    }
    
    // ========== MAIN ==========
    
    public static void main(String[] args) {
        DatabaseOperations db = new DatabaseOperations();
        
        try {
            db.connect();
            
            // DDL: Create structure
            db.createProductTable();
            db.addColumnToProducts();
            
            // DML: Add data
            db.insertProduct("Laptop", 999.99, 10);
            db.insertProduct("Mouse", 29.99, 50);
            db.insertProduct("Keyboard", 79.99, 30);
            
            // DML: Read data
            db.selectAllProducts();
            
            // DML: Update data
            db.updateProductPrice("Mouse", 24.99);
            db.selectAllProducts();
            
            // DML: Delete data
            db.deleteProduct("Keyboard");
            db.selectAllProducts();
            
            // DDL: Clean up (optional)
            // db.dropProductTable();
            
            db.close();
            
        } catch (SQLException e) {
            System.out.println("Database Error: " + e.getMessage());
        }
    }
}
```
