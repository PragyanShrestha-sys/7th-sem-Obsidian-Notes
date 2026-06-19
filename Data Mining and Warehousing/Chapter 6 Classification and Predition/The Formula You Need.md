I assume you're asking for the **ID3 algorithm formula**, which is used in decision tree machine learning.  

The core of ID3 is selecting the **best attribute** to split the data at each node, using **Information Gain** (based on **Entropy**).  

ID3 = **a process for making a decision tree**.
**ID3 is the cooking recipe, and the Decision Tree is the meal you get at the end!**

---

## 1. Entropy Formula  
Entropy measures the impurity or uncertainty of a dataset \( S \):

![[Pasted image 20260619070001.png]]

Where:
- \( c \) = number of classes
- \( p_i \) =[[p_i = proportion of samples in class i (siomple probability)]]


---

## 2. Information Gain Formula  
Information Gain measures the reduction in entropy after splitting on attribute \( A \):

![[Pasted image 20260619070015.png]]

[[what does Sv and S mean]]


---

## 3. ID3 Selection Criterion  

The **selection criterion** is just **the rule ID3 uses to decide which attribute to split on at each step**.

![[Pasted image 20260619070021.png]]
[[selection criterion formula explanation easy ]]

| Symbol       | Meaning                                        | Plain English                                  |
| ------------ | ---------------------------------------------- | ---------------------------------------------- |
| **A**        | An attribute (like Color, Size, Shape)         | A feature you could split on                   |
| **A***       | The best attribute to choose                   | The winner!                                    |
| **S**        | Your current dataset                           | All the data at this node                      |
| **IG(S, A)** | Information Gain of splitting S on attribute A | How much cleaner the data gets after splitting |
| **argmax**   | Pick the one with the highest value            | Choose the biggest number                      |

---

## 4. Stopping Criteria (Recursion base cases)
- All samples belong to the same class → return leaf node
- No attributes left → return majority class
- No samples → return parent’s majority class

---

## Example (quick)
If:
![[Pasted image 20260619070031.png]]

---

If you meant something else (like **ID3 tag format** for MP3 files, or **ID3 algorithm in a specific programming language**), just clarify and I’ll give you the right formulas.