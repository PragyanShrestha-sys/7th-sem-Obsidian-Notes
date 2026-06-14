# Handling Cookies and Sessions in Servlets - Complete Guide

Here's a **complete explanation** of handling cookies and sessions in servlets.

[[smaller code explanation]]

---

## Part 1: What are Cookies?

**Cookies** are small text files stored on the user's computer by the browser. They persist between browser sessions.

```
Browser (User's Computer)              Server
        │                                  │
        │  1. First request                │
        ├─────────────────────────────────→│
        │                                  │
        │  2. Response + Set-Cookie        │
        │←─────────────────────────────────┤
        │                                  │
        │  3. Next request + Cookie        │
        ├─────────────────────────────────→│
        │                                  │
```

**Analogy:** Cookies are like a **library card** - the server gives it to you, you keep it, and show it on each visit.

---

## Part 2: What are Sessions?

**Sessions** store user data on the server side, identified by a unique session ID (usually stored in a cookie).

```
┌─────────────────────────────────────────────────────────────┐
│                      WEB SERVER                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │                    SESSIONS                          │   │
│  │                                                      │   │
│  │  Session ID: ABC123 → {user: "john", cart: [...]}   │   │
│  │  Session ID: XYZ789 → {user: "jane", cart: [...]}   │   │
│  │  Session ID: DEF456 → {user: "bob", cart: [...]}    │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

**Analogy:** Sessions are like a **locker at a gym** - you get a key (session ID), the server keeps your stuff in the locker.

---

## Part 3: Cookies vs Sessions

| Aspect | Cookie | Session |
|--------|--------|---------|
| **Storage location** | Browser (client side) | Server side |
| **Data size limit** | ~4KB | Much larger |
| **Security** | Less secure (user can see) | More secure |
| **Persistence** | Can be permanent | Usually temporary |
| **Best for** | Preferences, tracking | Login status, shopping cart |

---


## The Golden Rule

> **Use sessions for server-side data storage (login, cart). Use cookies for client-side preferences (theme, language). Sessions are more secure but temporary. Cookies persist but have size limits. Always call `req.getSession(false)` before assuming a session exists.**

**Memory trick:**
```
Cookies = Client storage (small, persistent)
Sessions = Server storage (large, temporary)

Cookie = "I remember your preference"
Session = "I remember YOU"

setAttribute() = Store in session
getAttribute() = Read from session
invalidate() = End session
```