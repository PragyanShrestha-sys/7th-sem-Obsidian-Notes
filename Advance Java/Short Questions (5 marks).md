## List the steps to create a RMI application. Differentiate between RMI and CORBA

[[RMI Code Short]]

library funcitons used 
import javax.rmi
import javax.rmi.naming
iport javax.rmi.registry.LocateRegistry
Interface decalre
define interface ()
register interface(server side) (LocateRegistry.CreateRegistry and naming.rebind)
Call interface(client side) (Naming.Lookup)

---
![[Pasted image 20260616194956.png]]

```java
import java.sql.*;

public class MovieDB {
    public static void main(String[] args) throws Exception {
        Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "root", "password");
        
        // Insert 3 records in one line
        conn.createStatement().executeUpdate("INSERT INTO MOVIE VALUES(1,'Jatra','Drama'),(2,'Chha','Horror'),(3,'Kabhaddi','Action')");
        
        // Update genre using prepared statement
        PreparedStatement ps = conn.prepareStatement("UPDATE MOVIE SET genre=? WHERE title=?");
        ps.setString(1, "Comedy");//1 bhaneko first '?'
        ps.setString(2, "Jatra"); // 2 bhaneko second '?'
        ps.executeUpdate();
        
        conn.close();
    }
}
```

---
