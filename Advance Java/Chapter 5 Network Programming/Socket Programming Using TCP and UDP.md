Here's the **complete code with detailed comments** explaining what each part does, plus a brief explanation of what each program is.

---

## What is TCP Socket Programming?

**TCP (Transmission Control Protocol)** is a connection-oriented protocol that provides reliable, ordered, and error-checked delivery of data. Think of it like making a phone call - you dial, wait for answer, talk, then hang up. Both sides know the connection exists.

---

### TCP Server (Waits for clients)

```java
import java.io.*;   // For input/output streams (reading/writing data)
import java.net.*;  // For networking classes (Socket, ServerSocket)

public class TCPServer {
    public static void main(String[] args) throws IOException {
        
        // Step 1: Create a ServerSocket on port 5000
        // This "binds" the server to listen for incoming connections on port 5000
        // Port 5000 is like a door number - clients need this number to find us
        ServerSocket server = new ServerSocket(5000);
        
        // Print message to show server is running and waiting
        System.out.println("Server waiting on port 5000...");
        
        // Step 2: Wait for a client to connect (this line BLOCKS execution)
        // .accept() pauses the program until a client tries to connect
        // When a client connects, it returns a Socket object for that specific client
        Socket client = server.accept();
        
        // Print message when a client successfully connects
        System.out.println("Client connected!");
        
        // Step 3: Create an output stream to send data TO the client
        // getOutputStream() gets the stream that sends data
        // PrintWriter wraps it to easily send text (println method)
        // true enables auto-flush (sends immediately, not buffered)
        PrintWriter out = new PrintWriter(client.getOutputStream(), true);
        
        // Step 4: Send a message to the client
        // println() sends the string to the client
        out.println("Hello from server!");
        
        // Step 5: Close the client connection
        // Releases system resources associated with this client
        client.close();
        
        // Step 6: Close the server socket
        // Stops listening for new connections
        server.close();
    }
}
```

```java
import java.io.*;
import java.net.*;

public class TCPServer {
    public static void main(String[] args) throws IOException {
        
        ServerSocket server = new ServerSocket(5000);
        
        System.out.println("Server waiting on port 5000...");
        
        Socket client = server.accept();
        
        System.out.println("Client connected!");
        
        PrintWriter out = new PrintWriter(client.getOutputStream(), true);
        
        out.println("Hello from server!");
        
        
        client.close();
        server.close();
    }
}
```
---

### TCP Client (Connects to server)

```java
import java.io.*;   // For input/output streams
import java.net.*;  // For Socket class

public class TCPClient {
    public static void main(String[] args) throws IOException {
        
        // Step 1: Create a Socket and connect to server
        // "localhost" means the same computer (use IP address for remote)
        // 5000 is the port number the server is listening on
        // This line attempts to establish a TCP connection with the server
        Socket socket = new Socket("localhost", 5000);
        
        // Print message confirming connection
        System.out.println("Connected to server!");
        
        // Step 2: Create an input stream to read data FROM the server
        // getInputStream() gets the stream receiving data from server
        // InputStreamReader converts bytes to characters
        // BufferedReader allows efficient reading line-by-line
        BufferedReader in = new BufferedReader(
            new InputStreamReader(socket.getInputStream())
        );
        
        // Step 3: Read a line of text sent by the server
        // readLine() waits until a full line is received (blocks)
        // Returns null if connection is closed
        String message = in.readLine();
        
        // Step 4: Print the message received from server
        System.out.println("Server: " + message);
        
        // Step 5: Close the socket connection
        // Releases network resources
        socket.close();
    }
}
```


``` java 
import java.io.*;
import java.net.*;

public class TCPClient {
    public static void main(String[] args) throws IOException {
        
        Socket socket = new Socket("localhost", 5000);
        
        System.out.println("Connected to server!");
        
        BufferedReader in = new BufferedReader(
            new InputStreamReader(socket.getInputStream())
        );
        
        String message = in.readLine();
        
        System.out.println("Server: " + message);
        
        socket.close();
    }
}
```

**How to run TCP:**
```
1. First run:  java TCPServer    (starts waiting)
2. Then run:   java TCPClient     (connects and exchanges message)
```

---

## What is UDP Socket Programming?

**UDP (User Datagram Protocol)** is a connectionless protocol that sends independent packets of data. Think of it like sending a letter - you drop it in the mailbox and don't know if it arrives. No connection is established beforehand.

---

### UDP Sender (Sends packets)

```java
import java.net.*;  // For DatagramSocket, DatagramPacket, InetAddress

public class UDPSender {
    public static void main(String[] args) throws Exception {
        
        // Step 1: Create a DatagramSocket
        // This is the UDP equivalent of a phone - can send and receive packets
        // No port specified means the system assigns an available port automatically
        DatagramSocket socket = new DatagramSocket();
        
        // Step 2: Prepare the message to send
        String message = "Hello via UDP!";
        
        // Step 3: Convert String to bytes (network transmits raw bytes, not text)
        byte[] data = message.getBytes();
        
        // Step 4: Get the destination address
        // InetAddress represents an IP address
        // "localhost" = 127.0.0.1 (this same computer)
        InetAddress address = InetAddress.getByName("localhost");
        
        // Step 5: Create a DatagramPacket (the actual "letter")
        // Parameters:
        //   - data: the byte array to send
        //   - data.length: how many bytes to send
        //   - address: destination IP address
        //   - 7000: destination port number (receiver must listen on this port)
        DatagramPacket packet = new DatagramPacket(data, data.length, address, 7000);
        
        // Step 6: Send the packet through the socket
        // This is like dropping the letter in a mailbox
        // No confirmation that it arrived!
        socket.send(packet);
        
        // Step 7: Print confirmation of send (not delivery confirmation)
        System.out.println("Packet sent!");
        
        // Step 8: Close the socket (release resources)
        socket.close();
    }
}
```

---

### UDP Receiver (Listens for packets)

```java
import java.net.*;  // For DatagramSocket, DatagramPacket

public class UDPReceiver {
    public static void main(String[] args) throws Exception {
        
        // Step 1: Create a DatagramSocket bound to port 7000
        // This "listens" for incoming packets on port 7000
        // Think of it as sitting by a specific mailbox
        DatagramSocket socket = new DatagramSocket(7000);
        
        // Step 2: Create a buffer to hold incoming data
        // 1024 bytes is enough for most small messages
        byte[] buffer = new byte[1024];
        
        // Step 3: Create an empty packet to receive data into
        // The buffer will be filled when a packet arrives
        DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
        
        // Step 4: Wait for a packet to arrive (this line BLOCKS)
        // .receive() pauses the program until a packet arrives
        // When a packet arrives, it fills the packet object with data
        System.out.println("Waiting for UDP packet on port 7000...");
        socket.receive(packet);  // Blocks until packet arrives
        
        // Step 5: Extract the data from the packet
        // packet.getData() returns the byte array
        // packet.getLength() returns how many bytes were actually received
        // Create a String from those bytes (convert bytes to text)
        String message = new String(packet.getData(), 0, packet.getLength());
        
        // Step 6: Print the received message
        System.out.println("Received: " + message);
        
        // Step 7: Close the socket (stop listening)
        socket.close();
    }
}
```

**How to run UDP:**
```
1. First run:  java UDPReceiver   (starts listening on port 7000)
2. Then run:   java UDPSender      (sends packet to port 7000)
```

---

## Quick Reference Table

| TCP | UDP |
|-----|-----|
| `ServerSocket server = new ServerSocket(port)` | `DatagramSocket socket = new DatagramSocket(port)` |
| `Socket client = server.accept()` | `socket.receive(packet)` |
| `Socket socket = new Socket(host, port)` | `socket.send(packet)` |
| `PrintWriter out = new PrintWriter(socket.getOutputStream(), true)` | `DatagramPacket packet = new DatagramPacket(data, len, addr, port)` |
| `BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()))` | `byte[] buffer = packet.getData()` |

---

## The Golden Rule

> **TCP creates a connection before sending data (like a phone call). UDP just throws packets (like letters). Use TCP when data MUST arrive intact (web, email). Use UDP when speed matters more than reliability (gaming, streaming).**

**Memory trick:**
```
TCP = "Talking Phone Call" (reliable, connected)
UDP = "Unsigned Dropped Parcel" (fast, no confirmation)

ServerSocket = "I wait by the phone"
accept() = "Pick up when it rings"
DatagramSocket = "I check the mailbox"
receive() = "Wait for a letter"
```