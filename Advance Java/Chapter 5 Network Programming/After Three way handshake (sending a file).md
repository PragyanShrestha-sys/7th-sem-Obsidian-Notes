Great question! Once the **three-way handshake** is complete and the connection is **established**, here's how TCP actually sends a file (or any data) reliably.

## The Short Answer

TCP breaks the file into **packets (segments)** , numbers them, sends them, and the receiver sends back **acknowledgments (ACKs)** for every packet received. If an ACK doesn't arrive in time, the sender **retransmits** that packet.

---

## Step-by-Step: Sending a File (e.g., a 1MB image)

### Before sending (already done):
- Handshake complete
- Both sides know starting sequence numbers (e.g., client SEQ=100, server SEQ=500)

### Step 1: Break file into segments
The 1MB file is split into smaller chunks (typically **1460 bytes** each, to fit inside a single Ethernet frame).

```
File: [1MB]
  ↓
Segments: [Seg#1] [Seg#2] [Seg#3] ... [Seg#~700]
```

### Step 2: Send segments with sequence numbers

| Segment | Data | SEQ number | Size |
|---------|------|------------|------|
| #1 | First 1460 bytes | 101 | 1460 |
| #2 | Next 1460 bytes | 1561 | 1460 |
| #3 | Next 1460 bytes | 3021 | 1460 |
| ... | ... | ... | ... |

Each segment gets a unique **sequence number** (the byte offset from the start).

### Step 3: Receiver acknowledges

For every segment received, the receiver sends back an **ACK** with the **next expected byte**.

**Example:**
- Client sends Segment #1 (SEQ=101, size=1460 bytes)
- Server receives it correctly
- Server replies: `ACK=1561` ("I got everything up to byte 1560, send me byte 1561 next")

### Step 4: Sender handles missing packets (Retransmission)

**Scenario:** Segment #2 gets lost

```
Client:  [Seg#1] → Server (ACK=1561)
Client:  [Seg#2] → ✨ LOST in network ✨
Client:  [Seg#3] → Server

Server:  "Wait, I got #1 (ACK=1561) and #3 (SEQ=3021), but I'm missing #2 (SEQ=1561)."
Server sends: ACK=1561 (again!)
```

Client sees **duplicate ACK** or **timeout** → immediately resends Segment #2.

### Step 5: Sliding window (Flow control)

To avoid overwhelming the receiver or network, TCP uses a **window** – how much data can be sent before needing an ACK.

```
Client: [Seg1][Seg2][Seg3][Seg4] → sent, waiting for ACK before sending more
Server: ACK=1561 (got Seg1)
Client: Now can send Seg5
```

Think of it like a **conveyor belt**: you can put items on as long as there's empty space in the receiver's "buffer."

---

## Visual Timeline

```
Client (sending file)                    Server (receiving)
       |                                      |
       | ----- Seg#1 (SEQ=101, 1460B) ---->  |
       |                                      |
       | <----------- ACK=1561 ------------  |  "Got #1, next please"
       |                                      |
       | ----- Seg#2 (SEQ=1561, 1460B) ---->  |
       |                                      |
       | ----- Seg#3 (SEQ=3021, 1460B) ---->  |
       |                                      |
       | <----------- ACK=3021 ------------  |  "Got #2, still waiting for #3?"
       |                                      |
       | -- (timeout, retransmit Seg#3) -->  |
       |                                      |
       | <----------- ACK=4481 ------------  |  "Got #3, next"
       |                                      |
       | ... continues until EOF ...          |
       |                                      |
       | ----- FIN (end of file) ---------->  |
```

---

## Key TCP Features for File Transfer

| Feature | What it does |
|---------|--------------|
| **Sequence numbers** | Every byte is numbered – no confusion about order |
| **Cumulative ACKs** | ACK=1561 means "I got everything up to byte 1560" |
| **Retransmission timer** | If no ACK after ~200ms, resend the packet |
| **Duplicate ACKs** | Receiver sends same ACK repeatedly = "I'm missing something!" |
| **Sliding window** | Limits how much un-ACKed data can be in flight |
| **Congestion window** | Slows down if network is dropping packets |

---

## Real-world example: Downloading a file in Chrome

1. **Handshake** (SYN, SYN-ACK, ACK) – <1ms
2. **Server sends file chunks** – each chunk gets a SEQ number
3. **Browser sends ACKs** – "got chunks 1-100, send 101 next"
4. **If WiFi glitches** – missed chunk is retransmitted
5. **All chunks received** – TCP reassembles in order
6. **Connection closes** (FIN handshake)

You see a smooth download, but behind the scenes, TCP might have retransmitted 3-5% of packets without you ever knowing.

---

## What UDP would do differently

- **No ACKs** – just sends packets and forgets
- **No retransmission** – lost packet = gone forever
- **No ordering** – video player must handle out-of-order frames
- **No flow control** – can overwhelm a slow receiver

This is why **file downloads use TCP** – losing even 1 byte corrupts the entire file.

---

## Summary Table: Sending a file

| Phase | What happens |
|-------|--------------|
| **Handshake** | Establish connection, sync sequence numbers |
| **Transfer** | Break file → send numbered segments → receive ACKs |
| **Loss recovery** | Timeout or duplicate ACK triggers retransmission |
| **Completion** | Last segment sent → receiver ACKs → connection closes |

Would you like me to explain the **TCP fast retransmit** (how TCP detects loss without waiting for a timeout) or **congestion control** (how TCP avoids clogging the network)?