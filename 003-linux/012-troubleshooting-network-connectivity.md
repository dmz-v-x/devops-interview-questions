### Question
How do you troubleshoot network connectivity using Linux tools like `ping`, `traceroute`, or `netstat`?

### Answer

Troubleshooting network connectivity in Linux involves verifying different layers of networking such as **basic connectivity, routing path, DNS resolution, open ports, and application-level connectivity**. Several Linux tools help diagnose these issues, including `ping`, `traceroute`, `netstat`, `ss`, `ip`, `dig`, `curl`, `wget`, and `tcpdump`.

---

### Using `ping`

`ping` checks **basic network connectivity** between your system and a target host.

Syntax:

    ping <hostname or IP>

Examples:

    ping google.com
    ping -c 4 google.com

Explanation:

- `ping google.com` → checks if the host is reachable
- `-c 4` → sends only 4 packets instead of continuous pings

Key points to check:

- **Reply received** → connectivity is working
- **Request timed out** → host unreachable or network issue
- **Packet loss percentage** → indicates network quality problems

---

### Using `traceroute`

`traceroute` shows the **path packets take through the network** to reach the destination.

Syntax:

    traceroute <hostname or IP>

Example:

    traceroute google.com

How to interpret the output:

- Each line represents a **network hop (router or device)**.
- `* * *` indicates **no response from that hop**, possibly due to a firewall or network issue.
- **High latency at a hop** may indicate network congestion.

Alternative tool: `mtr`

`mtr` combines the functionality of **ping and traceroute** and provides real-time statistics.

Installation:

    sudo apt install mtr

Usage:

    mtr google.com

---

### Using `netstat` or `ss`

These commands display **network connections, listening ports, and statistics**.

Check listening ports:

    netstat -tuln
    ss -tuln

Options explanation:

- `-t` → TCP ports
- `-u` → UDP ports
- `-l` → listening ports
- `-n` → numeric addresses

Check established connections:

    netstat -an | grep ESTABLISHED
    ss -ant

Check network statistics:

    netstat -s

This displays detailed network statistics such as packet errors and retransmissions.

---

### Using `ifconfig` or `ip`

These commands verify **network interface status and IP configuration**.

Commands:

    ifconfig
    ip addr show
    ip link show

Explanation:

- `ifconfig` → older method for viewing interface configuration
- `ip addr show` → modern replacement
- `ip link show` → checks interface status (UP/DOWN)

Check gateway connectivity:

    ip route

Then ping the gateway:

    ping <gateway IP>

---

### Using `dig` or `nslookup`

These tools check **DNS resolution**.

Examples:

    dig google.com
    nslookup google.com

How to verify DNS:

- If an **IP address is returned** → DNS is working
- If an **error occurs** → DNS configuration problem

---

### Using `curl` or `wget`

These tools test **application-level connectivity**, particularly HTTP/HTTPS services.

Examples:

Check HTTP headers:

    curl -I https://google.com

Check site reachability:

    wget --spider https://google.com

These commands confirm whether the web service is reachable.

---

### Using `tcpdump`

`tcpdump` captures and analyzes **real-time network traffic**, useful for advanced troubleshooting.

Capture packets on an interface:

    sudo tcpdump -i eth0

Capture traffic for a specific port:

    sudo tcpdump -i eth0 port 80

This helps identify whether packets are reaching the system.

---

### Troubleshooting Workflow Using Multiple Tools

A structured troubleshooting approach may include the following steps.

Step 1: Check basic connectivity

    ping 8.8.8.8

---

Step 2: Check DNS resolution

    ping google.com
    dig google.com

---

Step 3: Trace the network path

    traceroute google.com

---

Step 4: Check active connections and listening ports

    ss -tuln
    netstat -an

---

Step 5: Check network interface and gateway

    ip addr
    ip route
    ping <gateway IP>

---

Step 6: Test application-level connectivity

    curl -I https://example.com
    wget --spider https://example.com

---

Step 7: Analyze traffic if needed

    sudo tcpdump -i eth0

---

### Tricky Interview Questions

How do you check if your DNS is working?

Use:

    dig <domain>

or

    nslookup <domain>

---

What is the difference between `ping` and `traceroute`?

- `ping` checks **basic connectivity**
- `traceroute` shows **the path packets take to reach a destination**

---

How do you check which process is using a port?

    ss -tulnp

or

    netstat -tulnp

---

How do you troubleshoot slow network performance?

- Check **ping latency and packet loss**
- Use **traceroute or mtr** to find congested hops
- Check interface statistics:

    ifconfig
    ip -s link

- Analyze traffic using:

    tcpdump

---

### Interview Summary

Network connectivity in Linux can be diagnosed using tools such as `ping` for basic connectivity, `traceroute` for path analysis, `netstat` or `ss` for network connections, `ip` for interface configuration, `dig` for DNS resolution, and tools like `curl`, `wget`, and `tcpdump` for deeper application-level and packet-level analysis.
