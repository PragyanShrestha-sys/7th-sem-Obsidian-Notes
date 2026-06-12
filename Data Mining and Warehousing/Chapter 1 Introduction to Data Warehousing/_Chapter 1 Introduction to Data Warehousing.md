## [[Life Cycle of Data]]
The data lifecycle is ==the entire sequence of stages data passes through, from creation or capture to storage, usage, archiving, and final destruction==. It ensures data integrity, compliance, and security, maximizing its value

---
## [[Types of Data]]

**Data types are classified by their degree of organization: structured (rigidly organized), unstructured (no predefined structure), and semi-structured (hybrid). Structured data uses rows/columns, unstructured comprises files/media, and semi-structured uses tags (JSON/XML) to provide partial structure. The key difference lies in flexibility vs. ease of analysis.**

---
## [[Data Warehouse and Data Warehousing]]
A data warehouse is a centralized repository that consolidates structured historical data from multiple sources to support business intelligence, analytics, and decision-making. Data warehousing is the overall process of gathering, cleaning, transforming, and managing this data (often using ETL/ELT) to provide a single, consistent version of the truth

---
## [[Difference betwween Operational Database and Data Warehouse]]


---
## [[Multidimensional Data Model ]]

This is a perfect topic for data warehousing. Think of a **multi-dimensional data model** as a way to organize data not as a flat spreadsheet or a series of linked relational tables, but as a **"cube"** (or a set of cubes) optimized for **analysis and reporting**, not for transaction processing.

---

## [[Architecture of Data Ware house (3 tier)]]

![[Pasted image 20260427074150.png]]

---
## [[Data Warehouse Implementation]]

---

## [[ Data mart]]

A **Data Mart** is a subject-oriented subset of a data warehouse. While a data warehouse contains integrated data from the entire enterprise (e.g., sales, finance, HR, supply chain), a data mart focuses on a single business function or department (e.g., **only Sales** or **only Marketing**).

---
## [[Types of OLAP SERVERS ]]
1. ROLAP
2. MOLAP
3. HOLAP

---
## [[Components of a data warehouse]]

![[Pasted image 20260427080649.png]]

---
## [[ Needs for Datawarehousnig]]

| Business Need          | Problem Without Warehouse            | Solution Provided by Warehouse     |
| :--------------------- | :----------------------------------- | :--------------------------------- |
| **Integration**        | Data silos, inconsistent IDs         | ETL + Central Database             |
| **History**            | Old data overwritten                 | Time-variant, non-volatile storage |
| **Performance**        | Slow queries impact operations       | Separate warehouse + OLAP cubes    |
| **Complex Queries**    | Hours or days of processing time     | Dimensional modeling, indexing     |
| **Data Quality**       | Conflicting reports, distrust        | ETL cleansing & transformation     |
| **Context (Metadata)** | Data is meaningless or misunderstood | Metadata repository                |
| **Strategy**           | Only tactical questions possible     | OLAP, Data Mining, Dashboards      |

![[Pasted image 20260427081734.png]]

---
## [[Current Trends in data warehousing]]

![[Pasted image 20260427081748.png]]


---

## [[Advantages and disadvantages of datawarehousign]]

| Viewpoint               | Summary                                                                                                                                                                           |
| :---------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **For decision-makers** | The advantages (better decisions, competitive edge, ROI) almost always outweigh the disadvantages **if** the organization is committed to the investment and discipline required. |
| **For technical teams** | Be aware of the complexity, ETL challenges, and maintenance burden. Start small (data mart), use agile methods, and leverage cloud services to reduce overhead.                   |
| **Bottom line**         | A data warehouse is not a "set it and forget it" solution. It is an ongoing strategic capability that requires continuous investment, governance, and evolution to deliver value. |

| Aspect           | Advantages                    | Disadvantages                  |
| :--------------- | :---------------------------- | :----------------------------- |
| **Cost**         | Positive ROI over time        | High initial investment        |
| **Time**         | Long-term efficiency          | Long implementation time       |
| **Complexity**   | Enables complex analysis      | Requires specialized skills    |
| **Data Quality** | Clean, consistent, integrated | ETL overhead and maintenance   |
| **Performance**  | Fast query response           | Batch latency (not real-time)  |
| **Flexibility**  | Supports strategic decisions  | Rigid to changing requirements |
| **Security**     | Centralized control           | High-value target for attacks  |
| **Scalability**  | Handles massive data          | Can lead to data sprawl        |