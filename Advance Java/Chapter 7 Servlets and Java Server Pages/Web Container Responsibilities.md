
### 1. Servlet Lifecycle Management

```
Container starts
      │
      ▼
┌─────────────────────────────────────────────────────────────┐
│ Step 1: Load Servlet Class                                  │
│         (Container loads .class file)                       │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ Step 2: Create Servlet Instance                             │
│         (Container calls constructor)                       │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ Step 3: Initialize Servlet                                  │
│         (Container calls init() method)                     │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ Step 4: Handle Requests                                     │
│         (Container calls service() for each request)        │
│         ├── doGet() for GET requests                        │
│         └── doPost() for POST requests                      │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│ Step 5: Destroy Servlet                                     │
│         (Container calls destroy() before shutdown)         │
└─────────────────────────────────────────────────────────────┘
```

### 2. Request Processing

```java
// Container does all this automatically!
// 1. Receives HTTP request from browser
// 2. Creates HttpServletRequest object
// 3. Creates HttpServletResponse object
// 4. Finds appropriate servlet
// 5. Creates or assigns thread
// 6. Calls servlet.service(request, response)
// 7. Sends response back to browser
// 8. Cleans up
```

### 3. Session Management

| Task | How Container Does It |
|------|----------------------|
| Create session | `HttpSession session = request.getSession()` |
| Track user | Uses cookies or URL rewriting |
| Store data | `session.setAttribute("key", value)` |
| Timeout | Automatically expires sessions |
| Cleanup | Removes inactive sessions |

### 4. Thread Management

```
┌─────────────────────────────────────────────────────────────┐
│                    THREAD POOL                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Request 1 ──→ Thread 1 ──→ Servlet Instance               │
│  Request 2 ──→ Thread 2 ──→ Servlet Instance (same object) │
│  Request 3 ──→ Thread 3 ──→ Servlet Instance               │
│                                                             │
│  Note: Same servlet instance handles multiple requests!    │
│        (Must be thread-safe!)                               │
└─────────────────────────────────────────────────────────────┘
```

### 5. JSP Management

```
JSP File (hello.jsp)
      │
      ▼ (Container translates)
      │
Servlet Java File (hello_jsp.java)
      │
      ▼ (Container compiles)
      │
Servlet Class (hello_jsp.class)
      │
      ▼ (Container loads and executes)
      │
HTML Response
```
