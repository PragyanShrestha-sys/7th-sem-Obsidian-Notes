**A Statement** is an object that sends SQL queries to the database for execution.

```java
Statement stmt = con.createStatement();
```

### Why is it needed?

| Without Statement                    | With Statement                          |
| ------------------------------------ | --------------------------------------- |
| Can't send SQL to database           | Can send SELECT, INSERT, UPDATE, DELETE |
| No way to execute queries            | Execute any SQL command                 |
| Application can't interact with data | Full database interaction               |
|                                      |                                         |
|                                      |                                         |

### Types of Statements

| Type | Class | When to use |
|------|-------|-------------|
| **Simple Statement** | `Statement` | Single execution, no parameters |
| **PreparedStatement** | `PreparedStatement` | Repeated execution, prevents SQL injection |
| **CallableStatement** | `CallableStatement` | Call stored procedures |
