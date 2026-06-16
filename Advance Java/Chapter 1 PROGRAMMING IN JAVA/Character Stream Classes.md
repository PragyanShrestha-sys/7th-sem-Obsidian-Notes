Here's a **detailed explanation** of Character Stream Classes in Java.

---
![[Pasted image 20260604065035.png]]
## What are Character Streams?

**Character streams** are specifically designed for reading and writing **text data** (characters), handling Unicode properly.

```
Data Flow:
Text File → FileReader → reads characters → Your Program
Your Program → FileWriter → writes characters → Text File
```

**Key concept:** Character streams automatically handle character encoding (ASCII, UTF-8, UTF-16, etc.) - you don't need to convert bytes to characters manually.

---

## Character Stream vs Byte Stream

| Aspect | Byte Stream | Character Stream |
|--------|-------------|------------------|
| **Unit** | 1 byte | 1 character (2 bytes) |
| **Best for** | Images, audio, video | Text files |
| **Encoding** | No (raw bytes) | Yes (Unicode aware) |
| **Parent classes** | `InputStream`, `OutputStream` | `Reader`, `Writer` |

```java
// Byte stream - reads raw bytes
FileInputStream fis = new FileInputStream("data.txt");  // Works but messy for text

// Character stream - reads text properly
FileReader fr = new FileReader("data.txt");  // Clean, handles Unicode
```

---

## Main Character Stream Classes

| Class | Purpose | Mode |
|-------|---------|------|
| **FileReader** | Read characters from a text file | Input (read) |
| **FileWriter** | Write characters to a text file | Output (write) |
| **BufferedReader** | Read text efficiently (with buffering) | Input (read) |
| **PrintWriter** | Write text with formatting | Output (write) |

---

## 1. FileReader (Reading Characters)

### Basic Methods:

| Method | What it does |
|--------|--------------|
| `read()` | Reads ONE character (returns int 0-65535, or -1 at end) |
| `read(char[] buffer)` | Reads multiple characters into array |
| `close()` | Closes the reader |

### Example 1: Reading One Character at a Time

```java
import java.io.*;

public class ReadOneChar {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("hello.txt")) {
            
            int charValue;
            // Read until end of file (-1 means EOF)
            while ((charValue = fr.read()) != -1) {
                char c = (char) charValue;
                System.out.print(c);
            }
            
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
}
```

**If hello.txt contains:** "Hello World"

**Output:** "Hello World"

### Example 2: Reading Multiple Characters (More Efficient)

```java
import java.io.*;

public class ReadMultipleChars {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("story.txt")) {
            
            char[] buffer = new char[1024];  // 1KB character buffer
            int charsRead;
            
            while ((charsRead = fr.read(buffer)) != -1) {
                // Process only the characters actually read
                String chunk = new String(buffer, 0, charsRead);
                System.out.print(chunk);
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 2. FileWriter (Writing Characters)

### Basic Methods:

| Method | What it does |
|--------|--------------|
| `write(int c)` | Writes ONE character |
| `write(char[] buffer)` | Writes character array |
| `write(String str)` | Writes a string |
| `write(String str, int offset, int length)` | Writes part of a string |
| `flush()` | Forces write to disk |
| `close()` | Closes the writer |

### Example 1: Writing One Character at a Time

```java
import java.io.*;

public class WriteOneChar {
    public static void main(String[] args) {
        try (FileWriter fw = new FileWriter("output.txt")) {
            
            // Write individual characters
            fw.write('H');
            fw.write('e');
            fw.write('l');
            fw.write('l');
            fw.write('o');
            
            System.out.println("Data written successfully!");
            
        } catch (IOException e) {
            System.out.println("Error writing: " + e.getMessage());
        }
    }
}
```

### Example 2: Writing Strings

```java
import java.io.*;

public class WriteString {
    public static void main(String[] args) {
        try (FileWriter fw = new FileWriter("message.txt")) {
            
            String[] lines = {
                "First line of text",
                "Second line of text",
                "Third line of text"
            };
            
            for (String line : lines) {
                fw.write(line);
                fw.write("\n");  // Add newline
            }
            
            System.out.println("String written successfully!");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

### Example 3: Append Mode (Add to existing file)

```java
import java.io.*;

public class AppendToTextFile {
    public static void main(String[] args) {
        // Second parameter 'true' enables append mode
        try (FileWriter fw = new FileWriter("log.txt", true)) {
            
            String logEntry = "[" + new java.util.Date() + "] Application started\n";
            fw.write(logEntry);
            
            System.out.println("Appended to log file");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 3. BufferedReader (Efficient Reading)

**Why use BufferedReader?** Reading one character at a time is slow. BufferedReader reads chunks of text and caches it.

### Example 1: Reading Line by Line

```java
import java.io.*;

public class ReadLineByLine {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
            
            String line;
            int lineNumber = 1;
            
            // readLine() returns null at end of file
            while ((line = br.readLine()) != null) {
                System.out.println(lineNumber + ": " + line);
                lineNumber++;
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

### Example 2: Reading CSV File

```java
import java.io.*;

public class ReadCSV {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("employees.csv"))) {
            
            String line;
            // Skip header
            br.readLine();
            
            while ((line = br.readLine()) != null) {
                String[] fields = line.split(",");
                System.out.println("Name: " + fields[0] + 
                                 ", Age: " + fields[1] + 
                                 ", Department: " + fields[2]);
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 4. PrintWriter (Formatted Writing)

**Why use PrintWriter?** Provides convenient methods like `print()`, `println()`, and `printf()` (similar to `System.out`).

### Example 1: Basic PrintWriter

```java
import java.io.*;

public class PrintWriterExample {
    public static void main(String[] args) {
        try (PrintWriter pw = new PrintWriter(new FileWriter("report.txt"))) {
            
            pw.println("=== Employee Report ===");
            pw.println();  // Empty line
            pw.println("Name: John Doe");
            pw.println("Age: 30");
            pw.println("Salary: $75,000");
            pw.println("Department: IT");
            
            // Using printf for formatted output
            pw.printf("Total employees: %d\n", 25);
            pw.printf("Average salary: $%.2f\n", 65000.50);
            
            System.out.println("Report generated successfully!");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

### Example 2: Auto-flush mode

```java
import java.io.*;

public class AutoFlushExample {
    public static void main(String[] args) {
        // Second parameter 'true' enables auto-flush
        try (PrintWriter pw = new PrintWriter(new FileWriter("log.txt"), true)) {
            
            pw.println("This will be flushed immediately");
            pw.println("No need to call flush() manually");
            
            // Auto-flush happens after each println()
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## Complete Example: Text File Processor

```java
import java.io.*;

public class TextFileProcessor {
    
    // Method to count lines, words, characters
    public static void analyzeFile(String filename) {
        try (BufferedReader br = new BufferedReader(new FileReader(filename))) {
            
            int lines = 0;
            int words = 0;
            int characters = 0;
            String line;
            
            while ((line = br.readLine()) != null) {
                lines++;
                characters += line.length();
                
                // Split by spaces and punctuation (simple approach)
                String[] wordArray = line.split("[\\s\\p{Punct}]+");
                words += wordArray.length;
            }
            
            System.out.println("File: " + filename);
            System.out.println("Lines: " + lines);
            System.out.println("Words: " + words);
            System.out.println("Characters: " + characters);
            
        } catch (IOException e) {
            System.out.println("Error analyzing file: " + e.getMessage());
        }
    }
    
    // Method to search for text in file
    public static void searchInFile(String filename, String searchTerm) {
        try (BufferedReader br = new BufferedReader(new FileReader(filename))) {
            
            String line;
            int lineNumber = 1;
            int occurrences = 0;
            
            while ((line = br.readLine()) != null) {
                if (line.contains(searchTerm)) {
                    System.out.println("Line " + lineNumber + ": " + line);
                    occurrences++;
                }
                lineNumber++;
            }
            
            System.out.println("Found " + occurrences + " occurrences of '" + searchTerm + "'");
            
        } catch (IOException e) {
            System.out.println("Error searching file: " + e.getMessage());
        }
    }
    
    // Method to create formatted report
    public static void createReport(String outputFile, String[] data) {
        try (PrintWriter pw = new PrintWriter(new FileWriter(outputFile))) {
            
            pw.println("=" .repeat(50));
            pw.println("DATA REPORT");
            pw.println("=" .repeat(50));
            pw.println();
            
            for (int i = 0; i < data.length; i++) {
                pw.printf("%3d. %s\n", i + 1, data[i]);
            }
            
            pw.println();
            pw.println("Total records: " + data.length);
            pw.println("Generated on: " + new java.util.Date());
            
            System.out.println("Report created: " + outputFile);
            
        } catch (IOException e) {
            System.out.println("Error creating report: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        // Analyze a text file
        analyzeFile("document.txt");
        
        // Search for text
        searchInFile("document.txt", "Java");
        
        // Create a report
        String[] employees = {"Alice Johnson", "Bob Smith", "Carol Davis"};
        createReport("employees_report.txt", employees);
    }
}
```

---

## The Reader Hierarchy

```
Reader (abstract parent)
├── InputStreamReader    ← Bridge from byte to character
│   └── FileReader       ← Read text from file
├── BufferedReader       ← Add buffering (faster, readLine)
├── StringReader         ← Read from String in memory
├── CharArrayReader      ← Read from char array
└── FilterReader         ← Base for filtering
```

---

## The Writer Hierarchy

```
Writer (abstract parent)
├── OutputStreamWriter   ← Bridge from character to byte
│   └── FileWriter       ← Write text to file
├── BufferedWriter       ← Add buffering (faster)
├── PrintWriter          ← Formatted writing (println, printf)
├── StringWriter         ← Write to String in memory
├── CharArrayWriter      ← Write to char array
└── FilterWriter         ← Base for filtering
```

---

## Buffered vs Unbuffered Performance

```java
// ❌ SLOW - No buffering, each character is a disk operation
try (FileReader fr = new FileReader("bigfile.txt")) {
    int c;
    while ((c = fr.read()) != -1) {  // Every read hits disk
        // process character
    }
}

// ✅ FAST - With buffering
try (BufferedReader br = new BufferedReader(new FileReader("bigfile.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {  // Reads chunks at a time
        // process line
    }
}
```

**Performance difference:** Buffered can be 10-100x faster!

---

## Character Encoding (Important!)

```java
// Default encoding (platform dependent - may cause issues)
FileReader fr = new FileReader("file.txt");

// Specify encoding (Java 11+)
import java.nio.charset.StandardCharsets;

try (FileReader fr = new FileReader("file.txt", StandardCharsets.UTF_8)) {
    // Read with UTF-8 encoding
}

// Alternative using InputStreamReader (Java 8+)
try (BufferedReader br = new BufferedReader(
         new InputStreamReader(new FileInputStream("file.txt"), "UTF-8"))) {
    // Read with explicit encoding
}
```

---

## Complete Example: Log File Analyzer

```java
import java.io.*;
import java.util.*;

public class LogAnalyzer {
    
    public static void analyzeLog(String logFile, String outputFile) {
        Map<String, Integer> errorCounts = new HashMap<>();
        int totalErrors = 0;
        
        try (BufferedReader br = new BufferedReader(new FileReader(logFile))) {
            String line;
            
            while ((line = br.readLine()) != null) {
                if (line.contains("ERROR")) {
                    totalErrors++;
                    
                    // Extract error type
                    String errorType = extractErrorType(line);
                    errorCounts.put(errorType, errorCounts.getOrDefault(errorType, 0) + 1);
                }
            }
            
        } catch (IOException e) {
            System.out.println("Error reading log: " + e.getMessage());
        }
        
        // Write report
        try (PrintWriter pw = new PrintWriter(new FileWriter(outputFile))) {
            pw.println("=== ERROR ANALYSIS REPORT ===");
            pw.println("Date: " + new java.util.Date());
            pw.println();
            pw.println("Total Errors: " + totalErrors);
            pw.println();
            pw.println("Error Breakdown:");
            
            for (Map.Entry<String, Integer> entry : errorCounts.entrySet()) {
                pw.printf("  %s: %d\n", entry.getKey(), entry.getValue());
            }
            
        } catch (IOException e) {
            System.out.println("Error writing report: " + e.getMessage());
        }
    }
    
    private static String extractErrorType(String line) {
        // Simple extraction - look for error pattern
        if (line.contains("NullPointerException")) return "NullPointer";
        if (line.contains("IOException")) return "IO Error";
        if (line.contains("SQLException")) return "Database Error";
        return "Other Error";
    }
    
    public static void main(String[] args) {
        analyzeLog("application.log", "error_report.txt");
        System.out.println("Analysis complete!");
    }
}
```

---

## Common Use Cases

| Use Case | Character Stream Class |
|----------|------------------------|
| **Read configuration file** | `BufferedReader` + `FileReader` |
| **Write log file** | `PrintWriter` + `FileWriter` |
| **Process CSV data** | `BufferedReader` |
| **Generate reports** | `PrintWriter` |
| **Copy text file** | `FileReader` + `FileWriter` |
| **Count lines/words** | `BufferedReader` |

---

## Quick Reference

```java
// BASIC READING
try (FileReader fr = new FileReader("file.txt")) {
    int c;
    while ((c = fr.read()) != -1) {
        System.out.print((char)c);
    }
}

// EFFICIENT READING (recommended)
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
}

// BASIC WRITING
try (FileWriter fw = new FileWriter("output.txt")) {
    fw.write("Hello World");
}

// FORMATTED WRITING (recommended)
try (PrintWriter pw = new PrintWriter(new FileWriter("output.txt"))) {
    pw.println("Hello World");
    pw.printf("Value: %d\n", 42);
}

// APPEND MODE
try (FileWriter fw = new FileWriter("log.txt", true)) {
    fw.write("New line appended\n");
}
```

---

## The Golden Rule

> **Character streams are for TEXT files only! Use `BufferedReader` for efficient reading (readLine() method), and `PrintWriter` for convenient writing (println(), printf()). Always specify character encoding for cross-platform compatibility.**

**Memory trick:**
```
Reader = "Read characters from text"
Writer = "Write characters to text"
BufferedReader = "Buffer + readLine() = efficient line-by-line reading"
PrintWriter = "Print + write = convenient formatted output"
```

Would you like me to explain **character encoding** (UTF-8, UTF-16, etc.) or **RandomAccessFile** next?