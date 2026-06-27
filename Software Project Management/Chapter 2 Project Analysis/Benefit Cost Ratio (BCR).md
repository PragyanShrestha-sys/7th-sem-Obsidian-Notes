**Benefit-Cost Ratio (BCR)** is another way to assess whether a project is worthwhile, but instead of giving a dollar amount or a percentage return, it gives a **ratio** of benefits to costs.

Here is a short explanation.

---

### What is Benefit-Cost Ratio (BCR)?

**Benefit-Cost Ratio (BCR)** compares the **present value of all benefits (cash inflows)** to the **present value of all costs (cash outflows)** .

It answers the question:

> *"For every dollar I spend, how many dollars do I get back?"*

---

### The Formula

$$BCR = \frac{\text{Present Value of Benefits}}{\text{Present Value of Costs}}$$

Where:
- **Present Value of Benefits:** All cash inflows discounted to today
- **Present Value of Costs:** All cash outflows discounted to today (including the initial investment)

---
### How is it Used?

The decision rule is straightforward:

- **If BCR > 1:** Benefits exceed costs. The project creates value. **Accept.**
- **If BCR = 1:** Benefits equal costs. The project breaks even. **Neutral.**
- **If BCR < 1:** Costs exceed benefits. The project destroys value. **Reject.**

---

### Real-World Example (Continuing GreenTech)

Let's return to the **GreenTech Manufacturing** example.

**The Data:**
- Initial Investment: **$1,000,000** (cost)
- Net Annual Cash Flow: **$300,000** (benefit) for years 1 through 5
- Salvage Value: **$50,000** (benefit) at year 5
- Discount Rate: **10%**

**Step 1: Calculate Present Value of Costs**

The costs are just the initial investment (assuming no other costs occur in future years that aren't already netted out).

$$PV_{\text{costs}} = \$1,000,000$$

**Step 2: Calculate Present Value of Benefits**

We already calculated this in the NPV example:

- PV of annual cash flows ($300,000 for 5 years): **$1,137,240**
- PV of salvage value ($50,000 at year 5): **$31,045**

$$PV_{\text{benefits}} = \$1,137,240 + \$31,045 = \$1,168,285$$

**Step 3: Calculate BCR**

$$BCR = \frac{\$1,168,285}{\$1,000,000} = 1.168$$

---

### What Does This Number Mean?

A BCR of **1.168** means:

> *For every $1 invested in this project, the company gets back **$1.168** in present value terms.*

That is a **16.8% return on investment** in present value terms.

---

### BCR vs. NPV vs. IRR

| Metric  | Output                         | Decision Rule                   | What It Tells You                      |
| :------ | :----------------------------- | :------------------------------ | :------------------------------------- |
| **NPV** | Dollar amount (e.g., $168,285) | Accept if NPV > 0               | Total value created in today's dollars |
| **IRR** | Percentage (e.g., 16.5%)       | Accept if IRR > Cost of Capital | Average annual percentage return       |
| **BCR** | Ratio (e.g., 1.168)            | Accept if BCR > 1               | Dollars returned per dollar invested   |

| Scenario                                        | Why BCR is Useful                                                                                                                     |
| :---------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| **Public sector / government projects**         | When evaluating infrastructure, healthcare, or education projects, BCR shows the social benefit per dollar of taxpayer money.         |
| **Budget-constrained environments**             | When you have a fixed budget and must choose between projects, BCR helps rank them by "bang for the buck."                            |
| **Communicating with non-finance stakeholders** | A ratio is often easier to explain than a dollar amount or a percentage. "For every dollar we spend, we get $1.17 back" is intuitive. |

---

### The Catch: When BCR Can Mislead

BCR has limitations, especially when comparing projects:

| Problem | Explanation | Example |
| :--- | :--- | :--- |
| **Ignores scale** | A project with BCR = 2.0 but small size may create less total value than a project with BCR = 1.2 but large size. | Project A: $100 cost, $200 benefit (BCR=2.0, NPV=$100). Project B: $1,000 cost, $1,200 benefit (BCR=1.2, NPV=$200). BCR says A is better, but B creates more actual wealth. |
| **Sensitive to cost classification** | Whether something is classified as a cost or a negative benefit affects the ratio. |

This is why **NPV is generally preferred** for final decisions—it shows the actual dollar value created, not just the ratio.

---

### Short Summary

| Concept | Explanation |
| :--- | :--- |
| **What it is** | Ratio of present value of benefits to present value of costs |
| **Decision Rule** | Accept if BCR > 1 (same as NPV > 0) |
| **What it tells you** | Dollars returned per dollar invested |
| **Best used for** | Public projects, budget-constrained environments, simple communication |
| **Limitation** | Ignores project scale; can rank smaller projects above larger value-creating ones |

---

### Final Simple Takeaway


> **BCR tells you *how many dollars you get back* for each dollar spent.**

---
question

![[Pasted image 20260325164058.png]]
