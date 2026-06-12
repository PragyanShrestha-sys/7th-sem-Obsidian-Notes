Here’s a clear explanation of the **TCP Three-Way Handshake** – the process TCP uses to establish a reliable connection before any data is sent.

## Why is it needed?

TCP is **connection-oriented** – both sides need to agree on:
- Starting sequence numbers (for ordering packets)
- Buffer sizes (for flow control)
- Options like window scaling

The handshake ensures both are ready and synchronizes these details.

---

## The Three Steps (SYN, SYN-ACK, ACK)

Think of it like a **polite phone call**:

| Step | Direction | Packet type | Meaning |
|------|-----------|-------------|---------|
| 1 | Client → Server | **SYN** | "I want to talk. Let's start with sequence number X." |
| 2 | Server → Client | **SYN-ACK** | "OK, I agree. My sequence number is Y. And I received your X." |
| 3 | Client → Server | **ACK** | "Got your Y. Connection is ready. Let's send data." |

---

## Detailed Breakdown

### Step 1: SYN (Synchronize)
The client sends a TCP packet with:
- `SYN` flag = 1
- `SEQ` (sequence number) = a random number, say **100**

> *"Hi server. I'm client. My first packet will be number 100."*

### Step 2: SYN-ACK (Synchronize + Acknowledge)
The server responds with:
- `SYN` flag = 1
- `ACK` flag = 1
- `SEQ` = a random number, say **500** (server's starting sequence)
- `ACK` = **101** (client's SEQ + 1)

> *"Hi client. My first packet is 500. And I confirm I received your packet #100. Next, send me packet #101."*

### Step 3: ACK (Acknowledge)
The client replies with:
- `ACK` flag = 1
- `SEQ` = **101** (the next packet client will send)
- `ACK` = **501** (server's SEQ + 1)

> *"Thanks server. I confirm I received your packet #500. Connection is open."*

---

## Visual Diagram

```
Client                                 Server
  |                                      |
  | ------- SYN (SEQ=100) ------------> |
  |                                      |
  | <---- SYN-ACK (SEQ=500, ACK=101) --- |
  |                                      |
  | ------- ACK (SEQ=101, ACK=501) ----> |
  |                                      |
  | ========= CONNECTION ESTABLISHED ====|
  |                                      |
  | --------- Data Transfer -----------> |
```

---

## Why random sequence numbers?

Security! If sequence numbers were predictable (like starting at 0), attackers could easily inject fake packets into the connection (TCP hijacking). Random numbers make that much harder.

---

## What happens if a step fails?

- **No SYN-ACK received?** → Client retries SYN after a timeout.
- **No final ACK received?** → Server resends SYN-ACK.
- After several failed retries, the connection attempt fails.

---

## Real-world analogy

| Step | Handshake | Phone call |
|------|-----------|-------------|
| 1 | SYN | You dial and say "Hello?" |
| 2 | SYN-ACK | Other person says "Hi! Can you hear me?" |
| 3 | ACK | You say "Yes, I hear you. Let's talk." |

---

## Quick facts

- **What's transmitted?** Only headers – no application data in the handshake.
- **How many round trips?** 1.5 (SYN, then SYN-ACK, then ACK) – technically 3 messages, but the final ACK can carry data in some implementations (called "TCP Fast Open").
- **State changes:**
  - Client: `CLOSED` → `SYN_SENT` → `ESTABLISHED`
  - Server: `LISTEN` → `SYN_RCVD` → `ESTABLISHED`

---

## Termination: The Four-Way Handshake

Just as a fun note – closing a TCP connection takes **4 steps** (FIN, ACK, FIN, ACK) because each side must independently say goodbye.

Would you like me to explain the termination (4-way handshake) as well?



---
## [[After Three way handshake (sending a file)]]

