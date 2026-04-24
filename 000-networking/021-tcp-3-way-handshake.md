### Question  
Explain how the TCP three-way handshake works.

---

### Answer  

---

### 1. What is the TCP Three-Way Handshake?

- It is the process used to **establish a reliable connection** between a client and a server  
- Ensures:
  - Both sides are ready  
  - Sequence numbers are synchronized  

---

### 2. Steps of the Three-Way Handshake

---

### Step 1: SYN (Synchronize)

- **Client → Server**

- Sends:
  - SYN flag  
  - Initial Sequence Number (ISN)  

---

#### Meaning:

“Hi, I want to start a connection. Here’s my sequence number.”

---

### Step 2: SYN-ACK (Synchronize + Acknowledge)

- **Server → Client**

- Sends:
  - SYN flag  
  - ACK flag  
  - Server’s own ISN  
  - Acknowledges client’s ISN  

---

#### ACK value:

```
ACK = client_ISN + 1
```

---

#### Meaning:

“Got your request. Here’s my sequence number, and I acknowledge yours.”

---

### Step 3: ACK (Acknowledge)

- **Client → Server**

- Sends:
  - ACK flag  
  - Acknowledges server’s sequence number  

---

#### ACK value:

```
ACK = server_ISN + 1
```

---

#### Meaning:

“Thanks. We’re now connected.”

---

### 3. Example with Sequence Numbers

| Step | Sender | Flags    | Seq / Ack Numbers    |
| ---- | ------ | -------- | -------------------- |
| 1    | Client | SYN      | Seq = 100            |
| 2    | Server | SYN, ACK | Seq = 500, Ack = 101 |
| 3    | Client | ACK      | Seq = 101, Ack = 501 |

---

### 4. After the Handshake

- Connection is established  
- Data transfer begins  
- Communication is:
  - Reliable  
  - Ordered  

---

### 5. Why Three-Way Handshake?

| Purpose                | Explanation                                                      |
| ---------------------- | ---------------------------------------------------------------- |
| **Reliable setup**     | Both sides agree on communication parameters                     |
| **Prevents data loss** | No data is sent before connection is confirmed                   |
| **Avoids spoofing**    | Ensures both client and server are reachable                     |

---

### 6. What If It Fails?

- If any step fails:
  - Connection is not established  
  - Retries or timeouts occur  

---

### 7. Simple Visualization

```
Client        Server
  | --- SYN ---> |
  | <-- SYN-ACK--|
  | --- ACK ---> |
```

---

### 8. Key Takeaways

- 3 steps: SYN → SYN-ACK → ACK  
- Establishes reliable connection  
- Uses sequence numbers for tracking  

---

### 9. Interview-Ready Summary

“The TCP three-way handshake is used to establish a reliable connection between a client and server. It involves three steps: the client sends a SYN, the server responds with SYN-ACK, and the client replies with ACK. This process ensures both sides are synchronized and ready for data transmission.”
