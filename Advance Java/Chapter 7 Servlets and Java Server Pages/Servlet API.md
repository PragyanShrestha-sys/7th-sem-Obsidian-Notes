
**Servlets API** is a set of Java interfaces and classes that define how servlets interact with a web container. It's part of Java EE (Enterprise Edition).

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