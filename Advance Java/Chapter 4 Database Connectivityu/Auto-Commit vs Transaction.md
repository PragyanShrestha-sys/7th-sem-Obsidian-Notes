


```java
// Auto-commit ON (default) - each statement commits immediately
con.setAutoCommit(true);
stmt.executeUpdate("INSERT INTO users VALUES (1, 'Alice')");  // Commits immediately
stmt.executeUpdate("INSERT INTO users VALUES (2, 'Bob')");    // Commits immediately

// Auto-commit OFF - all statements in one transaction
con.setAutoCommit(false);
stmt.executeUpdate("INSERT INTO users VALUES (1, 'Alice')");  // Not yet committed
stmt.executeUpdate("INSERT INTO users VALUES (2, 'Bob')");    // Not yet committed
con.commit();  // Both committed together
```
