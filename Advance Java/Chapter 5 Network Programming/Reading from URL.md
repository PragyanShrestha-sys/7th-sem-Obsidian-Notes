Here's a **simple, focused explanation** of reading from a URL in Java.

---

## What Does "Reading from a URL" Mean?

**Reading from a URL means downloading content from a web address into your Java program.**

```
Java Program → URL → Web Server → Returns HTML/JSON/Text → Your Program reads it
```

**Analogy:** Like opening a web page and copying the text.

---

## Why Read from a URL?

| Use Case | Example |
|----------|---------|
| **Call Web APIs** | Get weather data, stock prices |
| **Web Scraping** | Extract information from websites |
| **Download files** | Get images, PDFs from internet |
| **Consume web services** | Read JSON/XML from REST APIs |

---

## 3 Ways to Read from URL in Java

| Method | Best for |
|--------|----------|
| `openStream()` | Simple, one-liner reading |
| `URLConnection` | Need headers, metadata |
| `HttpURLConnection` | Need HTTP methods (GET/POST) |

---

## Method 1: openStream() (Simplest)

```java
import java.net.*;
import java.io.*;

public class ReadURLSimple {
    public static void main(String[] args) {
        try {
            // Create URL object
            URL url = new URL("https://www.example.com");
            
            // Open stream and read
            BufferedReader reader = new BufferedReader(
                new InputStreamReader(url.openStream())
            );
            
            // Read line by line
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
            reader.close();
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**What happens line by line:**
1. `url.openStream()` → Opens connection to the website
2. `InputStreamReader` → Converts bytes to characters
3. `BufferedReader` → Reads efficiently line by line
4. `readLine()` → Gets one line of HTML/text

---

## Method 2: openStream() - Shortest Version

```java
import java.net.*;
import java.io.*;

public class ReadURLShort {
    public static void main(String[] args) throws IOException {
        URL url = new URL("https://www.example.com");
        try (BufferedReader reader = new BufferedReader(
                new InputStreamReader(url.openStream()))) {
            reader.lines().forEach(System.out::println);
        }
    }
}
```

---
	

## Common Errors and Solutions

| Error                         | Cause              | Solution              |
| ----------------------------- | ------------------ | --------------------- |
| `MalformedURLException`       | Wrong URL format   | Check URL syntax      |
| `UnknownHostException`        | Domain not found   | Check internet/domain |
| `FileNotFoundException` (404) | Page doesn't exist | Check URL path        |
| `ConnectException`            | Server unreachable | Check server status   |
| `SocketTimeoutException`      | No response        | Increase timeout      |
|                               |                    |                       |

---
## Quick Reference

| Need | Use |
|------|-----|
| **Simple read** | `url.openStream()` |
| **Read headers** | `URLConnection` |
| **HTTP methods (GET/POST)** | `HttpURLConnection` |
| **Set timeout** | `conn.setConnectTimeout()` |
| **Set user agent** | `conn.setRequestProperty("User-Agent", "...")` |
| **Check response** | `conn.getResponseCode()` |

---

## The Golden Rule

> **Use `url.openStream()` for simple reading. Use `URLConnection` for headers. Use `HttpURLConnection` for HTTP-specific features (GET, POST, response codes). Always handle IOExceptions and close streams.**

**Memory trick:**
```
URL = Address
openStream() = Open door
BufferedReader = Read sign inside
readLine() = Read one line at a time

openStream() → InputStreamReader → BufferedReader → readLine() → Done!
```