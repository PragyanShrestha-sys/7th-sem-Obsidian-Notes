Here's a **complete explanation** of working with URLs in Java.

---

## What is a URL?

**URL** = **Uniform Resource Locator** (web address)

```
https://www.example.com:8080/products?id=123#section
  │          │           │      │        │        │
  │          │           │      │        │        └── Fragment
  │          │           │      │        └── Query
  │          │           │      └── Path
  │          │           └── Port
  │          └── Host
  └── Protocol
```

**Analogy:** URL is like a complete mailing address (country, city, street, house, apartment).

---

## Why Work with URLs?

| Need                     | Explanation                        |
| ------------------------ | ---------------------------------- |
| **Download web content** | Read HTML, JSON, XML from websites |
| **Call web APIs**        | Get data from REST services        |
| **Access resources**     | Read files from internet           |
| **Web scraping**         | Extract data from web pages        |

---

## Java URL Classes

| Class | Purpose |
|-------|---------|
| `URL` | Represents a web address |
| `URLConnection` | Connection to URL |
| `HttpURLConnection` | HTTP-specific connection |
| `URLDecoder` | Decode URL encoded strings |
| `URLEncoder` | Encode strings for URLs |

---

## 1. URL Class (Basic)

### Creating URL Objects

```java
import java.net.*;
import java.io.*;

public class URLDemo {
    public static void main(String[] args) throws MalformedURLException {
        
        // Way 1: Direct string
        URL url1 = new URL("https://www.google.com");
        
        // Way 2: Protocol + host + file
        URL url2 = new URL("https", "www.google.com", "/search");
        
        // Way 3: Protocol + host + port + file
        URL url3 = new URL("https", "www.google.com", 8080, "/search");
        
        System.out.println("URL: " + url1.toString());
    }
}
```
---
## 1.1. Creating a relative URL 

![[Pasted image 20260607074805.png]]

---

### Getting URL Components

```java
import java.net.*;

public class URLComponents {
    public static void main(String[] args) throws MalformedURLException {
        
        URL url = new URL("https://www.example.com:8080/products?id=123#reviews");
        
        System.out.println("Protocol: " + url.getProtocol());     // https
        System.out.println("Host: " + url.getHost());             // www.example.com
        System.out.println("Port: " + url.getPort());             // 8080
        System.out.println("Path: " + url.getPath());             // /products
        System.out.println("Query: " + url.getQuery());           // id=123
        System.out.println("File: " + url.getFile());             // /products?id=123
        System.out.println("Ref: " + url.getRef());               // reviews
        System.out.println("Authority: " + url.getAuthority());   // www.example.com:8080
    }
}
```

**Output:**
```
Protocol: https
Host: www.example.com
Port: 8080
Path: /products
Query: id=123
File: /products?id=123
Ref: reviews
Authority: www.example.com:8080
```

---

## 4. URL Encoder/Decoder

### Why URL Encoding?

**Some characters are not allowed in URLs** (spaces, symbols). They must be encoded.

| Character | Encoded |
|-----------|---------|
| Space | `%20` or `+` |
| `&` | `%26` |
| `=` | `%3D` |
| `?` | `%3F` |
| `#` | `%23` |

### Encoding Example

```java
import java.net.*;
import java.io.*;

public class URLEncodeDecode {
    public static void main(String[] args) {
        try {
            // Encoding
            String query = "Java Programming & Tutorials";
            String encoded = URLEncoder.encode(query, "UTF-8");
            System.out.println("Original: " + query);
            System.out.println("Encoded: " + encoded);
            
            // Decoding
            String encoded2 = "Java+Programming+%26+Tutorials";
            String decoded = URLDecoder.decode(encoded2, "UTF-8");
            System.out.println("Encoded: " + encoded2);
            System.out.println("Decoded: " + decoded);
            
            // Building a complete URL with parameters
            String baseURL = "https://www.google.com/search";
            String params = "q=" + URLEncoder.encode("java networking", "UTF-8");
            String fullURL = baseURL + "?" + params;
            System.out.println("Full URL: " + fullURL);
            
        } catch (UnsupportedEncodingException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Original: Java Programming & Tutorials
Encoded: Java+Programming+%26+Tutorials
Encoded: Java+Programming+%26+Tutorials
Decoded: Java Programming & Tutorials
Full URL: https://www.google.com/search?q=java+networking
```

---
## [[HTTP Response Codes (Common)]]

---

## Common URL Methods Summary

| Method             | What it returns             |
| ------------------ | --------------------------- |
| `getProtocol()`    | http, https, ftp            |
| `getHost()`        | Domain name                 |
| `getPort()`        | Port number (-1 if default) |
| `getPath()`        | /path/to/file               |
| `getQuery()`       | key=value&key2=value2       |
| `openStream()`     | InputStream to read content |
| `openConnection()` | URLConnection object        |

---
## Reading from URL

![[Pasted image 20260607075556.png]]


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

note: Mathi basically website ma connect garyo (`url.openStream()`), ani tesko content transalte garyo (`InputStreamReader` → Converts bytes to characters) then  import  large chunks of data at a time (new BufferedReader(...)), then output for the user line by line (while statementwhile ((line = reader.readLine()) != null) )

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
[[Above code explanation]]

``` java
Website
    │
    │ (sends raw bytes: 72, 101, 108, 108, 111)
    │
    ▼
url.openStream()
    │
    │ (raw bytes)
    │
    ▼
InputStreamReader
    │
    │ (converts to characters: H, e, l, l, o)
    │
    ▼
BufferedReader
    │
    │ (groups into lines: "Hello")
    │
    ▼
Your Program
```

---

## The Golden Rule

> **URL class represents a web address. Use `openStream()` for simple reading, `HttpURLConnection` for HTTP requests (GET, POST), and `URLEncoder/URLDecoder` for handling special characters in URLs.**

**Memory trick:**
```
URL = Web address
openStream() = "Give me the content"
HttpURLConnection = "I control HTTP requests"
GET = Read data
POST = Send data
URLEncoder = Make URL safe (spaces → %20)
```