# Java RMI - Short Explanation

## What is RMI?

**RMI (Remote Method Invocation)** allows a Java program on one computer to call methods on an object located on another computer.

```
Computer A (Client)              Computer B (Server)
     │                                │
     │─── remote method call ────────→│
     │                                │
     │←─── return value ──────────────│
```

**Analogy:** Like ordering pizza over phone - you (client) call, pizza shop (server) takes order, makes pizza (executes method), delivers it (returns value).

---

## Why Needed?

| Problem | Solution |
|---------|----------|
| Code runs on one computer | Call methods on remote computers |
| Build distributed systems | Java objects communicate across network |
| Client-server applications | Client calls server methods directly |

---

## RMI Components (Short)

| Component | What it does |
|-----------|--------------|
| **Remote Interface** | Declares methods (what client can call) |
| **Implementation Class** | Actual method code (on server) |
| **RMI Registry** | Phone book - finds remote objects by name |
| **Stub** | Client-side proxy (sends request to server) |

---

## Short Code Example - Calculator

### Step 1: Remote Interface

```java
import java.rmi.Remote;
import java.rmi.RemoteException;

// MUST extend Remote, ALL methods throw RemoteException
public interface Calculator extends Remote {
    int add(int a, int b) throws RemoteException;
}
```

---

### Step 2: Server Implementation

```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;

// MUST extend UnicastRemoteObject
public class CalculatorImpl extends UnicastRemoteObject implements Calculator {
    
    public CalculatorImpl() throws RemoteException {
        super();
    }
    
    @Override
    public int add(int a, int b) throws RemoteException {
        return a + b;  // Actual method logic
    }
}
```

---

### Step 3: RMI Server (Registers the object)

```java
import java.rmi.Naming;
import java.rmi.registry.LocateRegistry;

public class RMIServer {
    public static void main(String[] args) throws Exception {
        // Create remote object
        Calculator calc = new CalculatorImpl();
        
        // Start registry on port 1099
        LocateRegistry.createRegistry(1099);
        
        // Register object with name
        Naming.rebind("rmi://localhost:1099/CalculatorService", calc);
        
        System.out.println("Server ready");
    }
}
```

---

### Step 4: RMI Client (Calls remote method)

```java
import java.rmi.Naming;

public class RMIClient {
    public static void main(String[] args) throws Exception {
        // Lookup remote object
        Calculator calc = (Calculator) Naming.lookup(
            "rmi://localhost:1099/CalculatorService"
        );
        
        // Call remote method (executes on server!)
        int result = calc.add(10, 5);
        System.out.println("Result: " + result);  // Result: 15
    }
}
```

---

## The 4 Essential Rules

| Rule | Why |
|------|-----|
| `extends Remote` | Interface must be remote-capable |
| `throws RemoteException` | Every method can fail over network |
| `extends UnicastRemoteObject` | Makes object available remotely |
| Register with `Naming.rebind()` | Publish object in registry |

---

## The Golden Rule

> **Remote Interface = What (methods). Implementation = How (actual code). Registry = Where (lookup). Client = Who (calls methods). All remote methods throw RemoteException.**

**Memory trick:**
```
RMI = Remote Method Invocation
Interface = Contract
Implement = Logic
Registry = Phone book
Stub = Local proxy
```