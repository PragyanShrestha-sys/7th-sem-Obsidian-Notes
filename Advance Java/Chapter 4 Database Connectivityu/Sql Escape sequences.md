 ## SQL Escape Sequences
**Purpose:** Allow special characters in strings that would otherwise break SQL syntax.
### Common Escape Characters:

| Character | Escape Sequence | Used For |
|-----------|----------------|----------|
| `'` (single quote) | `''` or `\'` | String delimiters |
| `%` | `\%` | LIKE wildcard |
| `_` | `\_` | LIKE single-character wildcard |
| `\` (backslash) | `\\` | Escape character itself |

### Examples:

```sql
-- Single quote
INSERT INTO users VALUES ('O''Reilly');  -- O'Reilly

-- LIKE wildcards
SELECT * FROM products WHERE name LIKE '100\%';  -- 100% literal
SELECT * FROM users WHERE name LIKE 'John\_Doe';  -- John_Doe literal

-- Backslash
SELECT * FROM paths WHERE folder LIKE 'C:\\Windows';
```

### SQL Injection Prevention (Important!):
```java
// ❌ DANGEROUS - No escaping
String query = "SELECT * FROM users WHERE name = '" + userInput + "'";

// ✅ SAFE - Use PreparedStatement (automatic escaping)
PreparedStatement stmt = conn.prepareStatement("SELECT * FROM users WHERE name = ?");
stmt.setString(1, userInput);
```

### Note:
- **MySQL default:** `\` is escape character
- **Standard SQL:** `''` for single quote escaping
- **Best practice:** Use `PreparedStatement` instead of manual escaping