# Servlets API - Complete Explanation

Here's a **complete explanation** of the Servlets API, its main components, and how they work together.

---

## Part 1: What is Servlets API?

**Servlets API** is a set of Java interfaces and classes that define how servlets interact with a web container. It's part of Java EE (Enterprise Edition).

```
┌─────────────────────────────────────────────────────────────┐
│                    SERVLETS API                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Interfaces              Classes                            │
│  ├── Servlet             ├── GenericServlet                │
│  ├── ServletRequest      ├── HttpServlet                   │
│  ├── ServletResponse     ├── HttpServletRequest (interface)│
│  ├── ServletConfig       ├── HttpServletResponse (interface)│
│  ├── ServletContext      └── HttpSession (interface)       │
│  └── HttpSession                                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Analogy:** Servlets API is like a **toolbox** with all the tools (classes and interfaces) you need to build web applications.

![[Pasted image 20260608074507.png|376]]
![[Pasted image 20260608074514.png|470]]
![[Pasted image 20260608074537.png|473]]

---

## Part 2: Why is Servlets API Needed?

| Need | Provided by Servlets API |
|------|-------------------------|
| Handle HTTP requests | `HttpServletRequest` |
| Send HTTP responses | `HttpServletResponse` |
| Track users | `HttpSession` |
| Configure servlets | `ServletConfig` |
| Share data across app | `ServletContext` |
| Define servlet behavior | `Servlet` interface |

**Without Servlets API:** You'd have to manually parse HTTP requests, manage sessions, handle cookies, etc.

**With Servlets API:** You just use the provided classes and focus on your business logic.

---

## Part 3: Servlets API Package Structure

| Package | Purpose |
|---------|---------|
| `javax.servlet` | Core servlet interfaces and classes |
| `javax.servlet.http` | HTTP-specific servlet classes |
| `javax.servlet.annotation` | Annotations for servlet configuration |
| `javax.servlet.descriptor` | Configuration descriptors |

---

## Part 9: Servlets API Class Hierarchy (Complete)

```
Object
    │
    └── ServletConfig (interface)
    │       │
    │       └── GenericServlet (abstract) implements Servlet, ServletConfig
    │               │
    │               └── HttpServlet (abstract) extends GenericServlet
    │                       │
    │                       └── YourServlet extends HttpServlet
    │
    └── ServletRequest (interface)
    │       │
    │       └── HttpServletRequest (interface) extends ServletRequest
    │
    └── ServletResponse (interface)
    │       │
    │       └── HttpServletResponse (interface) extends ServletResponse
    │
    └── HttpSession (interface)
    │
    └── ServletContext (interface)
```

---

## Quick Reference Table

| Component | Type | Purpose |
|-----------|------|---------|
| `Servlet` | Interface | Root interface for all servlets |
| `HttpServlet` | Abstract class | Base class for HTTP servlets |
| `ServletRequest` | Interface | Client request data |
| `HttpServletRequest` | Interface | HTTP request data |
| `ServletResponse` | Interface | Server response data |
| `HttpServletResponse` | Interface | HTTP response data |
| `HttpSession` | Interface | User session tracking |
| `ServletConfig` | Interface | Servlet configuration |
| `ServletContext` | Interface | Application context |
| `Cookie` | Class | HTTP cookie |

---

## The Golden Rule

> **Servlets API provides all the building blocks for Java web applications. `HttpServlet` is the base class for your servlets. `HttpServletRequest` gives you request data (parameters, headers, session). `HttpServletResponse` lets you send responses (HTML, redirects, errors). `HttpSession` tracks users. `ServletContext` shares data across the whole application.**

**Memory trick:**
```
Request = What client sends
Response = What server sends back
Session = Who the client is
Context = Shared across all
Config = For one servlet

HttpServlet = Your starting point
doGet/doPost = Where you put your logic
```