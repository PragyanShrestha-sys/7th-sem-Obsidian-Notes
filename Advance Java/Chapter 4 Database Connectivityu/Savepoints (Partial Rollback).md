
```java
import java.sql.*;

public class SavepointDemo {
    public static void main(String[] args) {
        
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password")) {
            
            con.setAutoCommit(false);
            
            Savepoint sp1 = null;
            Savepoint sp2 = null;
            
            try {
                Statement stmt = con.createStatement();
                
                // Operation 1
                stmt.executeUpdate("INSERT INTO users VALUES (1, 'Alice')");
                System.out.println("User Alice added");
                
                // Create savepoint 1
                sp1 = con.setSavepoint("after_alice");
                
                // Operation 2
                stmt.executeUpdate("INSERT INTO users VALUES (2, 'Bob')");
                System.out.println("User Bob added");
                
                // Create savepoint 2
                sp2 = con.setSavepoint("after_bob");
                
                // Operation 3 (will fail - duplicate id)
                stmt.executeUpdate("INSERT INTO users VALUES (2, 'Charlie')");  // Duplicate ID!
                System.out.println("User Charlie added");
                
                // If all successful
                con.commit();
                
            } catch (SQLException e) {
                System.out.println("Error: " + e.getMessage());
                
                // Rollback to savepoint 2 (Bob is still saved, Charlie not inserted)
                if (sp2 != null) {
                    con.rollback(sp2);
                    System.out.println("Rolled back to savepoint 'after_bob'");
                    con.commit();
                    System.out.println("Alice and Bob are saved, Charlie was rolled back");
                }
                // Rollback to savepoint 1 (only Alice saved)
                else if (sp1 != null) {
                    con.rollback(sp1);
                    System.out.println("Rolled back to savepoint 'after_alice'");
                    con.commit();
                    System.out.println("Only Alice is saved");
                }
                // Rollback everything
                else {
                    con.rollback();
                    System.out.println("Complete rollback - no users saved");
                }
            }
            
        } catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```
