### Question  
Application deployed on NGINX returns "Connection Refused". How will you fix it?

---

### Answer  

---

### 1. Understanding the Error

- "Connection Refused" means:
  - No service is listening on the target port  
  - TCP handshake is rejected  
  - It is **not an HTTP (4xx/5xx) error**  

- Common causes:
  - NGINX not running  
  - Wrong port configuration  
  - Backend application not running  
  - Firewall blocking traffic  

---

### 2. Reproduce the Error

```bash
curl -I http://localhost
```

**Example Error:**
    curl: (7) Failed to connect to localhost port 80: Connection refused

- Confirms:
  - Server is not accepting connections on port 80  

---

### 3. Check if NGINX is Running

```bash
sudo systemctl status nginx
```

- If inactive or failed:

```bash
sudo systemctl restart nginx
```

- Check logs:

```bash
sudo journalctl -u nginx -xe
```

---

### 4. Check if NGINX is Listening on Port

```bash
sudo netstat -tulnp | grep nginx
```

OR:

```bash
ss -tuln | grep :80
```

- If no output:
  - NGINX is **not listening on port 80**  

---

### 5. Validate NGINX Configuration

```bash
sudo nginx -t
```

- Fix any syntax errors  

- Check config file:

    server {
        listen 80;
        location / {
            proxy_pass http://localhost:5000;
        }
    }

- Verify:
  - Correct `listen` directive  
  - Correct `proxy_pass` target  

---

### 6. Verify Backend Application

- Check if app is running:

```bash
sudo netstat -tulnp | grep 5000
```

- Test backend directly:

```bash
curl http://localhost:5000
```

- If not working:
  - Start or debug the application  
  - Ensure it is listening on the expected port  

---

### 7. Check Firewall / Security Rules

- Check UFW:

```bash
sudo ufw status
```

- Check iptables:

```bash
sudo iptables -L
```

- In cloud environments:
  - AWS Security Groups  
  - GCP Firewall Rules  

- Ensure ports:
  - 80 (HTTP)  
  - 443 (HTTPS)  

---

### 8. Common Root Causes

- NGINX service stopped  
- Port mismatch in config  
- Backend app not running  
- Incorrect proxy_pass  
- Firewall blocking access  

---

### 9. Preventive Measures

- Enable auto-start:

```bash
sudo systemctl enable nginx
```

- Add health checks for backend  
- Monitor using:
  - Prometheus + Grafana  

- Set alerts for downtime  

---

### 10. Key Takeaways

- "Connection Refused" = **No service listening on port**  
- Always debug in order:
  - Service → Port → Config → Backend → Network  

---

### 11. Interview-Ready Summary

“I would first reproduce the issue using curl to confirm it’s a connection refusal. Then I’d check if NGINX is running and listening on the correct port. Next, I’d validate the NGINX configuration and ensure the backend application is running and reachable. Finally, I’d verify firewall and security group settings. Based on findings, I’d restart services, fix configurations, or bring the backend up.”
