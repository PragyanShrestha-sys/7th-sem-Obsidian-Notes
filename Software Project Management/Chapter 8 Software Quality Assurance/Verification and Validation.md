


---

## The Core Difference

| Concept          | Key Question                           | Meaning                                                                      |
| ---------------- | -------------------------------------- | ---------------------------------------------------------------------------- |
| **Verification** | **Are we building the product right?** | Checking that the software meets its specifications and is free of bugs.     |
| **Validation**   | **Are we building the right product?** | Checking that the software meets customer needs and high-level requirements. |

---

## Verification (Static Testing)

**Definition:** Verification is the process of checking that **software achieves its goal without any bugs**. It ensures whether the product that is developed is right or not.

**Also known as:** **Static Testing** (because no code execution is involved)

### Verification Activities:
- **Inspections** – Formal examination of documents or code
- **Reviews** – Peer or team review of requirements, design, or code
- **Walkthroughs** – Author-led guided review of documents
- **Desk-checking** – Manual code review by a developer

### When Verification Happens:
At each stage before coding:
- Review CRS (Customer Requirement Specification)
- Review SRS (Software Requirement Specification)
- Review HLD (High-Level Design)
- Review LLD (Low-Level Design)

---

## Validation (Dynamic Testing)

**Definition:** Validation is the process of checking whether the software product is **up to the mark** and has **high-level requirements**. It checks **what we are developing is the right product**.

**Also known as:** **Dynamic Testing** (because code is executed)

### Validation Activities:
- **Black Box Testing** – Testing functionality without internal code knowledge
- **White Box Testing** – Testing internal code structure and logic
- **Unit Testing** – Testing individual components
- **Integration Testing** – Testing how modules work together
- **System Testing** – Testing the complete integrated system
- **User Acceptance Testing (UAT)** – Testing by end users to validate business needs

### When Validation Happens:
After coding, during execution phases:
- White box testing (during coding)
- Functional testing (after LLD)
- Integration testing (after HLD)
- System testing (after SRS)
- User acceptance testing (after CRS)

---

## Verification and Validation Model (V-Model)

![[Pasted image 20260403080704.png|443]]

The images show a **V-Model** (Verification and Validation model), which maps verification activities on the left (descending) and validation activities on the right (ascending).

| Development Phase | Verification Activity | Corresponding Validation Activity |
|-------------------|----------------------|-----------------------------------|
| **CRS** (Customer Requirement Specification) | Review CRS | User Acceptance Testing |
| **SRS** (Software Requirement Specification) | Review SRS | System Testing |
| **HLD** (High-Level Design) | Review HLD | Integration Testing |
| **LLD** (Low-Level Design) | Review LLD | Functional Testing |
| **Coding** | Code reviews, inspections | White Box Testing |

### Visual Representation (from your image):

```
        CRS ─────────────────────────────────────► User Acceptance Testing
         │                                              │
         ▼                                              ▼
        SRS ─────────────────────────────────────► System Testing
         │                                              │
         ▼                                              ▼
        HLD ─────────────────────────────────────► Integration Testing
         │                                              │
         ▼                                              ▼
        LLD ─────────────────────────────────────► Functional Testing
         │                                              │
         ▼                                              ▼
       Coding ─────────────────────────────────────► White Box Testing
         
    VERIFICATION (Left side)              VALIDATION (Right side)
    (Static Testing)                      (Dynamic Testing)
    "Building the product right?"         "Building the right product?"
```

---

## Comparison Summary Table

| Aspect | Verification | Validation |
|--------|--------------|------------|
| **Question** | Are we building the product right? | Are we building the right product? |
| **Also known as** | Static Testing | Dynamic Testing |
| **Execution** | No code execution | Code is executed |
| **Focus** | Specifications, standards, documentation | High-level requirements, customer needs |
| **Activities** | Reviews, inspections, walkthroughs, desk-checking | Black box, white box, unit, integration, system, UAT |
| **When performed** | Early (requirements through coding) | Later (coding through acceptance) |
| **Examples** | Reviewing SRS, code walkthrough | Running test cases, UAT |

---

