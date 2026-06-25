Since you’ve already asked about the *functions* and *responsibilities*, asking about the **"roles of SCM"** is the perfect final piece of the puzzle. 

Here is the key distinction: **Functions** are the *jobs that need to get done* (planning, auditing, etc.). **Responsibilities** are the *duties assigned to a specific person*. **Roles** are the actual **job titles** and **personas** that people hold within an organization to carry out those duties.

In the software industry, SCM roles exist on a spectrum. You don't need all of these for a 5-person startup, but you absolutely need all of them for a 500-person enterprise. Here is the breakdown of the 5 core SCM roles:

---

### Role 1: The Configuration Manager (The "Process Guru")
*This is the dedicated, full-time SCM specialist. If a company is large or heavily regulated (banking, healthcare, aerospace), this is a standalone job title.*

**What they do:** They own the SCM infrastructure. They don't write much application code themselves; instead, they build and maintain the servers, the backup systems, and the automated build pipelines (Jenkins/GitLab CI). 
**Their daily mantra:** *"Is the server up? Are the permissions correct? Did the nightly build succeed?"*

---

### Role 2: The Change Control Board (CCB) Member (The "Traffic Cops")
*This is not a single person, but a committee. It usually includes the Project Manager, the Lead Architect, the QA Lead, and the Configuration Manager.*

**What they do:** They meet regularly (weekly or bi-weekly) to review "Change Requests." They decide which bugs get fixed now, which new features wait until next quarter, and which changes are too risky to approve. 
**Their daily mantra:** *"What is the business impact of this change? Is it worth the risk of breaking the existing system?"*

---

### Role 3: The Build Engineer / Release Manager (The "Packager")
*This role is the bridge between the developers and the IT/Ops team. Often a specialized DevOps role.*

**What they do:** They take the source code approved by the Change Control Board and physically compile it, run the final tests, and package it into an installer, a mobile app file, or a Docker container. They then hand this "artifact" to the operations team for deployment. They also manage the version numbers (e.g., moving from 2.3.0 to 2.4.0).
**Their daily mantra:** *"Is this build clean? Can we replicate it perfectly if we need to roll back?"*

---

### Role 4: The Lead Developer / Tech Lead (The "Merger")
*This is a senior developer who still writes code but has extra SCM authority.*

**What they do:** They are the gatekeepers of the `main` branch. While junior developers write code in feature branches, the Lead Developer is primarily responsible for reviewing Pull Requests (PRs), resolving complex merge conflicts, and ensuring that code-quality standards are met before anything gets merged. 
**Their daily mantra:** *"Does this code meet our standards? Will it break the codebase if I merge it?"*

---

### Role 5: The Developer / Programmer (The "Committer")
*This is every software engineer on the team. Even if they have zero interest in SCM, they have a role to play.*

**What they do:** They are the ones actually creating the changes. Their role is to diligently commit their code frequently, write clear commit messages, pull updates from the server daily to avoid conflicts, and follow the branching rules set by the Configuration Manager. 
**Their daily mantra:** *"Did I commit my work? Did I write a good message? Did I break the build?"*

---

### The "Unofficial" Role: The SCM Evangelist
*This is usually the Configuration Manager or a Senior Dev who loves automation.*

**What they do:** They don't just enforce rules; they actively look for ways to make SCM easier. They write custom scripts to automate tedious tasks, create cheat-sheets for new hires, and hold lunch-and-learn sessions to teach the team advanced Git tricks. They turn SCM from a "chore" into a "superpower" for the team.

---

### A Quick Summary Table: Who Does What?

| Role | Primary Focus | Key Authority |
| :--- | :--- | :--- |
| **Configuration Manager** | Infrastructure & Tooling | Can shut down a build server to fix it. |
| **Change Control Board** | Approving/Rejecting big changes | Can officially delay a product release. |
| **Build/Release Engineer** | Packaging & Version Numbers | Decides exactly what code goes to the customer. |
| **Lead Developer** | Code Quality & Merging | Can reject a developer's Pull Request. |
| **Developer** | Writing code & committing | Can break the build (and is responsible to fix it!). |

---

### The Startup Rule (When roles overlap)

If you are at a small startup with only 3 developers, **you do not need 5 separate people**. The roles simply collapse:

- The **CTO** plays the **Configuration Manager** (sets up GitHub) and the **Lead Developer** (reviews PRs).
- The **developers** play the **Build Engineer** (they click the "Deploy" button themselves).
- The entire team acts as the **Change Control Board** (they huddle around a table and decide what goes into the next release).

---

**What is your current situation?** Are you hiring for a dedicated SCM role, or are you trying to figure out which of these roles *you* are expected to play in your current team? Let me know, and I'll give you tailored advice!