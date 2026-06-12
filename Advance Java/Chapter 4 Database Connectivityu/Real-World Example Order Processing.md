
```java
import java.sql.*;

public class OrderProcessingDemo {
    
    public static void placeOrder(int customerId, int productId, int quantity) {
        
        try (Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/store", "root", "password")) {
            
            con.setAutoCommit(false);  // Start transaction
            
            try {
                // 1. Check if product has enough stock
                String checkStock = "SELECT quantity FROM products WHERE id = ?";
                PreparedStatement pstmt1 = con.prepareStatement(checkStock);
                pstmt1.setInt(1, productId);
                ResultSet rs = pstmt1.executeQuery();
                rs.next();
                int available = rs.getInt("quantity");
                rs.close();
                pstmt1.close();
                
                if (available < quantity) {
                    throw new SQLException("Insufficient stock! Available: " + available);
                }
                
                // 2. Update product quantity (deduct stock)
                String updateStock = "UPDATE products SET quantity = quantity - ? WHERE id = ?";
                PreparedStatement pstmt2 = con.prepareStatement(updateStock);
                pstmt2.setInt(1, quantity);
                pstmt2.setInt(2, productId);
                pstmt2.executeUpdate();
                pstmt2.close();
                System.out.println("Stock updated");
                
                // 3. Create order
                String createOrder = "INSERT INTO orders (customer_id, product_id, quantity, order_date) VALUES (?, ?, ?, NOW())";
                PreparedStatement pstmt3 = con.prepareStatement(createOrder);
                pstmt3.setInt(1, customerId);
                pstmt3.setInt(2, productId);
                pstmt3.setInt(3, quantity);
                pstmt3.executeUpdate();
                pstmt3.close();
                System.out.println("Order created");
                
                // 4. All successful → Commit
                con.commit();
                System.out.println("\n✅ Order placed successfully!");
                
            } catch (SQLException e) {
                // Any error → Rollback everything
                con.rollback();
                System.out.println("\n❌ Order failed: " + e.getMessage());
                System.out.println("All changes rolled back.");
            }
            
        } catch (SQLException e) {
            System.out.println("Database connection error: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        placeOrder(1, 101, 2);  // Customer 1 buys 2 of product 101
    }
}
```
