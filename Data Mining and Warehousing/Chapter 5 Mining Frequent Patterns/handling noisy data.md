
**1. Binning (Smoothing by Neighbors)**
- **What it does:** It looks at the values around a noisy data point and "averages them out."
- **How it handles noise:** Instead of keeping the wild, wrong number, it replaces it with the average (or middle value) of its neighbors. This evens out the spikes.

**2. Regression (Drawing a Trend Line)**
- **What it does:** It draws a smooth straight or curved line that best fits the general pattern of your data.
- **How it handles noise:** The noisy points that jump far away from this line are pulled back toward the line. The line acts as a "smoothing guide."

**3. Clustering (Grouping Similar Items)**
- **What it does:** It groups together points that are very similar to each other.
- **How it handles noise:** Points that are all alone and don't fit into any group are flagged as "noise." You then either **delete** those loners or study them separately so they don't mess up your analysis.

**4. Detection & Removal (Finding and Deleting)**
- **What it does:** It uses simple math (like checking how far a number is from the average) to find extreme values.
- **How it handles noise:** If a number is way too high or too low (like a salary of $1 billion among regular salaries), you simply **delete it** from your data set.



---

**In short:** All these methods either **smooth out** the wrong values, **pull them back** toward normal, or **delete them** so they stop ruining your results.