## Socket Programming - Complete Explanation with Comments

### What Each Component Does

| Component | Purpose |
|-----------|---------|
| **Socket** | Establishes a communication link between client and server over network |
| **InputStream** | Reads data **from** the socket (receiving data) |
| **OutputStream** | Writes data **to** the socket (sending data) |
| **readInt()** | Reads 4 bytes from stream and converts to integer |
| **writeInt()** | Converts integer to 4 bytes and writes to stream |

## Annotated Server Code

```java
import java.net.*;  // For Socket, ServerSocket classes
import java.io.*;   // For InputStream, OutputStream classes

public class Server {
    public static void main(String[] args) throws Exception {
        
        // 1. CREATE SERVER SOCKET
        // Binds to port 9999 and listens for incoming connections
        // Port number identifies which application on the machine
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("Server is running on port 9999...");
        
        // 2. ACCEPT CLIENT CONNECTION
        // Blocks (waits) until a client connects
        // Returns a Socket object for communication with that specific client
        Socket clientSocket = serverSocket.accept();
        System.out.println("Client connected from: " + clientSocket.getInetAddress());
        
        // 3. GET INPUT STREAM (for receiving data from client)
        // InputStream reads data sent by the client
        // DataInputStream adds methods like readInt() for primitive types
        DataInputStream dataInput = new DataInputStream(clientSocket.getInputStream());
        
        // 4. GET OUTPUT STREAM (for sending data to client)
        // OutputStream writes data to be sent to the client
        // DataOutputStream adds methods like writeInt() for primitive types
        DataOutputStream dataOutput = new DataOutputStream(clientSocket.getOutputStream());
        
        // 5. RECEIVE TWO INTEGERS FROM CLIENT
        // readInt() reads 4 bytes from the stream and constructs an integer
        // Blocks until 4 bytes are received
        int firstNumber = dataInput.readInt();  // Reads first integer from client
        System.out.println("Received first number: " + firstNumber);
        //note : `readInt()` 'readUTF()'(forstring) Automatically Reads the Next Available Data
        int secondNumber = dataInput.readInt(); // Reads second integer from client
        System.out.println("Received second number: " + secondNumber);
        
        // 6. CALCULATE GREATEST
        // Math.max() returns the larger of two numbers
        int greatest = Math.max(firstNumber, secondNumber);
        
        // 7. SEND RESULT BACK TO CLIENT
        // writeInt() converts integer to 4 bytes and sends through OutputStream
        dataOutput.writeInt(greatest);
        System.out.println("Sent greatest number: " + greatest);
        
        // 8. CLOSE ALL RESOURCES
        // Important to free up system resources
        clientSocket.close();   // Close connection with this client
        serverSocket.close();   // Stop listening for new connections
        System.out.println("Server closed.");
    }
}
```

## Annotated Client Code

```java
import java.net.*;  // For Socket class
import java.io.*;   // For InputStream, OutputStream classes

public class Client {
    public static void main(String[] args) throws Exception {
        
        // 1. CREATE CLIENT SOCKET
        // Connects to server at "localhost" (127.0.0.1) on port 9999
        // localhost means same machine (for testing)
        Socket socket = new Socket("localhost", 9999);
        System.out.println("Connected to server!");
        
        // 2. GET OUTPUT STREAM (to send data to server)
        // OutputStream writes data that will be sent to the server
        DataOutputStream dataOutput = new DataOutputStream(socket.getOutputStream());
        
        // 3. GET INPUT STREAM (to receive data from server)
        // InputStream reads data sent by the server
        DataInputStream dataInput = new DataInputStream(socket.getInputStream());
        
        // 4. SEND TWO INTEGERS TO SERVER
        int number1 = 25;  // First number to send
        int number2 = 42;  // Second number to send
        
        System.out.println("Sending numbers: " + number1 + " and " + number2);
        
        // writeInt() converts each integer to 4 bytes and sends through OutputStream
        dataOutput.writeInt(number1);  // Sends 4 bytes representing 25
        dataOutput.writeInt(number2);  // Sends 4 bytes representing 42
        
        // 5. RECEIVE RESULT FROM SERVER
        // readInt() reads 4 bytes and constructs the integer
        int result = dataInput.readInt();  // Blocks until 4 bytes are received
        System.out.println("Greatest number from server: " + result);
        
        // 6. CLOSE CONNECTION
        socket.close();  // Closes the connection to server
        System.out.println("Client closed.");
    }
}
```

## Visual Data Flow Diagram

```
CLIENT                                  SERVER
┌─────────────┐                        ┌─────────────┐
│  25, 42     │                        │             │
│             │    ──── Socket ────►   │  readInt()  │
│  writeInt() │                        │  readInt()  │
│  writeInt() │                        │             │
│             │    ◄─── Socket ────    │  max(25,42) │
│  readInt()  │                        │  writeInt() │
│             │                        │             │
└─────────────┘                        └─────────────┘
    Result: 42                              Result: 42
```

## How Data Flows (Byte Level)

```java
// When you write:
dataOutput.writeInt(25);

// Internally converts to 4 bytes:
// [0][0][0][25]  (big-endian format)

// Network transmits these 4 bytes

// Server reads:
dataInput.readInt();
// Reads 4 bytes and reconstructs integer: 25
```

## Complete Working Code with Comments

### Server.java
```java
import java.net.*;
import java.io.*;

public class Server {
    public static void main(String[] args) throws Exception {
        // Create server socket on port 9999
        ServerSocket serverSocket = new ServerSocket(9999);
        System.out.println("Server waiting for client...");
        
        // Accept client connection
        Socket clientSocket = serverSocket.accept();
        System.out.println("Client connected!");
        
        // Create streams for communication
        DataInputStream in = new DataInputStream(clientSocket.getInputStream());
        DataOutputStream out = new DataOutputStream(clientSocket.getOutputStream());
        
        // Receive numbers
        int a = in.readInt();  // Read first number (4 bytes)
        int b = in.readInt();  // Read second number (4 bytes)
        System.out.println("Received: " + a + ", " + b);
        
        // Calculate and send result
        out.writeInt(Math.max(a, b));  // Send greatest number (4 bytes)
        System.out.println("Sent: " + Math.max(a, b));
        
        // Close resources
        clientSocket.close();
        serverSocket.close();
    }
}
```

### Client.java
```java
import java.net.*;
import java.io.*;

public class Client {
    public static void main(String[] args) throws Exception {
        // Connect to server
        Socket socket = new Socket("localhost", 9999);
        System.out.println("Connected to server!");
        
        // Create streams
        DataOutputStream out = new DataOutputStream(socket.getOutputStream());
        DataInputStream in = new DataInputStream(socket.getInputStream());
        
        // Send two numbers
        int num1 = 25, num2 = 42;
        out.writeInt(num1);  // Send 25 as 4 bytes
        out.writeInt(num2);  // Send 42 as 4 bytes
        System.out.println("Sent: " + num1 + ", " + num2);
        
        // Receive and display result
        int result = in.readInt();  // Read 4 bytes as integer
        System.out.println("Greatest number: " + result);
        
        // Close socket
        socket.close();
    }
}
```

## Key Points to Remember

1. **Socket** = Communication endpoint between client and server
2. **InputStream** = Receives data (read from socket)
3. **OutputStream** = Sends data (write to socket)
4. **readInt()** = Reads 4 bytes → converts to int
5. **writeInt()** = Converts int → writes 4 bytes
6. **Blocking**: Methods like `accept()`, `readInt()` wait until data arrives
7. **Order matters**: Must read in same order data was written
8. **Always close resources** to free system resources