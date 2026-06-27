
**Official Definition:** A baseline is a formally approved, frozen snapshot of a software project’s configuration items (source code, documents, libraries, and environment settings) at a specific point in time. 

**Real-World Translation:** It is an official, unchangeable milestone. Once a baseline is created, you cannot edit it directly. You can only build *from* it or create a *new* version from it.

---

### The 3 Most Common Types of Baselines

Not all baselines are created equal. In a professional software project, you will usually create these three:

| Type of Baseline        | What it is                                                                                                   | Real-World Example                                                                                                                     |
| :---------------------- | :----------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------- |
| **Functional Baseline** | The initial agreed-upon requirements. What the customer *said* they wanted at the very start of the project. | The signed contract and design documents before a single line of code is written.                                                      |
| **Allocated Baseline**  | The breakdown of those requirements into specific, assignable pieces.                                        | Saying, *"The 'Login' feature belongs to Team A, and the 'Payment' feature belongs to Team B."*                                        |
| **Product Baseline**    | The actual, tested, working source code and executable files that are ready to be shipped to the customer.   | The exact code you tagged as `v2.0.0` and sent to the Apple App Store. *(This is what most developers mean when they say "baseline").* |

---

### How a Baseline Works in Practice (The Git Tag)

In modern development, creating a baseline is incredibly simple. You use a **Tag** in Git. 

Imagine you are releasing Version 3.0 to your customers. You don't just tell them, *"Go download the latest code from our main branch,"* because the `main` branch changes daily with bug fixes. 

Instead, you type this command:
`git tag -a v3.0.0 -m "Official release to all customers"`
`git push origin v3.0.0`

What just happened? 

- Git took a perfect, frozen picture of every single file at that exact millisecond.
- That picture is now permanently labeled `v3.0.0`. 
- It is **read-only**. No developer can accidentally change it. 

Now, if a customer reports a critical bug in Version 3.0 six months from now, you simply check out that tag (`git checkout v3.0.0`), fix the bug, and release `v3.0.1`—without affecting the new features you are building for `v5.0` in the `main` branch.

---

### Why Management Absolutely LOVES Baselines

As a manager, baselines are your best friend because they solve four huge headaches:

1. **Reproducibility:** A baseline guarantees you can rebuild *exactly* the same software that a customer is using right now, even if it's 10 years old.
2. **Accountability:** If the software fails a security audit, you can point to the baseline and say, *"This exact code is what the government reviewed and approved. Nothing else was added."*
3. **Parallel Development:** Because `v3.0` is frozen in a baseline, your developers can work on `v4.0` in the `main` branch without worrying about breaking the version your customers are currently using.
4. **Rollback:** If you release `v4.0` and it crashes in production 10 minutes later, you don't panic. You simply revert the production servers to the `v3.0` baseline. You are back online in 2 minutes while you figure out what went wrong.

---

### The Golden Rule of Baselines (Never Break It!)

There is one hard, unbreakable rule in SCM regarding baselines: 

> **Once a baseline is created and officially approved, you NEVER change it. You can only build a NEW baseline (v3.1, v4.0) from it.**

If you find a bug in `v3.0`, you do **not** open the `v3.0` tag and edit the file. You check out the `v3.0` tag, create a *new* branch from it, fix the bug, and release that new branch as `v3.1`. The original `v3.0` baseline remains untouched forever—like a museum piece.

---

### A Quick Analogy to Lock It In

Think of a software baseline like the **blueprints** for a skyscraper:

- The architect creates the blueprint (the Functional Baseline).
- The construction crew pours the foundation, adds floors, and installs windows (the Product Baseline).
- Once the building is finished and people move in, you cannot go back and change the blueprint for *that* specific building. 
- If the owner wants a new elevator, you don't alter the original blueprint; you create a *new* blueprint (Version 2) based on the old one, and build a new wing onto the side.

---

**Are you about to create your first baseline for a project?** If so, I can give you a quick pre-release checklist (what to verify *before* you hit that "create tag" button) so you don't accidentally freeze broken code!