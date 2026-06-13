Here’s a clear explanation of **TCP** and **UDP**, the two most common transport layer protocols used for sending data over networks (like the internet).

## The Big Analogy: Sending a Package

TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are ==foundational transport protocols used to send data packets across the internet==. TCP prioritizes reliability and accuracy, ensuring no data is lost, while UDP prioritizes speed and efficiency, sacrificing error-checking for faster delivery.

Key Differences

| Feature             | TCP (Transmission Control Protocol)                           | UDP (User Datagram Protocol)                             |
| ------------------- | ------------------------------------------------------------- | -------------------------------------------------------- |
| **Primary Focus**   | Reliability and Data Integrity                                | Speed and Performance                                    |
| **Connection Type** | Connection-oriented (establishes a connection before sending) | Connectionless (sends data immediately without checking) |
| **Error Checking**  | High; tracks, reorders, and resends lost packets              | None; ignores lost packets                               |
| **Speed**           | Slower (due to overhead and acknowledgments)                  | Faster (minimal overhead)                                |

How They Work

- **TCP:** Before sending data, it establishes a dedicated connection via a "three-way handshake". It breaks data into numbered packets and requires the receiver to acknowledge every packet. If a packet goes missing, TCP resends it to guarantee the final file or message is complete and perfectly ordered.
- **UDP:** It simply blasts data packets toward the destination without verifying if the receiver is ready or if the packets arrive. If a packet drops during transit, UDP does not attempt to recover it
---

## TCP (Transmission Control Protocol)

**Key characteristics:**
- **Connection-oriented** – Establishes a connection before sending data (3-way handshake).
- **Reliable** – Guarantees data arrives, and in the correct order.
- **Error-checked** – Detects and retransmits lost or corrupted packets.
- **Flow control** – Adjusts transmission speed to avoid overwhelming the receiver.
- **Congestion control** – Slows down if the network is busy.

**How it works (simplified):**
1. Sender and receiver agree to talk (handshake).
2. Data is broken into packets with sequence numbers.
3. Receiver acknowledges each packet; if missing, sender resends.
4. Packets are reassembled in order at the destination.

**Good for:**  
- Web browsing (HTTP/HTTPS)
- Email (SMTP, IMAP)
- File transfers (FTP, SFTP)
- Anywhere missing data would cause problems

**Downside:** Slower, more overhead.

---

## UDP (User Datagram Protocol)

**Key characteristics:**
- **Connectionless** – Just sends data without establishing a connection.
- **Unreliable** – No guarantee of delivery or order.
- **No retransmission** – Lost packets are gone forever.
- **No flow or congestion control** – Sends as fast as the application wants.
- **Very low overhead** – Tiny header (8 bytes vs. TCP’s 20+ bytes).

**How it works (simplified):**
1. Application gives a packet (datagram) to UDP.
2. UDP adds destination port info and sends it.
3. No acknowledgment, no retries, no ordering.

**Good for:**  
- Live video streaming (YouTube, Twitch)
- Voice over IP (Zoom, Skype, FaceTime)
- Online gaming (real-time action)
- DNS lookups (one quick question, one quick answer)

**Downside:** Packets can be lost, duplicated, or arrive out of order.

---

## When to use which?

- **Use TCP** if you need **all the data**, in order, and can tolerate slight delays.  
  *Example: Loading a webpage — you don’t want missing pieces.*

- **Use UDP** if **speed matters more than perfection**, or lost data is okay.  
  *Example: A video game — one lost position update is better than waiting for a retransmit and causing lag.*

---

## Real-world examples

| Application | Protocol | Why |
|-------------|----------|-----|
| Browsing the web | TCP | Must get entire page, in order |
| Watching a live stream | UDP | A few dropped frames are fine; lag is not |
| Sending an email | TCP | You can't lose the message |
| Playing Fortnite | UDP | Instant updates matter more than perfect delivery |
| Loading a map tile | TCP | Needs complete image |
| Voice call | UDP | Slight audio glitch > awkward pause |

---
## [[Difference Between TCP and udp]]

---
## [[Three way handshake in TCP]]
