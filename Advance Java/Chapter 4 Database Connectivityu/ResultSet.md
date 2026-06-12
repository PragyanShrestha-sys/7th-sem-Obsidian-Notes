

### Why is it needed?

| Without ResultSet | With ResultSet |
|-------------------|----------------|
| Can't retrieve query results | Can get all returned data |
| No way to access column values | Access by column name or index |
| Can't iterate through rows | Can loop through all matching records |

### ResultSet as a Table

```
ResultSet visually represents a database table:

     id │ name     │ age │ grade
    ────┼──────────┼─────┼───────
     1  │ Alice    │ 20  │ A      ← Current row (cursor points here)
     2  │ Bob      │ 21  │ B
     3  │ Charlie  │ 19  │ A

- Cursor starts BEFORE first row
- next() moves to first row
- getString("name") gets "Alice"
```

---
## [[ResultSet Types & Concurrency]]

![[Pasted image 20260606105130.png]]
![[Pasted image 20260606105139.png]]


## Common Use Cases Table

|What you need to do|Method|Why|
|---|---|---|
|Display all rows|`next()`|Most common, works with all types|
|Get total row count|`last()` + `getRow()`|Need count before displaying|
|Jump to specific row|`absolute(row)`|Direct access by row number|
|Go back to previous row|`previous()`|When you need to re-read|
|Reset to beginning|`beforeFirst()`|To loop through again|
|Check if data exists|`next()`|Returns false if empty|
|Get current position|`getRow()`|To know where you are|
