Here's a clear explanation of the **Critical Path Method (CPM)** steps, based on the content you provided:

---
### 1. Define Activities  
List all tasks needed to complete the project.  
Each activity should have a clear start and end point.  
*Example: Design, Coding, Testing, Deployment*

---
### 2. Sequence Activities  
Determine the logical order of tasks by identifying dependencies (what must happen before what).  
*Example: Design → Coding → Testing → Deployment*

---
### 3. Draw the Network Diagram  
Create a visual representation of the project workflow using nodes (activities) and arrows (dependencies).  
This helps in understanding the flow and relationships between tasks.

---
### 4. Estimate Activity Durations  
Assign a time estimate to each activity based on past data, experience, or expert judgment.  
*Example: Design = 5 days, Coding = 10 days*

---
### 5. [[Perform Forward Pass and Backward Pass]]
Calculate the **earliest start (ES)** and **earliest finish (EF)** for each activity.  
- **ES** = earliest time an activity can begin  
- **EF** = ES + duration  

This step determines the earliest possible project completion time if all tasks start as soon as possible.

Calculate the **latest finish (LF)** and **latest start (LS)** for each activity without delaying the project.  
- **LF** = latest time an activity can finish without delaying the project  
- **LS** = LF – duration  


---

### 7. Calculate Float (Slack)  
Float is the amount of time an activity can be delayed without affecting the overall project duration.  

Float = LS − ES = LF − EF

Activities with zero float are critical.

---

### 8. Identify Critical Path  
The **critical path** is the longest sequence of activities with **zero float**.  
Any delay in these activities directly delays the project.  
*Note: Float = 0 ⇒ Critical Activity*

---
### 9. Project Duration  
The total project duration is the sum of durations of all activities on the critical path.  
This represents the **minimum time needed** to complete the project.

---
Labelling Conventions 
![[Pasted image 20260328083445.png]]
