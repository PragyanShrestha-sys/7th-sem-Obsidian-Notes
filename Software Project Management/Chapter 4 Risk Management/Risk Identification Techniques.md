Here is a detailed explanation of the **8 Risk Identification Techniques** listed in your image. These techniques are used in software project management to discover, document, and categorize potential risks before they become problems.

---

## 1. Brainstorming

**What it is:** A group creativity technique where team members generate a large number of ideas about potential risks in a free-flowing, non-judgmental environment.

**How it works:**
- A facilitator leads the session
- Participants call out any risk that comes to mind
- No criticism or evaluation during the generation phase
- All ideas are recorded (whiteboard, sticky notes, digital tool)
- After generation, ideas are grouped and prioritized

**Best for:** Quick identification of a broad range of risks; early project phases.

**Example:** *"During a 1-hour session, the team identifies 45 potential risks including 'database migration fails,' 'key developer resigns,' and 'API rate limits exceeded.'"*

**Pros:** Fast, collaborative, encourages creativity.  
**Cons:** Can be dominated by loud voices; may miss niche technical risks.

---

## 2. Delphi Technique

**What it is:** A structured, anonymous method that uses multiple rounds of questionnaires to gather and refine expert opinions until consensus is reached.

**How it works:**
- Select a panel of experts (they never meet face-to-face)
- Round 1: Experts anonymously submit risks via questionnaire
- Facilitator summarizes and anonymizes responses
- Round 2: Experts review the summary and revise their inputs
- Repeat until consensus emerges (typically 2-4 rounds)

**Best for:** Large, complex projects; avoiding groupthink; geographically distributed teams.

**Example:** *"Ten security experts independently rate 30 potential risks. After three rounds, they agree that 'SQL injection vulnerability' is the top priority risk."*

**Pros:** No bias from dominant personalities; true expert consensus.  
**Cons:** Time-consuming; requires skilled facilitator.

---

## 3. Interviewing

**What it is:** One-on-one or small group conversations with experienced stakeholders, project managers, technical leads, and subject matter experts to extract risk knowledge.

**How it works:**
- Identify key individuals with relevant experience
- Prepare open-ended questions (e.g., "What kept you up at night on the last project?")
- Conduct interviews (30-60 minutes each)
- Document all risks mentioned
- Follow up to clarify ambiguous points

**Best for:** Capturing deep, experience-based risks that don't surface in group settings.

**Example:** *"Interviewing the senior database architect reveals: 'The new sharding strategy has never been tested at our expected data volume.'"*

**Pros:** In-depth information; builds stakeholder buy-in.  
**Cons:** Time-intensive; quality depends on interviewer skill.

---

## 4. SWOT Analysis (Strengths, Weaknesses, Opportunities, Threats)

**What it is:** A strategic technique that examines internal and external factors across four dimensions to identify both positive and negative risks.

**How it works:**

| Dimension         | Focus                           | Generates                      |
| ----------------- | ------------------------------- | ------------------------------ |
| **Strengths**     | Internal capabilities           | Opportunities (positive risks) |
| **Weaknesses**    | Internal gaps                   | Threats (negative risks)       |
| **Opportunities** | External favorable conditions   | Positive risks to exploit      |
| **Threats**       | External unfavorable conditions | Negative risks to mitigate     |

**Best for:** Strategic planning; early project phases; understanding big-picture context.

**Example:**
- *Weakness:* "Only one developer understands the payment module" → Risk of knowledge loss
- *Opportunity:* "New cloud service offers free tier" → Chance to reduce costs

**Pros:** Balanced view (internal/external, positive/negative); easy to understand.  
**Cons:** Can be too high-level; requires honest self-assessment.

---

## 5. Causal Mapping

**What it is:** A visual technique that identifies root causes and chains of events that could lead to project risks.

**How it works:**
- Start with a potential negative outcome (e.g., "Project delayed by 2 months")
- Work backward to identify all possible causes
- Draw arrows showing cause-effect relationships
- Continue until root causes are identified
- Analyze the map to find leverage points

**Best for:** Complex risks with multiple contributing factors; understanding risk dependencies.

**Example:**
```
Budget Cut → Understaffing → Slow Development → Delayed Launch
     ↑
Poor Planning → Budget Cut
```

**Pros:** Reveals root causes, not just symptoms; shows risk interconnections.  
**Cons:** Can become very complex; time-consuming to build.

---

## 6. Flowchart Method

**What it is:** Creating visual diagrams of project workflows, processes, or system architectures to identify risks at decision points, handoffs, and dependencies.

**How it works:**
- Map out a key process (e.g., deployment, requirements approval, testing)
- Draw each step, decision point, and handoff
- Examine each element for potential failures
- Identify risks where dependencies cross team or system boundaries

**Best for:** Processes with many handoffs; integration points; critical path analysis.

**Example:** *"The deployment flowchart shows: Code Commit → Build → Test → Manual Approval → Deploy. Risk: Manual approval step requires a specific person who might be unavailable."*

**Pros:** Visual and intuitive; reveals hidden dependencies.  
**Cons:** Only as good as the diagram; misses risks outside the mapped flow.

---

## 7. Structured ‘What-If’ Technique (SWIFT)

**What it is:** A systematic, question-driven method where the team asks "What if X happens?" for each component, process step, or decision point.

**How it works:**
- Break the project into components or phases
- For each component, ask structured "What if?" questions
- Generate possible scenarios (both normal and abnormal)
- Assess each scenario for risk potential
- Document risks and recommended actions

**Typical questions:**
- "What if the server crashes during peak hours?"
- "What if the client changes requirements after sign-off?"
- "What if two developers modify the same file simultaneously?"

**Best for:** Safety-critical systems; structured environments; thorough risk coverage.

**Pros:** Systematic and thorough; easy to facilitate with a checklist.  
**Cons:** Can generate many low-priority risks; requires discipline to stay focused.

---

## 8. Fault Tree Analysis (FTA)

**What it is:** A top-down, deductive technique that starts with a specific undesirable event (the "top event") and works backward using logic gates (AND/OR) to identify all possible causes.

**How it works:**
- Define the top event (e.g., "System security breach")
- Identify immediate causes connected by logic gates
- Break each cause down further until basic, identifiable risks are found
- Calculate probability if quantitative data is available

**Example Fault Tree:**

```
                    System Security Breach
                           |
                          OR
                           |
        +------------------+------------------+
        |                                     |
   Weak Authentication                   Software Vulnerability
        |                                     |
       OR                                    OR
        |                                     |
   +---+---+                            +-----+-----+
   |       |                            |           |
Weak    No MFA                      SQL        Unpatched
Password                            Injection   Server
```

**Best for:** High-consequence risks; safety-critical systems; root cause analysis.

**Pros:** Rigorous and logical; excellent for critical risks; quantifiable.  
**Cons:** Time-consuming; requires expertise; only works for known top events.

---

## Summary Table

| Technique        | Best For                         | Effort | Output Type                        |
| ---------------- | -------------------------------- | ------ | ---------------------------------- |
| Brainstorming    | Quick, broad lists               | Low    | Long list of risks                 |
| Delphi Technique | Expert consensus, no bias        | High   | Prioritized, agreed risks          |
| Interviewing     | Deep, experience-based           | Medium | Rich, detailed risks               |
| SWOT Analysis    | Strategic overview               | Low    | Balanced positive/negative risks   |
| Causal Mapping   | Root cause analysis              | Medium | Visual cause-effect diagrams       |
| Flowchart Method | Process dependencies             | Medium | Process-specific risks             |
| SWIFT            | Systematic coverage              | Medium | Comprehensive scenario-based risks |
| FTA              | Critical, high-consequence risks | High   | Logical tree of causes             |

---
## Practical Recommendation
Most software projects should use a **combination** of techniques:

1. **Start with Brainstorming** (fast, broad)
2. **Add Flowchart Method** (process risks)
3. **Conduct key Interviews** (deep expertise)
4. **Use SWOT** (strategic balance)
5. **Reserve FTA or Delphi** for critical/high-risk projects only

> **Key takeaway:** No single technique finds all risks. A multi-technique approach provides the most complete risk identification.


---
Question

![[Pasted image 20260329165914.png]]