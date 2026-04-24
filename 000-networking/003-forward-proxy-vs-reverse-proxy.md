### Question  
What is the difference between Forward Proxy and Reverse Proxy?

---

### Answer  

---

### 1. Forward Proxy

- A **forward proxy** sits **between client and internet**  
- It is used by **clients to access external servers**  

---

#### Key Points:

- Client sends request → Proxy → Internet  
- Server only sees the **proxy**, not the real client  
- Used for:
  - Content filtering  
  - Access control  
  - Privacy  

---

#### Example Scenario:

- A school uses a proxy to block:
  - YouTube  
  - Social media  

---

#### Flow:

```
Client → Forward Proxy → Internet Server
```

---

### 2. Reverse Proxy

- A **reverse proxy** sits **in front of servers**  
- It is used by **servers to handle client requests**  

---

#### Key Points:

- Client sends request → Proxy → Backend servers  
- Client thinks it is talking to the server  
- Used for:
  - Load balancing  
  - Security  
  - SSL termination  

---

#### Example Scenario:

- A company uses NGINX to route:
  - `/api` → API service  
  - `/auth` → Auth service  
  - `/app` → Web app  

---

#### Flow:

```
Client → Reverse Proxy → Backend Servers
```

---

### 3. Key Differences

| Feature        | Forward Proxy                          | Reverse Proxy                          |
| -------------- | -------------------------------------- | -------------------------------------- |
| Positioned for | Clients                                | Servers                                |
| Hides          | Client identity                        | Server identity                        |
| Purpose        | Control outgoing traffic               | Manage incoming traffic                |
| Use Case       | Filtering, anonymity, corporate access | Load balancing, security, scalability  |
| Example Tools  | Squid, Proxy servers                   | NGINX, HAProxy, AWS ALB                |

---

### 4. Real-World Analogy

- Forward Proxy → Like a **school gatekeeper** deciding what students can access  
- Reverse Proxy → Like a **receptionist** directing visitors to the right department  

---

### 5. Key Takeaways

- Forward proxy → client-side control  
- Reverse proxy → server-side control  
- Both improve:
  - Security  
  - Performance  
  - Control  

---

### 6. Interview-Ready Summary

“A forward proxy sits between clients and the internet and is used to control or filter outgoing traffic, hiding the client’s identity. A reverse proxy sits in front of servers and routes incoming requests to backend services, providing load balancing, security, and scalability.”
