### Question  
What is the purpose of the `/etc/hosts` file?

---

### Answer  

---

### 1. Purpose of `/etc/hosts`

- The `/etc/hosts` file is used to **map hostnames to IP addresses locally**  
- It provides a **manual DNS resolution mechanism**  

---

#### Key Idea:

- Before querying DNS, the system checks `/etc/hosts`  
- If a match is found → it uses that IP directly  

---

### 2. Why It’s Useful

- Override DNS resolution  
- Test applications locally  
- Define internal hostnames  
- Block domains (by mapping to `127.0.0.1`)  

---

### 3. File Format

Each line follows:

```
<IP_address>   <hostname>   [aliases]
```

---

#### Example:

```
127.0.0.1       localhost
192.168.1.10    webserver.local   web
```

---

#### Meaning:

- `webserver.local` → `192.168.1.10`  
- `web` (alias) → same IP  

---

### 4. How Resolution Works

```
Application → /etc/hosts → DNS → Internet
```

- `/etc/hosts` is checked **first**  

---

### 5. How to Edit `/etc/hosts`

```bash
sudo nano /etc/hosts
```

- Add or modify entries  
- Save changes  

---

### 6. Common Use Cases

- Local development:
```
127.0.0.1   myapp.local
```

- Internal servers:
```
192.168.1.20   db.internal
```

- Block website:
```
127.0.0.1   facebook.com
```

---

### 7. Key Takeaways

- Local hostname resolution  
- Overrides DNS  
- Requires root access to modify  
- Useful for testing and debugging  

---

### 8. Interview-Ready Summary

“The /etc/hosts file is used for local hostname-to-IP mapping and is checked before DNS resolution. It allows manual control over how hostnames are resolved, making it useful for testing, overriding DNS, and defining internal hostnames.”
