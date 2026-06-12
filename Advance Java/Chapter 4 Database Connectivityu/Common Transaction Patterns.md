### Pattern 1: Simple Transaction

```java
con.setAutoCommit(false);
try {
    // Do work
    con.commit();
} catch (SQLException e) {
    con.rollback();
}
```

### Pattern 2: Transaction with Savepoint

```java
con.setAutoCommit(false);
Savepoint sp = null;
try {
    // Work before checkpoint
    sp = con.setSavepoint();
    // Critical work
    con.commit();
} catch (SQLException e) {
    if (sp != null) con.rollback(sp);
    else con.rollback();
}
```

### Pattern 3: Nested Transaction

```java
con.setAutoCommit(false);
Savepoint outer = con.setSavepoint();
try {
    // Outer work
    Savepoint inner = con.setSavepoint();
    try {
        // Inner work
        con.commit();  // Only releases inner
    } catch (SQLException e) {
        con.rollback(inner);
    }
    con.commit();
} catch (SQLException e) {
    con.rollback(outer);
}
```
