## [[Java Architecture]]

![[Pasted image 20260518121046.png|462]]

---
## [[Java Buzzwords]]
1. JDK 
2. JRE 
3. JVM

JRE = For RUNNING (consumers, end users)
JDK = For BUILDING (developers, programmers)
JVM = For EXECUTING (PART OF THE JRE) (the actual engine that does the work)

---
## [[Path and Class Path ]]

| Variable      | What it does                                                                                                                           | For Whom             |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| **PATH**      | Tells OS where to find **Java executables** (`java`, `javac`)                                                                          | Operating System     |
| **CLASSPATH** | Tells JVM where to find **your compiled classes** (`.class` files, which includes your own codes classes and library funciton classes) | Java Virtual Machine |
![[Pasted image 20260527064052.png]]

---
## [[Simple Sample Java Program]]

![[Pasted image 20260527072321.png]]


---

## [[1.2]]

Arrays
For Each Loop
Classes and Objects
Overloading Access Privledges
Interface, Inner Class
Final and Static Modifiers
Packages
Inheritence
Overriding

---
## [[1.3 Exception Handling]]

- Try
- Catch 
- Finally 
- Throw
- Thorws
- Exception Classes


![[Pasted image 20260529120241.png|433]]

---

## [[Concurrency]]

**Concurrency** is the ability of a program to execute **multiple tasks at the same time**.

```
Without Concurrency:
Task 1 → Task 2 → Task 3 (slow, one after another)

With Concurrency: (multithreading)
Task 1 ─→
Task 2 ─→ (all running together)
Task 3 ─→
```
---
## [[Working with files]]
Java handles file I/O through **streams**. A stream is a flow of data between your program and a file (or other source/destination).

```
Program → (writes) → Stream → (writes to) → File
Program ← (reads) ← Stream ← (reads from) ← File
```

**Two main categories of streams:**
- **Byte Streams** → For binary data (images, videos, executables)
- **Character Streams** → For text data (`.txt`, `.csv`, `.json`)
- ---
