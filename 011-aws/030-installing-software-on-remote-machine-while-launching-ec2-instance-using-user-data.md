### Question  
How do you install Apache automatically while launching an EC2 instance using User Data?

---

### Answer  

When launching an EC2 instance, you can use the **User Data** field to provide a startup script that installs Apache automatically.

---

### 1. Steps

- Create an EC2 instance (via AWS Console, AWS CLI, or SDK).  
- In the **User Data field** (under Advanced settings), provide a shell script.  
- This script runs automatically on first boot.  

---

### 2. Example User Data Script (Amazon Linux 2)

```bash
#!/bin/bash
# Update packages
yum update -y

# Install Apache (httpd)
yum install -y httpd

# Start and enable Apache
systemctl start httpd
systemctl enable httpd

# Create a test page
echo "<h1>Hello from Apache on EC2</h1>" > /var/www/html/index.html
```

---

### 3. Using AWS CLI

You can pass the script when launching the instance:

```bash
aws ec2 run-instances \
  --image-id ami-08c40ec9ead489470 \
  --instance-type t2.micro \
  --key-name my-keypair \
  --security-group-ids sg-1234567890abcdef \
  --subnet-id subnet-12345678 \
  --user-data file://userdata.sh \
  --count 1
```

*(where `userdata.sh` contains the script above)*

---

### 4. How it works

- User Data runs at first boot via **cloud-init**  
- Apache (`httpd`) is installed, started, and enabled to survive reboots  
- The test page becomes accessible on **port 80** (if allowed by security group)  

---

### 5. Key Takeaways

- User Data automates instance configuration  
- Runs only on first boot (by default)  
- Useful for bootstrapping servers  
- Eliminates manual setup steps  

---

### 6. Interview-Ready Summary

“When launching an EC2 instance, I use the User Data field to pass a shell script that installs and configures Apache automatically. The script runs during the first boot using cloud-init, installs httpd, starts the service, and deploys a test page. This ensures the server is ready immediately after launch without manual intervention.”
