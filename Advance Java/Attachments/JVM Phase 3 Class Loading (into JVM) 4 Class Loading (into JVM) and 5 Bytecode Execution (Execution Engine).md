
## Phase 3: Class Loading (into JVM)


**JVM is a complete managed runtime environment that takes your bytecode and handles EVERY aspect of execution - memory, threads, garbage collection, JIT compilation, and system interaction - so you don't have to.**

note: JVM is a runtime environment



When you run `java Hello`, the **Class Loader** subsystem activates:

```
┌─────────────────────────────────────────────────────────────┐
│                    CLASS LOADER SUBSYSTEM                    │
├─────────────────┬─────────────────┬─────────────────────────┤
│  Bootstrap      │  Extension      │  Application            │
│  ClassLoader    │  ClassLoader    │  ClassLoader            │
│  (loads rt.jar) │  (loads ext/*)  │  (loads classpath)      │
└─────────────────┴─────────────────┴─────────────────────────┘
                           ↓
              ┌────────────────────────┐
              │  Loading → Linking →   │
              │  Initialization        │
              └────────────────────────┘
```

### Steps in class loading:

| Step | What happens |
|------|--------------|
| **Loading** | Finds `.class` file, reads bytecode, creates `Class` object in heap |
| **Verification** | Checks bytecode validity (no illegal jumps, correct stack usage) |
| **Preparation** | Allocates memory for static variables (default values) |
| **Resolution** | Replaces symbolic references with actual memory addresses |
| **Initialization** | Executes static initializers, assigns real values to statics |

---

## Phase 4:Class Loading (into JVM)

Once loaded, bytecode runs in **JVM memory**:

```
                        ┌─────────────────────────────┐
                        │         HEAP                 │
                        │  (All objects, arrays,       │
                        │   String pool)               │
                        └──────────────┬──────────────┘
                                       │
┌──────────────┐    ┌──────────────┐   │   ┌──────────────┐
│   STACK      │    │  METHOD AREA │   │   │ PC REGISTERS │
│ (Each thread)│    │ (Class data, │   │   │ (Per thread) │
│ - Local vars │    │  static vars,│   │   │ Current line │
│ - Operand    │    │  bytecode)   │   │   │ of execution │
│   stack      │    └──────────────┘   │   └──────────────┘
│ - Frame refs │                       │
└──────────────┘    ┌──────────────┐   │
                    │ NATIVE METHOD │   │
                    │    STACK      │   │
                    │ (For native   │   │
                    │  code calls)  │   │
                    └──────────────┘   │
                                       ↓
                              ┌─────────────────┐
                              │ GARBAGE COLLECTOR│
                              │ (Automatic heap  │
                              │  memory cleanup) │
                              └─────────────────┘
```

### Detailed example: When `main` runs

```java
public static void main(String[] args) {
    int a = 10;        // stored in stack frame
    Hello obj = new Hello();  // 'obj' in stack, object in heap
}
```

**Memory state:**
```
STACK (Thread 1)                    HEAP
┌─────────────────────┐            ┌─────────────────┐
│ main() stack frame  │            │ Hello object    │
│ - args: reference ──┼───(null)──→│ (no fields yet) │
│ - a: 10             │            └─────────────────┘
│ - obj: reference ───┼───────────→┌─────────────────┐
│ - return address    │            │ Hello object    │
└─────────────────────┘            │ (actual object) │
                                   └─────────────────┘
```

---

## Phase 5: Bytecode Execution (Execution Engine)

The **Execution Engine** has two components working together:

### A. Interpreter
- Reads bytecode **one instruction at a time**
- Converts each to machine code **on the fly**
- **Slow** because same code may be interpreted many times

### B. JIT Compiler (Just-In-Time)
- Monitors **hot methods** (frequently executed)
- Compiles entire method to **native machine code**
- Caches compiled code for reuse
- **Major performance boost** (50-100x for hot code)

```
Bytecode → [Interpreter starts] → detects hot method → [JIT compiles to native] → [Direct CPU execution]
                ↓                                                      ↓
            (slow start)                                         (fast after)
```

### Optimization levels (HotSpot JVM):
| Level | Mode | Use case |
|-------|------|----------|
| 0 | Interpreted | Startup, cold code |
| 1 | C1 (Client) | Light optimization, quick startup |
| 2 | C2 (Server) | Aggressive optimization, long-running apps |
| 3 | Tiered (default) | Mix of C1 + C2 |

---
