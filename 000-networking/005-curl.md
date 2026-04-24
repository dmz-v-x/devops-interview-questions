### Question  
When using `curl`, the request works with an IP address but fails when using the domain name. What could be the issue and how do you fix it?

---

### Answer  

If:

```bash
curl http://<IP>
```

works, but:

```bash
curl http://example.com
```

fails, the issue is **most likely DNS-related**.

---

### 1. DNS Not Resolving

- Your system cannot resolve the domain to an IP  

Check:

```bash
nslookup example.com
dig example.com
```

- If these fail → DNS is the issue  

---

### 2. Wrong or Missing DNS Configuration

Check DNS config:

```bash
cat /etc/resolv.conf
```

- Ensure valid nameserver exists:

```
nameserver 8.8.8.8
```

- If missing or incorrect → DNS won't work  

---

### 3. Firewall or Network Blocking DNS

- DNS uses **port 53**  

Test:

```bash
dig example.com @8.8.8.8
```

- If this works → local DNS is blocked  

---

### 4. Domain Doesn't Exist or Typo

- Verify domain is correct  

```bash
whois example.com
```

- Try from another network/browser  

---

### 5. Hosts File Override

Check:

```bash
cat /etc/hosts
```

- Incorrect entry may override DNS  

Example:
```
127.0.0.1 example.com
```

- Remove or fix incorrect mappings  

---

### 6. Internal DNS Issue

- If domain is internal:

```
myapp.internal.local
```

- Ensure:
  - VPN is connected  
  - Internal DNS is reachable  

---

### 7. Quick Fixes

---

#### Add DNS Server

```bash
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf > /dev/null
```

---

#### Temporary Curl Test (Bypass DNS)

```bash
curl --resolve example.com:80:<IP> http://example.com
```

---

### 8. Key Takeaways

- IP works → network is fine  
- Domain fails → DNS issue  
- Always check:
  - `dig` / `nslookup`  
  - `/etc/resolv.conf`  
  - `/etc/hosts`  

---

### 9. Interview-Ready Summary

“If curl works with an IP but not with a domain, it usually indicates a DNS issue. I check DNS resolution using dig or nslookup, verify /etc/resolv.conf for correct nameservers, ensure no incorrect entries exist in /etc/hosts, and confirm that DNS traffic isn’t blocked. If needed, I test using a public DNS server or bypass DNS using curl --resolve.”
