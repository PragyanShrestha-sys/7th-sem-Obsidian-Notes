
A **Data Mart** is a subject-oriented subset of a data warehouse. While a data warehouse contains integrated data from the entire enterprise (e.g., sales, finance, HR, supply chain), a data mart focuses on a single business function or department (e.g., **only Sales** or **only Marketing**).

Think of it this way:
- **Data Warehouse** = A central library containing books on every subject.
- **Data Mart** = A small reading room dedicated only to "History" or "Science."

### Key Characteristics

- **Smaller & Focused:** Typically ranges from 10 GB to 100 GB (compared to warehouses that can be TB or PB).
- **Departmental:** Owned and managed by a specific department (e.g., the Finance team), not central IT.
- **Faster Implementation:** Can be built in weeks rather than months.
- **Contains Summarized Data:** It usually holds aggregated or summarized data rather than every atomic detail found in the warehouse.

### Data Mart vs. Data Warehouse (Comparison)

| Feature | Data Warehouse | Data Mart |
| :--- | :--- | :--- |
| **Scope** | Enterprise-wide (Company-wide) | Departmental (e.g., Sales only) |
| **Size** | Very large (Terabytes to Petabytes) | Small (Gigabytes) |
| **Time to Build** | Months to Years | Weeks |
| **Data Source** | Many internal operational sources | Usually 1 or 2 specific sources or the DW |
| **Users** | Executives, Data Scientists, Analysts (cross-functional) | Department managers, Analysts |
| **Design** | Top-down (Central design) | Bottom-up (Department design) |

### Advantages of Using Data Marts (Reference to your second image)

Relating this back to the **Data Warehouse Implementation** steps you asked about earlier:

1.  **Improved Performance (Hardware Integration):** Because the data mart is smaller, users do not run slow, complex queries against the giant warehouse.
2.  **Security (User Application):** You can grant a user access to the Marketing Mart without exposing sensitive HR or Finance data.
3.  **Faster Roll-out:** Instead of waiting 2 years for the whole enterprise warehouse to be perfect, you can "Roll-out" a single Sales Data Mart in 4 weeks.
