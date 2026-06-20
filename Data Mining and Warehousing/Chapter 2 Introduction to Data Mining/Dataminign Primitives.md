**Data mining primitives** are ==the fundamental building blocks used by a user to interact with a data mining system==. They allow users to construct a specific data mining query, directing the system on exactly what to search for and how to present the results

1. **Task-Relevant Data** – *What data to use.* Specifies the specific dataset, attributes, and filtering conditions (e.g., "US customers in 2025").

2. **Kind of Knowledge** – *What to find.* Defines the mining task, such as association, classification, clustering, or outlier detection.

3. **Background Knowledge** – *Context to guide mining.* Usually in the form of concept hierarchies (e.g., *city → state → country*) to allow different levels of detail.

4. **Interestingness Measures** – *What makes a pattern worthwhile.* Criteria like support, confidence, simplicity, and novelty to filter out trivial results.

5. **Presentation/Visualization** – *How to show results.* Output formats like rules, tables, decision trees, charts, or graphs.

---

**In short:** These primitives act like a "mining query" — they tell the system *where* to look, *what* to look for, *how* to interpret it, *what* to keep, and *how* to show it. Together, they form the basis for a Data Mining Query Language (DMQL).