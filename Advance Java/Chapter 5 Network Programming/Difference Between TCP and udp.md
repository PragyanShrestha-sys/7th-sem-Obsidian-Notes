Here’s a clear **tabular comparison** of TCP and UDP:

| Feature                 | TCP (Transmission Control Protocol)                      | UDP (User Datagram Protocol)                          |
| ----------------------- | -------------------------------------------------------- | ----------------------------------------------------- |
| **Connection**          | Connection-oriented (handshake required)                 | Connectionless (no handshake)                         |
| **Reliability**         | Reliable – guarantees delivery                           | Unreliable – no delivery guarantee                    |
| **Acknowledgment**      | Yes – sends ACKs for received packets                    | No                                                    |
| **Retransmission**      | Retransmits lost packets                                 | No retransmission                                     |
| **Ordering**            | Preserves packet order                                   | No ordering – packets may arrive out of sequence      |
| **Error checking**      | Yes (checksum) + error recovery                          | Yes (checksum) but no recovery                        |
| **Flow control**        | Yes – prevents sender from overwhelming receiver         | No                                                    |
| **Overhead**            | High (due to reliability features)                       | Very low                                              |
| **Speed**               | Slower                                                   | Faster                                                |
| **Data streaming**      | Byte-stream (no message boundaries)                      | Datagram (message boundaries preserved)               |
| **Multicast/Broadcast** | Not supported                                            | Supported                                             |
| **Typical use cases**   | Web (HTTP/HTTPS), Email (SMTP), File transfer (FTP), SSH | Streaming video/audio, VoIP, online gaming, DNS, DHCP |
| **Example apps**        | Chrome, Outlook, FileZilla, Zoom (signaling)             | YouTube live, Discord voice, Twitch, Skype calls      |

---

### Quick rule of thumb:
- **Need every byte, in order, no exceptions?** → Use **TCP**
- **Speed matters more than perfect accuracy?** → Use **UDP**