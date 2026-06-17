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

| Need                  | Explanation                            |
| --------------------- | -------------------------------------- |
| **User Registration** | Send confirmation/welcome emails       |
| **Password Reset**    | Email reset links to users             |
| **Notifications**     | Order confirmations, alerts, reminders |
| **Reports**           | Email generated reports automatically  |
| **Marketing**         | Send newsletters to subscribers        |

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
        // SMTP server address (for Gmail: smtp.gmail.com)
        props.put("mail.smtp.host", "smtp.gmail.com");
        
        // SMTP server port (587 is standard TLS port)
        props.put("mail.smtp.port", "587");
        

        //This creates a **mail session** - a connection factory that holds all your email configuration and can create messages.
        Session session = Session.getInstance(props);
        
        
        
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