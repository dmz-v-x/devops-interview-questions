### Question  
Your website is not loading.  

Task:  
Describe the step-by-step investigation process to identify and fix the issue.

---

### Answer  

---

### 1. Check if Site is Down Globally or Locally

```bash
curl -I https://yourdomain.com
ping yourdomain.com
```

- Or use external tools:
  - https://downforeveryoneorjustme.com  

- Helps determine:
  - Global outage vs local/network issue  

---

### 2. Verify DNS Resolution

```bash
dig yourdomain.com
```

```bash
nslookup yourdomain.com
```

- Expected:
  - Correct IP address returned  

- If not:
  - Check DNS provider (Route53, Cloudflare, etc.)  
  - Verify A/AAAA/CNAME records  

---

### 3. Validate Domain Routing

```bash
curl -v https://yourdomain.com
```

- Compare:
  - Response IP vs actual server IP  

- If mismatch:
  - Check:
    - DNS records  
    - Load balancer configuration  
    - CDN rules  

---

### 4. Check Network Connectivity / Firewall

```bash
telnet yourdomain.com 443
```

```bash
nc -zv yourdomain.com 80
```

- If connection fails:
  - Check:
    - Security Groups  
    - Firewall rules (ufw/iptables)  
    - Network ACLs  

---

### 5. Verify Web Server Status

```bash
sudo systemctl status nginx
```

```bash
sudo systemctl status apache2
```

- If not running:

```bash
sudo systemctl restart nginx
```

- Ensure service is active and listening  

---

### 6. Check Web Server Logs

```bash
/var/log/nginx/error.log
```

```bash
/var/log/httpd/error_log
```

- Look for:
  - Crashes  
  - Misconfigurations  
  - Permission issues  

- Also check application logs:
  - `app.log`, `stderr`  

---

### 7. Check System Resources

```bash
df -h
```

```bash
top
```

```bash
free -m
```

- Look for:
  - Disk full  
  - High CPU  
  - Memory exhaustion  

- These can make server unresponsive  

---

### 8. Check Backend Dependencies

- Verify:
  - Database (MySQL/Postgres)  
  - Cache (Redis/Memcached)  
  - Application server  

- If backend is down:
  - App may fail even if web server is running  

---

### 9. Check SSL Certificate

```bash
curl -Iv https://yourdomain.com
```

- Look for:
  - Expired certificate  
  - SSL handshake errors  

- Fix:
  - Renew certificate (e.g., Let’s Encrypt)  

---

### 10. Rollback Recent Changes

- If issue started after deployment:

```bash
kubectl rollout undo deployment your-deployment
```

- Or:
  - Redeploy last stable version  

---

### 11. Key Takeaways

- Always debug layer by layer:
  - DNS → Network → Server → Application → Dependencies  

- Most issues come from:
  - Misconfiguration  
  - Service downtime  
  - Resource exhaustion  

---

### 12. Interview-Ready Summary

“I would troubleshoot step by step starting from checking if the site is globally down using curl or ping, then verify DNS resolution using dig or nslookup. Next, I’d check network connectivity, firewall rules, and ensure the web server is running. I’d inspect logs for errors, check system resources, and verify backend services like databases or caches. I’d also validate SSL certificates and, if the issue started after a deployment, perform a rollback. This systematic approach helps quickly isolate and fix the issue.”
