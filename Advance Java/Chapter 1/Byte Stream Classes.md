Here's a **detailed explanation** of Byte Stream Classes in Java.

---
![[Pasted image 20260604065053.png]]
## What are Byte Streams?

**Byte streams** are used to read and write **raw binary data** (individual bytes) to/from files or other sources.

```
Data Flow:
File (binary data) → FileInputStream → reads byte by byte → Your Program
Your Program → FileOutputStream → writes byte by byte → File (binary data)
```

**Key concept:** Everything in a file is ultimately bytes. Byte streams don't interpret data - they just move raw bytes.

---

## The Two Main Byte Stream Classes

| Class | Purpose | Mode |
|-------|---------|------|
| **FileInputStream** | Read bytes FROM a file | Input (read) |
| **FileOutputStream** | Write bytes TO a file | Output (write) |

---

## 1. FileInputStream (Reading Bytes)

### Basic Methods:

| Method | What it does |
|--------|--------------|
| `read()` | Reads ONE byte (returns int 0-255, or -1 at end) |
| `read(byte[] buffer)` | Reads multiple bytes into array |
| `close()` | Closes the stream (releases system resources) |

### Example 1: Reading One Byte at a Time

```java
import java.io.*;

public class ReadOneByte {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("data.bin")) {
            
            int byteValue;
            // Read until end of file (-1 means EOF)
            while ((byteValue = fis.read()) != -1) {
                System.out.println("Byte: " + byteValue);
                System.out.println("As char: " + (char) byteValue);
            }
            
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
}
```

### Example 2: Reading Multiple Bytes at Once (More Efficient)

```java
import java.io.*;

public class ReadMultipleBytes {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("data.bin")) {
            
            byte[] buffer = new byte[1024];  // 1KB buffer
            int bytesRead;
            
            while ((bytesRead = fis.read(buffer)) != -1) {
                System.out.println("Read " + bytesRead + " bytes");
                
                // Process only the bytes actually read
                for (int i = 0; i < bytesRead; i++) {
                    System.out.print(buffer[i] + " ");
                }
                System.out.println();
            }
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

### Example 3: Reading a Binary File (Image)

```java
import java.io.*;

public class CopyImage {
    public static void main(String[] args) {
        // Copy an image file using byte streams
        try (FileInputStream fis = new FileInputStream("original.jpg");
             FileOutputStream fos = new FileOutputStream("copy.jpg")) {
            
            byte[] buffer = new byte[4096];  // 4KB buffer
            int bytesRead;
            long totalBytes = 0;
            
            while ((bytesRead = fis.read(buffer)) != -1) {
                fos.write(buffer, 0, bytesRead);  // Write exactly what was read
                totalBytes += bytesRead;
            }
            
            System.out.println("File copied! Total bytes: " + totalBytes);
            
        } catch (FileNotFoundException e) {
            System.out.println("Source file not found!");
        } catch (IOException e) {
            System.out.println("Error during copy: " + e.getMessage());
        }
    }
}
```

---

## 2. FileOutputStream (Writing Bytes)

### Basic Methods:

| Method | What it does |
|--------|--------------|
| `write(int b)` | Writes ONE byte |
| `write(byte[] buffer)` | Writes entire byte array |
| `write(byte[] buffer, int offset, int length)` | Writes part of array |
| `flush()` | Forces any buffered data to be written |
| `close()` | Closes the stream |

### Example 1: Writing One Byte at a Time

```java
import java.io.*;

public class WriteOneByte {
    public static void main(String[] args) {
        try (FileOutputStream fos = new FileOutputStream("output.bin")) {
            
            // Write ASCII values
            fos.write(72);   // 'H'
            fos.write(101);  // 'e'
            fos.write(108);  // 'l'
            fos.write(108);  // 'l'
            fos.write(111);  // 'o'
            
            System.out.println("Data written successfully!");
            
        } catch (IOException e) {
            System.out.println("Error writing: " + e.getMessage());
        }
    }
}
```

### Example 2: Writing Byte Arrays

```java
import java.io.*;

public class WriteByteArray {
    public static void main(String[] args) {
        byte[] data = {65, 66, 67, 68, 69};  // A, B, C, D, E
        
        try (FileOutputStream fos = new FileOutputStream("alphabet.bin")) {
            
            fos.write(data);  // Write entire array
            
            // Write part of array (C, D, E)
            fos.write(data, 2, 3);
            
            System.out.println("Array written successfully!");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

### Example 3: Append Mode (Add to existing file)

```java
import java.io.*;

public class AppendToFile {
    public static void main(String[] args) {
        // Second parameter 'true' enables append mode
        try (FileOutputStream fos = new FileOutputStream("log.txt", true)) {
            
            String logEntry = "New log entry at " + System.currentTimeMillis() + "\n";
            fos.write(logEntry.getBytes());  // Convert String to bytes
            
            System.out.println("Appended to log file");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## Complete Example: File Encryption (Simple XOR)

```java
import java.io.*;

public class SimpleEncryption {
    
    // Encrypt/decrypt using XOR with a key
    public static void processFile(String inputFile, String outputFile, byte key) {
        try (FileInputStream fis = new FileInputStream(inputFile);
             FileOutputStream fos = new FileOutputStream(outputFile)) {
            
            int byteValue;
            while ((byteValue = fis.read()) != -1) {
                // XOR operation (same operation encrypts and decrypts)
                byte encrypted = (byte) (byteValue ^ key);
                fos.write(encrypted);
            }
            
            System.out.println("File processed successfully!");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        byte secretKey = 0x55;  // 85 in decimal
        
        // Encrypt a file
        processFile("secret.txt", "secret.enc", secretKey);
        System.out.println("File encrypted!");
        
        // Decrypt it back
        processFile("secret.enc", "decrypted.txt", secretKey);
        System.out.println("File decrypted!");
    }
}
```

---

## Byte Stream vs Character Stream

| Aspect | Byte Stream | Character Stream |
|--------|-------------|------------------|
| **Unit** | Bytes (1 byte) | Characters (2 bytes) |
| **Classes** | `InputStream`, `OutputStream` | `Reader`, `Writer` |
| **Best for** | Images, audio, video, binaries | Text files |
| **Encoding** | No encoding (raw bytes) | Handles Unicode |
| **Example** | `FileInputStream` | `FileReader` |

```java
// Byte stream - works with any file
FileInputStream fis = new FileInputStream("image.jpg");  // ✅ Good for images

// Character stream - for text only
FileReader fr = new FileReader("image.jpg");  // ❌ Will corrupt binary data!
```

---

## The InputStream Hierarchy

```
InputStream (abstract parent)
├── FileInputStream      ← Read from file
├── ByteArrayInputStream ← Read from byte array in memory
├── BufferedInputStream  ← Add buffering (faster)
├── DataInputStream      ← Read primitive types (int, double, etc.)
├── ObjectInputStream    ← Read objects (serialization)
└── FilterInputStream    ← Base for filtering
```

---

## The OutputStream Hierarchy

```
OutputStream (abstract parent)
├── FileOutputStream      ← Write to file
├── ByteArrayOutputStream ← Write to byte array in memory
├── BufferedOutputStream  ← Add buffering (faster)
├── DataOutputStream      ← Write primitive types
├── ObjectOutputStream    ← Write objects (serialization)
└── FilterOutputStream    ← Base for filtering
```

---

## Practical Example: File Copy Utility

```java
import java.io.*;

public class FileCopyUtility {
    
    // Copy file with different buffer sizes
    public static void copyFile(String source, String destination, int bufferSize) {
        long startTime = System.currentTimeMillis();
        
        try (FileInputStream fis = new FileInputStream(source);
             FileOutputStream fos = new FileOutputStream(destination)) {
            
            byte[] buffer = new byte[bufferSize];
            int bytesRead;
            int totalRead = 0;
            
            while ((bytesRead = fis.read(buffer)) != -1) {
                fos.write(buffer, 0, bytesRead);
                totalRead += bytesRead;
                
                // Progress indicator
                if (totalRead % (1024 * 1024) == 0) {
                    System.out.println("Copied: " + (totalRead / 1024) + " KB");
                }
            }
            
            long endTime = System.currentTimeMillis();
            System.out.println("Copied " + totalRead + " bytes in " + 
                             (endTime - startTime) + " ms");
            
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
    
    public static void main(String[] args) {
        // Copy a large file with 16KB buffer
        copyFile("largefile.dat", "copy.dat", 16384);
    }
}
```

---

## Important: Always Close Streams!

```java
// ❌ BAD - Resource leak!
FileInputStream fis = new FileInputStream("file.txt");
int data = fis.read();
// Never closed! System resources wasted.

// ✅ GOOD - Using try-with-resources (auto-closes)
try (FileInputStream fis = new FileInputStream("file.txt")) {
    int data = fis.read();
} // Automatically closed here

// ✅ GOOD - Manual closing (old style)
FileInputStream fis = null;
try {
    fis = new FileInputStream("file.txt");
    int data = fis.read();
} finally {
    if (fis != null) {
        fis.close();  // Always close in finally block
    }
}
```

---

## Common Use Cases

| Use Case | Byte Stream Class |
|----------|-------------------|
| **Copy any file** | `FileInputStream` + `FileOutputStream` |
| **Read image for processing** | `FileInputStream` |
| **Download binary file from network** | `InputStream` |
| **Upload file to server** | `OutputStream` |
| **Read encrypted data** | `FileInputStream` |
| **Write ZIP file** | `FileOutputStream` |

---

## Performance Tips

```java
// ❌ SLOW - Reading one byte at a time
int b;
while ((b = fis.read()) != -1) {  // Each read = system call
    // process
}

// ✅ FAST - Reading in chunks (buffering)
byte[] buffer = new byte[8192];  // 8KB buffer
int bytesRead;
while ((bytesRead = fis.read(buffer)) != -1) {
    // process buffer
}

// ✅ EVEN FASTER - Use BufferedInputStream
try (BufferedInputStream bis = new BufferedInputStream(new FileInputStream("file.txt"))) {
    // Auto-buffered, up to 8KB default
}
```

---

## The Golden Rule

> **Byte streams are for ANY file (text or binary). They read/write raw bytes without interpretation. Use `FileInputStream` to read, `FileOutputStream` to write, and ALWAYS close them (try-with-resources).**

**Memory trick:**
```
InputStream  = "Data flows IN to program" (read)
OutputStream = "Data flows OUT of program" (write)

FileInputStream  = "Read bytes FROM a FILE"
FileOutputStream = "Write bytes TO a FILE"
```

Would you like me to explain **BufferedInputStream/BufferedOutputStream** (for better performance) or **DataInputStream/DataOutputStream** (for reading/writing primitive types) next?