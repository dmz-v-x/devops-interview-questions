### Question  
What is the difference between TCP and UDP?

---

### Answer  

TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are both **transport layer protocols**, but they differ in reliability, speed, and how they transmit data.

---

### 1. Key Differences

| Feature         | TCP                                                                        | UDP                                                |
| --------------- | -------------------------------------------------------------------------- | -------------------------------------------------- |
| **Connection**  | Connection-oriented (establishes connection before transfer)               | Connectionless (no setup required)                 |
| **Reliability** | Reliable – ensures delivery, order, and retransmission                     | Unreliable – no guarantee of delivery or order     |
| **Speed**       | Slower due to checks and acknowledgments                                   | Faster due to minimal overhead                     |
| **Use Cases**   | HTTP/HTTPS, SMTP, FTP                                                      | Streaming, gaming, VoIP, DNS                       |
| **Overhead**    | High                                                                       | Low                                                |

---

### 2. TCP (Transmission Control Protocol)

#### Characteristics:

- Connection-oriented  
- Reliable delivery  
- Ordered data transfer  
- Error checking and retransmission  

---

#### How it works:

1. Establishes connection (3-way handshake)  
2. Sends data in sequence  
3. Waits for acknowledgment  
4. Retransmits if data is lost  

---

#### Example Use Cases:

- Web browsing (HTTP/HTTPS)  
- Email (SMTP)  
- File transfer (FTP)  

---

### 3. UDP (User Datagram Protocol)

#### Characteristics:

- Connectionless  
- No guarantee of delivery  
- No ordering  
- Minimal overhead  

---

#### How it works:

- Sends packets (datagrams) directly  
- No acknowledgment  
- No retransmission  

---

#### Example Use Cases:

- Video streaming  
- Online gaming  
- VoIP calls  
- DNS queries  

---

### 4. Real-World Analogy

- TCP → Like a **phone call** (confirmation required)  
- UDP → Like sending a **letter** (no guarantee it arrives)  

---

### 5. Key Takeaways

- TCP = reliability + order + slower  
- UDP = speed + low overhead + no guarantees  
- Choice depends on:
  - Accuracy vs speed  

---

### 6. Interview-Ready Summary

“TCP is a connection-oriented protocol that ensures reliable and ordered data delivery using acknowledgments and retransmissions, making it suitable for applications like web browsing and file transfers. UDP is a connectionless protocol that prioritizes speed over reliability, making it ideal for real-time applications like streaming, gaming, and DNS.”
