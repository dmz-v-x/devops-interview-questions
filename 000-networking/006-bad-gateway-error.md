### Question  
Your website is returning a **502 Bad Gateway** HTTP status code. How would you troubleshoot it?

---

### Answer  

---

### 1. What is 502 Bad Gateway?

- A **502 Bad Gateway** error occurs when:
  - A **reverse proxy/load balancer** (NGINX, HAProxy, AWS ELB)  
  - Receives an **invalid or no response** from the backend server  

---

### 2. Architecture Context

```
Client → Proxy (NGINX/ELB) → Backend App
```

- 502 happens when:
  - Proxy cannot communicate properly with backend  

---

### 3. Common Root Causes

---

#### 3.1 Backend Service is Down

- Application server is not running  

Check:

```bash
systemctl status your-app
```

---

#### 3.2 Wrong Upstream Configuration (NGINX)

- Incorrect host or port  

Example:

```nginx
proxy_pass http://localhost:5000;
```

- Verify:
  - Port is correct  
  - Service is running  

---

#### 3.3 Backend Timeout / Slow Response

- Backend is too slow  

Fix:

```nginx
proxy_read_timeout 60s;
```

---

#### 3.4 Firewall / Security Group Blocking

- Backend port blocked  

Test:

```bash
nc -zv localhost 5000
```

---

#### 3.5 Incorrect Protocol (HTTP vs HTTPS)

- Proxy expects HTTP but backend uses HTTPS  

Fix:

```nginx
proxy_pass https://localhost:5000;
```

---

#### 3.6 Application Crash / OOM

- App crashed or killed due to memory  

Check logs:

```bash
journalctl -u your-app
docker logs your-container
```

---

### 4. Step-by-Step Troubleshooting

---

#### Step 1: Check Proxy Logs

```bash
tail -f /var/log/nginx/error.log
```

---

#### Step 2: Check Backend Health

```bash
curl http://localhost:5000/health
```

---

#### Step 3: Restart Services

```bash
systemctl restart your-app
systemctl restart nginx
```

---

#### Step 4: Verify Port Listening

```bash
ss -tulnp | grep 5000
```

---

#### Step 5: Check Connectivity

```bash
curl http://localhost:5000
```

---

### 5. Key Debug Flow

1. Check backend service status  
2. Check proxy configuration  
3. Check logs (NGINX + app)  
4. Test backend directly  
5. Check network/firewall  
6. Verify timeouts and protocols  

---

### 6. Common Causes Summary

- Backend down  
- Wrong port/config  
- Timeout issues  
- Firewall blocking  
- SSL mismatch  
- App crash  

---

### 7. Interview-Ready Summary

“A 502 Bad Gateway error occurs when a proxy like NGINX cannot get a valid response from the backend server. I start by checking if the backend service is running, then verify the proxy configuration and logs. I test the backend directly using curl, check for port or firewall issues, and ensure there are no protocol mismatches or timeouts. This helps quickly isolate whether the issue is in the proxy, network, or application.”
