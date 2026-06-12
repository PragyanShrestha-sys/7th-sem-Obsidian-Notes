```java
public class BatchTransactionDemo {
    public static void main(String[] args) {
        
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password")) {
            
            con.setAutoCommit(false);
            
            try {
                String sql = "INSERT INTO employees (id, name, salary) VALUES (?, ?, ?)";
                PreparedStatement pstmt = con.prepareStatement(sql);
                
                // Add 1000 records to batch
                for (int i = 1; i <= 1000; i++) {
                    pstmt.setInt(1, i);
                    pstmt.setString(2, "Employee " + i);
                    pstmt.setDouble(3, 50000 + i);
                    pstmt.addBatch();
                    
                    // Execute every 200 records
                    if (i % 200 == 0) {
                        pstmt.executeBatch();
                        System.out.println("Committed 200 records");
                    }
                }
                
                // Execute remaining
                pstmt.executeBatch();
                con.commit();  // Commit all
                System.out.println("All 1000 records inserted successfully!");
                
                pstmt.close();
                
            } catch (SQLException e) {
                con.rollback();  // Rollback ALL if any error
                System.out.println("Batch failed! All changes rolled back.");
                System.out.println("Error: " + e.getMessage());
            }
        } catch (SQLException e) {
            System.out.println("Connection error: " + e.getMessage());
        }
    }
}
```
