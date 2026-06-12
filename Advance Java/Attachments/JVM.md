

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

## Phase 4: Runtime Data Areas (Memory Layout)

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