# JavaMail API: Sending and Receiving Email

Here's a **complete explanation** of the JavaMail API, what it is, why it's needed, and how to implement it with detailed code comments.

---

## What is JavaMail API?

**JavaMail API** is a Java library that provides a platform-independent framework for sending and receiving emails. Think of it as a toolkit that lets your Java application talk to mail servers.

```
Your Java App → JavaMail API → Mail Server → Recipient's Inbox
```

**Analogy:** JavaMail is like a universal postal worker. You give it a message and an address, and it handles all the details of delivering it through the right mail system.

---

## Why is JavaMail Needed?

| Need | Explanation |
|------|-------------|
| **User Registration** | Send confirmation/welcome emails |
| **Password Reset** | Email reset links to users |
| **Notifications** | Order confirmations, alerts, reminders |
| **Reports** | Email generated reports automatically |
| **Marketing** | Send newsletters to subscribers |

**Without JavaMail:** You would need to implement complex network protocols (SMTP, POP3, IMAP) yourself.

**With JavaMail:** You just create a message and call `Transport.send()`.

---

## How JavaMail Works - The Architecture

JavaMail has 4 main architectural components:

```
┌─────────────────────────────────────────────────────────────┐
│                       YOUR APPLICATION                      │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      JAVAMAIL API                           │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐          │
│  │ Session │ │ Message │ │Transport│ │  Store  │          │
│  └─────────┘ └─────────┘ └─────────┘ └─────────┘          │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   PROTOCOL PROVIDERS                        │
│         SMTP        │        POP3        │       IMAP       │
│      (Sending)      │     (Receiving)    │    (Receiving)   │
└─────────────────────────────┬───────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      MAIL SERVER                            │
│              (Gmail, Outlook, Yahoo, etc.)                  │
└─────────────────────────────────────────────────────────────┘
```

---

## The 5 Main Components of JavaMail

| Component | Purpose | Role |
|-----------|---------|------|
| **Session** | Represents a mail session with the server | Factory that creates messages and transports |
| **Message** | The actual email (subject, body, attachments) | What you send |
| **Address** | Email addresses (From, To, CC, BCC) | Who sends/receives |
| **Transport** | Protocol for SENDING email (SMTP) | The sender |
| **Store** | Protocol for RECEIVING email (POP3/IMAP) | The receiver |

---

## 1. Sending Email - Step by Step

### Prerequisites

1. **Enable SMTP service** in your email account
2. **Get an authorization code** (not your regular password) from your email provider
3. **Add JavaMail dependency** to your project

### Maven Dependency

```xml
<dependency>
    <groupId>com.sun.mail</groupId>
    <artifactId>javax.mail</artifactId>
    <version>1.6.2</version>
</dependency>
```

---

## Complete Code: Sending a Plain Text Email

```java
import java.util.Properties;           // For setting configuration properties
import javax.mail.*;                   // Main JavaMail classes
import javax.mail.internet.*;          // Internet-specific email classes (MIME)

public class EmailSender {
    
    public static void main(String[] args) {
        
        // ========== CONFIGURATION ==========
        
        // 1. Set up mail server properties
        // Properties object holds configuration parameters for the mail session
        Properties props = new Properties();
        
        // Enable authentication (server requires username/password)
        props.put("mail.smtp.auth", "true");
        
        // Enable STARTTLS (encrypts the connection)
        props.put("mail.smtp.starttls.enable", "true");
        
        // SMTP server address (for Gmail: smtp.gmail.com)
        props.put("mail.smtp.host", "smtp.gmail.com");
        
        // SMTP server port (587 is standard TLS port)
        props.put("mail.smtp.port", "587");
        
        // ========== AUTHENTICATION ==========
        
        // 2. Create a Session object with authentication
        // The Authenticator class handles login credentials
        Session session = Session.getInstance(props, new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // Return username and password (or authorization code)
                // Note: Use environment variables for production!
                return new PasswordAuthentication("your-email@gmail.com", "your-auth-code");
            }
        });
        
        // Optional: Enable debug mode to see SMTP conversation
        // session.setDebug(true);
        
        try {
            // ========== CREATE MESSAGE ==========
            
            // 3. Create a MimeMessage object (represents the email)
            MimeMessage message = new MimeMessage(session);
            
            // 4. Set the sender's email address
            // InternetAddress validates and formats email addresses
            message.setFrom(new InternetAddress("your-email@gmail.com"));
            
            // 5. Set the recipient(s)
            // RecipientType.TO = primary recipient
            // Other types: CC (carbon copy), BCC (blind carbon copy)
            message.setRecipients(Message.RecipientType.TO, 
                InternetAddress.parse("recipient@example.com"));
            
            // 6. Set the email subject
            message.setSubject("Test Email from Java");
            
            // 7. Set the email body (plain text)
            // Use setText() for plain text, setContent() for HTML
            message.setText("Hello! This is a test email sent from Java using JavaMail API.");
            
            // ========== SEND MESSAGE ==========
            
            // 8. Send the email
            // Transport.send() is a static convenience method
            // It gets the transport from the session and sends the message
            Transport.send(message);
            
            System.out.println("Email sent successfully!");
            
        } catch (MessagingException e) {
            // MessagingException is the parent of all JavaMail errors
            System.out.println("Failed to send email: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

---

## Complete Code: Sending an HTML Email with Attachment

```java
import java.util.Properties;
import javax.mail.*;
import javax.mail.internet.*;
import javax.activation.*;     // For handling attachments (DataHandler, FileDataSource)

public class EmailWithAttachment {
    
    public static void main(String[] args) {
        
        // ========== SERVER CONFIGURATION ==========
        Properties props = new Properties();
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.starttls.enable", "true");
        props.put("mail.smtp.host", "smtp.gmail.com");
        props.put("mail.smtp.port", "587");
        
        // ========== AUTHENTICATION ==========
        Session session = Session.getInstance(props, new Authenticator() {
            protected PasswordAuthentication getPasswordAuthentication() {
                return new PasswordAuthentication("your-email@gmail.com", "your-auth-code");
            }
        });
        
        try {
            // ========== CREATE MESSAGE ==========
            MimeMessage message = new MimeMessage(session);
            message.setFrom(new InternetAddress("your-email@gmail.com"));
            message.setRecipients(Message.RecipientType.TO, 
                InternetAddress.parse("recipient@example.com"));
            message.setSubject("HTML Email with Attachment");
            
            // ========== CREATE MULTIPART EMAIL ==========
            // A Multipart email can contain multiple parts (text, HTML, attachments)
            MimeMultipart multipart = new MimeMultipart();
            
            // ----- PART 1: HTML Body -----
            MimeBodyPart htmlPart = new MimeBodyPart();
            String htmlContent = "<h1>Hello!</h1>"
                               + "<p>This is an <b>HTML</b> email sent from Java.</p>"
                               + "<p>Check the attachment below.</p>";
            htmlPart.setContent(htmlContent, "text/html");
            multipart.addBodyPart(htmlPart);
            
            // ----- PART 2: Attachment -----
            MimeBodyPart attachmentPart = new MimeBodyPart();
            
            // DataHandler handles the file data
            // FileDataSource points to the file on disk
            String filename = "path/to/your/file.pdf";
            FileDataSource source = new FileDataSource(filename);
            attachmentPart.setDataHandler(new DataHandler(source));
            attachmentPart.setFileName(source.getName());  // Set name in email
            multipart.addBodyPart(attachmentPart);
            
            // ========== SET CONTENT AND SEND ==========
            message.setContent(multipart);
            Transport.send(message);
            
            System.out.println("HTML email with attachment sent!");
            
        } catch (MessagingException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 2. Receiving Email - IMAP/POP3

### Protocols for Receiving Email

| Protocol | What it does | Default Port | Use case |
|----------|--------------|--------------|----------|
| **IMAP** | Reads messages from server | 993 (SSL) | Multiple devices, keep messages on server |
| **POP3** | Downloads messages (often deletes from server) | 995 (SSL) | Single device, offline reading |

### Code: Receiving Emails with IMAP

```java
import java.util.Properties;
import javax.mail.*;

public class EmailReceiver {
    
    public static void main(String[] args) {
        
        // ========== CONFIGURATION FOR IMAP ==========
        Properties props = new Properties();
        
        // Set the protocol to IMAP
        props.put("mail.store.protocol", "imap");
        
        // IMAP server (Gmail: imap.gmail.com)
        props.put("mail.imap.host", "imap.gmail.com");
        
        // IMAP port (993 for SSL)
        props.put("mail.imap.port", "993");
        
        // Enable SSL for secure connection
        props.put("mail.imap.ssl.enable", "true");
        
        try {
            // ========== CREATE SESSION ==========
            Session session = Session.getDefaultInstance(props);
            
            // ========== CREATE STORE AND CONNECT ==========
            // Store handles the connection to the mail server
            Store store = session.getStore("imap");
            store.connect("imap.gmail.com", "your-email@gmail.com", "your-auth-code");
            
            // ========== OPEN A FOLDER ==========
            // INBOX is the default folder for received emails
            Folder inbox = store.getFolder("INBOX");
            
            // OPEN_READ_ONLY: Just read, don't mark as read
            // OPEN_READ_WRITE: Mark messages as read when opened
            inbox.open(Folder.READ_ONLY);
            
            // ========== GET MESSAGES ==========
            // Get all messages from the folder
            Message[] messages = inbox.getMessages();
            
            System.out.println("Total messages: " + messages.length);
            
            // Process only the latest 10 messages
            int start = Math.max(messages.length - 10, 0);
            for (int i = start; i < messages.length; i++) {
                Message msg = messages[i];
                
                System.out.println("\n--- Message " + (i + 1) + " ---");
                System.out.println("Subject: " + msg.getSubject());
                System.out.println("From: " + msg.getFrom()[0]);
                System.out.println("Date: " + msg.getSentDate());
                
                // Get the content as String (plain text)
                Object content = msg.getContent();
                if (content instanceof String) {
                    System.out.println("Body: " + ((String) content).substring(0, Math.min(100, ((String) content).length())) + "...");
                }
            }
            
            // ========== CLEAN UP ==========
            inbox.close(false);  // false = don't expunge deleted messages
            store.close();
            
        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## How JavaMail Works Internally

### The Transport Class (Sending)

```
Your Code → Session → Transport.connect(SMTP server) → Transport.sendMessage()
                                                              │
                                                              ▼
                                                         Email Server
```

### The Store Class (Receiving)

```
Your Code → Session → Store.connect(IMAP/POP3 server) → Folder.open() → Message[]
```

---

## Common SMTP Server Settings

| Email Provider | SMTP Host | Port | Security |
|----------------|-----------|------|----------|
| **Gmail** | smtp.gmail.com | 587 | STARTTLS |
| **Outlook/Hotmail** | smtp-mail.outlook.com | 587 | STARTTLS |
| **Yahoo** | smtp.mail.yahoo.com | 465 | SSL |
| **163.com** | smtp.163.com | 465 | SSL |

---

## Important Security Notes

1. **Don't hardcode passwords** - Use environment variables
2. **Use authorization codes** - Many providers require app-specific passwords
3. **Enable SSL/TLS** - Always use secure connections
4. **Check provider requirements** - Some need "Allow less secure apps" or app passwords

---

## Quick Reference Table

| Task | Class | Key Method |
|------|-------|------------|
| Configure connection | `Properties` | `props.put(key, value)` |
| Create mail session | `Session` | `Session.getInstance(props, authenticator)` |
| Create email | `MimeMessage` | `new MimeMessage(session)` |
| Send email | `Transport` | `Transport.send(message)` |
| Receive email | `Store` | `store.getFolder("INBOX")` |
| Add attachment | `MimeBodyPart` | `attachmentPart.setDataHandler()` |

---

## The Golden Rule

> **JavaMail uses Session to configure the connection, Message to create the email content, and Transport to send it. For receiving, use Store to connect and Folder to access messages. Always authenticate and use secure connections (SSL/TLS).**

**Memory trick:**
```
Session = "Setup and login"
Message = "What I want to send"
Transport = "How it gets delivered"
Store = "Where received mail lives"
Folder = "Where messages are organized"

Send: Session → Message → Transport
Receive: Session → Store → Folder → Message[]
```