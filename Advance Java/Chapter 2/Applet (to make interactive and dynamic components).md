
## What is an Applet?

**Applet** = A Java program that runs inside a web browser.

```
Normal Java program: Runs on your computer (like a calculator app)
Applet: Runs INSIDE a web page (like a game embedded in a website)
```

---

## Visual Example

```
┌─────────────────────────────────────────────┐
│                  Web Browser                │
├─────────────────────────────────────────────┤
│  www.example.com                            │
├─────────────────────────────────────────────┤
│                                             │
│  Welcome to my website!                     │
│                                             │
│  ┌─────────────────────────────────────┐   │
│  │                                     │   │
│  │      JAVA APPLET RUNNING HERE       │   │
│  │                                     │   │
│  │  [Animated graphic or game or form] │   │
│  │                                     │   │
│  └─────────────────────────────────────┘   │
│                                             │
│  Thanks for visiting!                       │
│                                             │
└─────────────────────────────────────────────┘
```

---

## The Simple Idea

| Without Applets | With Applets |
|----------------|--------------|
| Websites were static (text and images only) | Websites could have interactive Java programs |
| No animations, games, or complex features | Could have games, charts, forms, animations |

**Applets made websites COME ALIVE in the 1990s!**

---

## How Applets Worked

```
1. Webpage has <applet> tag
   ↓
2. Browser downloads the Java code
   ↓
3. Browser runs the Java program inside the webpage
   ↓
4. User sees interactive content (game, animation, form)
```

```html
<!-- Simple webpage with applet -->
<html>
<body>
    <applet code="MyGame.class" width="400" height="300">
        Your browser doesn't support Java
    </applet>
</body>
</html>
```

---

## The Main Purpose of Applets

| Purpose | Example |
|---------|---------|
| **Games** | Simple online games |
| **Animations** | Moving charts, banners |
| **Forms** | Interactive data entry |
| **Educational** | Math tutorials, simulations |
| **Visualization** | Stock charts, graphs |

---

## Applet Life Cycle (Quick Overview)

Applet has 4 automatic stages:

| Stage | Method      | When?                      |
| ----- | ----------- | -------------------------- |
| 1     | `init()`    | When applet first loads    |
| 2     | `start()`   | When applet begins running |
| 3     | `stop()`    | When you leave the page    |
| 4     | `destroy()` | When browser closes        |

---
## Why You Don't See Applets Today

| Problem                 | Explanation                                   |
| ----------------------- | --------------------------------------------- |
| **Security**            | Applets could harm your computer              |
| **Browsers**            | Chrome, Firefox, Safari removed Java support  |
| **Better alternatives** | HTML5, JavaScript, Flash (historically)       |
| **Java plugin**         | Required users to install Java (inconvenient) |

**Current status:** Applets are **DEPRECATED** (dead) since Java 9. Browsers no longer support them.

---

## Summary Table

| Question | Answer |
|----------|--------|
| **What is an applet?** | Java program that runs in a web browser |
| **When were they used?** | 1995-2010 (mostly) |
| **What were they used for?** | Games, animations, interactive websites |
| **Are they still used?** | ❌ No (dead technology) |
| **Should I learn applets?** | Only for historical understanding or exams |
| **What replaced them?** | HTML5, JavaScript, CSS |

---

## The Golden Rule

> **Applets were Java programs that ran inside web browsers to make websites interactive. They are now OBSOLETE (dead). Learn about them for history, not for building new applications.**

**Memory trick:**
```
Applet = "Little Application" (app + let)
Born: 1995, Died: ~2015
Rest in peace, applets. You were cool in the 90s.
```

**For your study:** Know what applets were (a Java program in a browser), but FOCUS on Swing for desktop applications and Java for backend/server applications.

Would you like me to explain **why applets died** or **what replaced them** next?