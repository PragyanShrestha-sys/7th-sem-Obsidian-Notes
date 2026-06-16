# Java RMI (Remote Method Invocation) - Complete Guide

Here's a **complete explanation** of Java RMI, what it is, why it's needed, and how to implement it.

---

## Part 1: What is RMI?

**RMI (Remote Method Invocation)** is a Java API that allows a program running on one computer to invoke methods on an object located on another computer.

```
Computer A (Client)                    Computer B (Server)
┌─────────────────────┐               ┌─────────────────────┐
│   Java Program      │               │   Java Program      │
│         │           │               │         │           │
│    [Stub]           │               │  [Skeleton]         │
│         │           │               │         │           │
│    Remote Call      │ ── Network ──→│    Actual Object    │
│         │           │               │         │           │
│    Return Value     │ ←─ Network ──→│    Method Executed  │
└─────────────────────┘               └─────────────────────┘
```

**Analogy:** RMI is like ordering pizza over the phone. You (client) call the pizza shop (server), talk to the person who takes orders (stub), they prepare your pizza (actual object method), and deliver it back to you (return value).

---

## Part 2: Why is RMI Needed?

| Problem | Solution with RMI |
|---------|-------------------|
| Code runs on one computer only | Invoke methods on remote computers |
| Distributed systems complexity | Java objects can call each other across network |
| Need to share functionality | Remote objects accessible to many clients |
| Building client-server apps | Client calls server methods directly |

**Real-world use cases:**
- Distributed computing systems
- Client-server applications
- Remote administration tools
- Multi-tier enterprise applications

---

## Part 3: How RMI Works - Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      RMI ARCHITECTURE                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  CLIENT SIDE                      SERVER SIDE               │
│  ┌─────────────────┐              ┌─────────────────┐      │
│  │  Client Program │              │  Server Program │      │
│  └────────┬────────┘              └────────┬────────┘      │
│           │                                │               │
│           ▼                                ▼               │
│  ┌─────────────────┐              ┌─────────────────┐      │
│  │      Stub       │ ←── Network ─→│   Skeleton      │      │
│  │ (Client Proxy)  │              │ (Server Proxy)  │      │
│  └─────────────────┘              └─────────────────┘      │
│                                                             │
│           ▼                                ▼               │
│  ┌─────────────────┐              ┌─────────────────┐      │
│  │   RMI Registry  │◄────────────►│   Remote Object │      │
│  └─────────────────┘              └─────────────────┘      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### RMI Components:

| Component | What it does |
|-----------|--------------|
| **Remote Interface** | Declares methods that can be called remotely |
| **Remote Object** | Actual implementation on server |
| **Stub** | Client-side proxy that forwards calls to server |
| **Skeleton** | Server-side proxy that receives calls (Java 1.2+ automatic) |
| **RMI Registry** | Looks up remote objects by name (like a phone book) |
| **RMI Runtime** | Manages connections, marshaling, unmarshaling |

---

## Part 4: RMI Implementation Steps

```
Step 1: Create Remote Interface
        ↓
Step 2: Implement Remote Object (Server)
        ↓
Step 3: Create RMI Server (Register object)
        ↓
Step 4: Create RMI Client (Lookup and call)
        ↓
Step 5: Compile, Generate Stub, Run
```

---

## Complete RMI Example - Calculator

### Step 1: Remote Interface

```java
import java.rmi.Remote;
import java.rmi.RemoteException;

// Remote interface - defines methods that can be called remotely
// MUST extend Remote interface
// ALL methods MUST throw RemoteException
public interface Calculator extends Remote {
    
    // Remote methods - these can be called from any machine
    int add(int a, int b) throws RemoteException;
    int subtract(int a, int b) throws RemoteException;
    int multiply(int a, int b) throws RemoteException;
    int divide(int a, int b) throws RemoteException;
}
```

---

### Step 2: Remote Object Implementation (Server)

```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;

// Implementation class MUST extend UnicastRemoteObject
// This exports the remote object and makes it available to clients
public class CalculatorImpl extends UnicastRemoteObject implements Calculator {
    
    // Constructor must throw RemoteException
    public CalculatorImpl() throws RemoteException {
        super();  // Call parent constructor
    }
    
    // Implement all remote methods
    @Override
    public int add(int a, int b) throws RemoteException {
        System.out.println("Adding: " + a + " + " + b);
        return a + b;
    }
    
    @Override
    public int subtract(int a, int b) throws RemoteException {
        System.out.println("Subtracting: " + a + " - " + b);
        return a - b;
    }
    
    @Override
    public int multiply(int a, int b) throws RemoteException {
        System.out.println("Multiplying: " + a + " * " + b);
        return a * b;
    }
    
    @Override
    public int divide(int a, int b) throws RemoteException {
        if (b == 0) {
            throw new RemoteException("Cannot divide by zero!");
        }
        System.out.println("Dividing: " + a + " / " + b);
        return a / b;
    }
}
```

---

### Step 3: RMI Server (Registers the Remote Object)

```java
import java.rmi.Naming;
import java.rmi.registry.LocateRegistry;

public class RMIServer {
    
    public static void main(String[] args) {
        try {
            // Step 1: Create remote object
            Calculator calculator = new CalculatorImpl();
            
            // Step 2: Start RMI Registry on port 1099 (default)
            LocateRegistry.createRegistry(1099);
            System.out.println("RMI Registry started on port 1099");
            
            // Step 3: Bind (register) the remote object with a name
            // Format: rmi://host:port/name
            Naming.rebind("rmi://localhost:1099/CalculatorService", calculator);
            System.out.println("Calculator Server is ready!");
            System.out.println("Waiting for client requests...");
            
        } catch (Exception e) {
            System.out.println("Server error: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

---
### Step 4: RMI Client (Calls Remote Methods)

```java
import java.rmi.Naming;

public class RMIClient {
    
    public static void main(String[] args) {
        try {
            // Step 1: Lookup the remote object from RMI Registry
            // This returns a reference to the stub (client proxy)
            Calculator calculator = (Calculator) Naming.lookup(
                "rmi://localhost:1099/CalculatorService"
            );
            
            System.out.println("Connected to Calculator Server!");
            
            // Step 2: Call remote methods (they execute on server!)
            int a = 25;
            int b = 10;
            
            System.out.println("\n--- Remote Method Calls ---");
            System.out.println(a + " + " + b + " = " + calculator.add(a, b));
            System.out.println(a + " - " + b + " = " + calculator.subtract(a, b));
            System.out.println(a + " * " + b + " = " + calculator.multiply(a, b));
            System.out.println(a + " / " + b + " = " + calculator.divide(a, b));
            
            // Call divide by zero to show exception
            try {
                System.out.println("\nTrying divide by zero:");
                calculator.divide(10, 0);
            } catch (Exception e) {
                System.out.println("Remote exception: " + e.getMessage());
            }
            
        } catch (Exception e) {
            System.out.println("Client error: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

---

## How to Compile and Run RMI

### Step-by-step execution:

```bash
# Step 1: Compile all Java files
javac Calculator.java CalculatorImpl.java RMIServer.java RMIClient.java

# Step 2: Start RMI Registry (in separate terminal)
rmiregistry

# Step 3: Start Server (in another terminal)
java RMIServer

# Step 4: Run Client (in another terminal)
java RMIClient
```

### Expected Output:

**Server Output:**
```
RMI Registry started on port 1099
Calculator Server is ready!
Waiting for client requests...
Adding: 25 + 10
Subtracting: 25 - 10
Multiplying: 25 * 10
Dividing: 25 / 10
```

**Client Output:**
```
Connected to Calculator Server!

--- Remote Method Calls ---
25 + 10 = 35
25 - 10 = 15
25 * 10 = 250
25 / 10 = 2

Trying divide by zero:
Remote exception: Cannot divide by zero!
```

---

## RMI Terminology

| Term | Meaning |
|------|---------|
| **Marshaling** | Converting parameters to byte stream for network transfer |
| **Unmarshaling** | Converting byte stream back to parameters |
| **Stub** | Client-side proxy that marshals parameters and sends to server |
| **Skeleton** | Server-side proxy that unmarshals parameters and calls actual method |
| **Binding** | Registering remote object with a name in RMI Registry |
| **Lookup** | Finding remote object by name from RMI Registry |

---

## Complete Example: Chat Application using RMI

### Remote Interface

```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface ChatService extends Remote {
    void sendMessage(String user, String message) throws RemoteException;
    void registerClient(ChatClient client) throws RemoteException;
    String getMessages() throws RemoteException;
}
```

### Client Callback Interface

```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface ChatClient extends Remote {
    void receiveMessage(String user, String message) throws RemoteException;
}
```

### Server Implementation

```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;
import java.util.ArrayList;
import java.util.List;

public class ChatServiceImpl extends UnicastRemoteObject implements ChatService {
    
    private List<String> messages = new ArrayList<>();
    private List<ChatClient> clients = new ArrayList<>();
    
    public ChatServiceImpl() throws RemoteException {
        super();
    }
    
    @Override
    public void sendMessage(String user, String message) throws RemoteException {
        String fullMessage = user + ": " + message;
        messages.add(fullMessage);
        System.out.println(fullMessage);
        
        // Broadcast to all clients
        for (ChatClient client : clients) {
            try {
                client.receiveMessage(user, message);
            } catch (Exception e) {
                // Client disconnected
            }
        }
    }
    
    @Override
    public void registerClient(ChatClient client) throws RemoteException {
        clients.add(client);
        System.out.println("New client registered");
    }
    
    @Override
    public String getMessages() throws RemoteException {
        return String.join("\n", messages);
    }
}
```

---

## RMI vs Other Technologies

| Feature | RMI | Socket | Web Services |
|---------|-----|--------|--------------|
| **Level** | Method-level | Data-level | Service-level |
| **Complexity** | Medium | High | Low |
| **Performance** | Good | Very Good | Moderate |
| **Platform** | Java only | Any language | Any language |
| **Firewall friendly** | No | Yes (with HTTP) | Yes (HTTP) |
| **Use case** | Java-to-Java | Any communication | Cross-platform |

---

## RMI Advantages and Disadvantages

### Advantages

| Advantage | Explanation |
|-----------|-------------|
| **Object-oriented** | Direct method calls on remote objects |
| **Type safety** | Compile-time checking of remote interfaces |
| **Distributed garbage collection** | Automatic cleanup of remote objects |
| **Security** | Built-in security manager |
| **Loading classes** | Can load class definitions from server |

### Disadvantages

| Disadvantage | Explanation |
|--------------|-------------|
| **Java-only** | Both client and server must be Java |
| **Firewall issues** | Uses custom ports (not HTTP) |
| **Complex setup** | Need registry, security policies |
| **Not for web** | Doesn't work well with web browsers |

---

## RMI Limitations

| Limitation | Solution |
|------------|----------|
| Parameters must be serializable | Implement Serializable |
| Remote methods throw RemoteException | Handle in client code |
| Objects passed by copy (not reference) | Use remote objects for shared access |
| Network failures possible | Implement retry logic |

---

## The Golden Rule

> **RMI allows Java objects on different computers to call each other's methods. The remote interface defines available methods, the server implements them and registers with RMI registry, the client looks up the object and calls methods as if local. All remote methods must throw RemoteException.**

**Memory trick:**
```
RMI = Remote Method Invocation
Remote Interface = "What can be called"
Implementation = "How it works"
Registry = "Phone book"
Stub = "Local representative"
Skeleton = "Server representative"

Client → Stub → Network → Skeleton → Server Object
```