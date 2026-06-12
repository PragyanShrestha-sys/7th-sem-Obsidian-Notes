# RMI Architecture - Complete Explanation

Here's a **detailed explanation** of the RMI Architecture layers from your diagram.

---

## RMI Architecture Layers (Bottom to Top)

```
┌─────────────────────────────────────────────────────────────┐
│                    CLIENT SIDE                              │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────────────┐   │
│  │ 1. Client Application (Application Layer)           │   │
│  │    - Your program that wants to call remote method  │   │
│  └─────────────────────────┬───────────────────────────┘   │
│                             │                               │
│  ┌─────────────────────────▼───────────────────────────┐   │
│  │ 2. Stub (Client Proxy)                              │   │
│  │    - Packs parameters (marshaling)                  │   │
│  │    - Sends request to server                        │   │
│  └─────────────────────────┬───────────────────────────┘   │
│                             │                               │
│  ┌─────────────────────────▼───────────────────────────┐   │
│  │ 3. Remote Reference Layer (RRL)                     │   │
│  │    - Manages remote references                       │   │
│  │    - Handles unicast/multicast communication        │   │
│  └─────────────────────────┬───────────────────────────┘   │
│                             │                               │
│  ┌─────────────────────────▼───────────────────────────┐   │
│  │ 4. Transport Layer                                  │   │
│  │    - Establishes network connection                 │   │
│  │    - Sends/receives bytes over network              │   │
│  └─────────────────────────┬───────────────────────────┘   │
└─────────────────────────────┼───────────────────────────────┘
                              │
                              │ Network (TCP/IP)
                              │
┌─────────────────────────────┼───────────────────────────────┐
│                    SERVER SIDE                              │
├─────────────────────────────┼───────────────────────────────┤
│  ┌─────────────────────────▼───────────────────────────┐   │
│  │ 5. Transport Layer                                  │   │
│  │    - Receives bytes from network                    │   │
│  │    - Passes to upper layers                         │   │
│  └─────────────────────────┬───────────────────────────┘   │
│                             │                               │
│  ┌─────────────────────────▼───────────────────────────┐   │
│  │ 6. Remote Reference Layer (RRL)                     │   │
│  │    - Finds correct remote object                    │   │
│  │    - Manages reference counting                     │   │
│  └─────────────────────────┬───────────────────────────┘   │
│                             │                               │
│  ┌─────────────────────────▼───────────────────────────┐   │
│  │ 7. Server Skeleton                                   │   │
│  │    - Unpacks parameters (unmarshaling)              │   │
│  │    - Calls actual method on remote object           │   │
│  └─────────────────────────┬───────────────────────────┘   │
│                             │                               │
│  ┌─────────────────────────▼───────────────────────────┐   │
│  │ 8. Server Application (Remote Object)               │   │
│  │    - Actual implementation of remote methods        │   │
│  │    - Executes the business logic                    │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

---

## [[Layer-by-Layer Explanation]]

---
## Communication Patterns

### One-way (no return)
```
Client → Server: method call, no return
```

### Two-way (with return)
```
Client → Server: method call
Server → Client: return value
```

---

## Layer Responsibilities Summary

| Layer             | Client Responsibility | Server Responsibility        |
| ----------------- | --------------------- | ---------------------------- |
| **Application**   | Makes remote calls    | Implements business logic    |
| **Stub/Skeleton** | Marshals requests     | Unmarshals, dispatches calls |
| **RRL**           | Manages references    | Finds remote objects         |
| **Transport**     | Sends/receives bytes  | Listens, sends/receives      |

---

## Key Terms Defined

| Term | Meaning |
|------|---------|
| **Marshaling** | Converting Java objects to byte stream for network |
| **Unmarshaling** | Converting byte stream back to Java objects |
| **Stub** | Client-side proxy that forwards calls |
| **Skeleton** | Server-side proxy that receives calls |
| **RRL** | Remote Reference Layer - manages remote references |
| **Transport Layer** | Lowest level - handles actual network I/O |

---

## The Golden Rule

> **RMI has 4 layers on each side: Application (your code), Stub/Skeleton (proxy), RRL (reference management), Transport (network I/O). Stub marshals parameters on client, Skeleton unmarshals on server. RRL manages remote references. Transport handles TCP/IP communication.**

**Memory trick (bottom to top):**
```
Transport = "Bytes on wire"
RRL = "Find the object"  
Stub/Skeleton = "Pack/Unpack"
Application = "Your code"

Client: App → Stub → RRL → Transport → Network
Server: Network → Transport → RRL → Skeleton → App
```