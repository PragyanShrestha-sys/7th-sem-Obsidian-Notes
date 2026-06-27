
## Risk Identification Steps 
### 1. Study Past Projects

**What it means:** Review historical data, lessons learned, and post-mortem reports from similar completed projects.

**Why it's important:** History tends to repeat itself. Problems that occurred in past projects (e.g., integration failures, staff turnover, scope creep) are likely to appear again.

**How to do it:**
- Examine project closure reports
- Interview team members from previous projects
- Review issue logs and defect databases

**Example:** *"Three past projects using the same legacy database system all had performance issues—this is a risk for our project too."*

### 2. Analyze the Project Plan

**What it means:** Break down the project plan (WBS, schedule, resource allocation) and convert it into a flowchart to identify critical workflows and vulnerabilities.

**Why it's important:** A visual representation of the workflow reveals dependencies, bottlenecks, and handoff points where risks often hide.

**How to do it:**
- Create flowcharts showing task sequences
- Identify critical path activities
- Flag areas with tight dependencies or external inputs

**Example:** *"The flowchart shows that testing cannot start until the API integration is complete. If API delivery is delayed, testing is blocked—that's a risk."*



### 3. Conduct Brainstorming Sessions

**What it means:** Bring together stakeholders, team members, subject matter experts, and even end-users to generate risk ideas collaboratively.

**Why it's important:** Different perspectives catch different risks. Developers see technical risks; managers see schedule risks; clients see business risks.

**How to do it:**
- Use structured brainstorming (each person shares ideas)
- Categorize as **known risks** (already experienced) and **known unknowns** (we know we don't know something)
- Avoid criticism during ideation

**Example:** *"During a brainstorming session, the QA lead mentions that the test environment is unstable—this risk wasn't on anyone else's radar."*



### 4. Evaluate Key Decisions

**What it means:** Assess major decisions made during project planning—technical, operational, legal, political, and financial—for their risk implications.

**Why it's important:** Every decision carries trade-offs. Choosing one technology over another, selecting a vendor, or committing to a deadline all introduce specific risks.

**How to do it:**
- List all major project decisions
- For each decision, ask: *"What could go wrong because of this choice?"*
- Consider legal compliance, political stakeholder dynamics, and financial constraints

**Example:** *"The decision to outsource development to a low-cost vendor introduces legal (contract), operational (time zone), and quality risks."*

---

### 5. Document the Risk

**What it means:** Record each identified risk in a structured format (typically a **Risk Register**) with essential details.

**Why it's important:** Undocumented risks are easily forgotten. Written records enable tracking, analysis, and communication.


**Example Risk Register entry:**
> *ID: R-012 | Date: March 29 | Description: Key backend developer may leave during the project | Category: Project Risk | Source: Past project analysis*

## Summary Table of Steps

| Step                      | Action                  | Key Question                          |
| ------------------------- | ----------------------- | ------------------------------------- |
| 1. Study Past Projects    | Review historical data  | *What went wrong before?*             |
| 2. Analyze Project Plan   | Create flowcharts       | *Where are the bottlenecks?*          |
| 3. Brainstorming          | Collaborate with team   | *What are we worried about?*          |
| 4. Evaluate Key Decisions | Assess major choices    | *What risks come with this decision?* |
| 5. Document the Risk      | Record in Risk Register | *How do we track this?*               |

## Key Takeaway

Risk identification is **not a one-time event**. These five steps should be repeated throughout the project lifecycle—especially after major milestones, requirement changes, or team changes. The earlier you identify a risk, the cheaper and easier it is to manage.


---

