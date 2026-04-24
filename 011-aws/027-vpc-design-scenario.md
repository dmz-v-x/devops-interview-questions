### Question:

I have three EC2 machines A, B and C. A is deployed in VPC A while B and C are deployed in VPC B. Now I want that Applications running on EC2 A also interacts with the application running on EC2 B but at the same time I want that application A should not interact with Application C and vice versa. What kind of setup you will do for this? 

---

Here’s a step-by-step approach to setting this up:

---

### 1. VPC Peering between VPC A and VPC B

Since EC2 A is in VPC A and EC2 B and C are in VPC B, you need to establish VPC Peering between VPC A and VPC B to enable communication between EC2 A and EC2 B.

#### Create VPC Peering Connection:

- Go to the VPC Dashboard in the AWS Management Console.  
- Select Peering Connections and create a new peering connection between VPC A and VPC B.  
- After the connection is established, accept the request on the other side (VPC B).  

#### Update Route Tables:

- In both VPCs, update the route tables to allow traffic to flow between the VPCs.  

- For example:
  - In VPC A's route table, add a route for traffic destined for VPC B's CIDR block via the peering connection.  
  - Similarly, in VPC B's route table, add a route for traffic destined for VPC A's CIDR block via the peering connection.  

**Why:** VPC peering allows communication between instances in different VPCs.

---

### 2. Use Security Groups for Fine-Grained Control

Security groups can be used to control inbound and outbound traffic at the instance level. We will configure security groups to ensure the desired access between EC2 A and EC2 B while restricting communication with EC2 C.

---

#### Setup:

##### For EC2 A (in VPC A):

- Create a security group (SG-A) for EC2 A in VPC A that only allows inbound traffic from EC2 B's private IP address (in VPC B).  

- Deny communication from EC2 C by not allowing EC2 C’s IP or security group ID in the inbound rules.  

##### Example:

**Inbound rules for SG-A:**
- Allow inbound traffic on the required ports (e.g., HTTP, HTTPS) from the private IP of EC2 B.  
- Block inbound traffic from EC2 C (not specifying EC2 C’s IP or security group ID).  

---

##### For EC2 B (in VPC B):

- Create a security group (SG-B) for EC2 B that allows inbound traffic from EC2 A.  

- Make sure to deny traffic from EC2 C by not specifying the IP or security group of EC2 C in the inbound rules.  

##### Example:

**Inbound rules for SG-B:**
- Allow inbound traffic on the required ports (e.g., HTTP, HTTPS) from the private IP of EC2 A.  
- Block inbound traffic from EC2 C (again, by not including EC2 C’s IP or security group ID).  

---

##### For EC2 C (in VPC B):

- Create a security group (SG-C) for EC2 C.  

- This security group should not allow communication with EC2 A but can be open to other services within VPC B (or restricted further, depending on your use case).  

---

**Why:** Security groups provide fine-grained control over which instances can communicate with each other. By controlling the inbound/outbound traffic, you can ensure that A can talk to B, but A cannot talk to C, and vice versa.

---

### 3. Control Traffic with Network Access Control Lists (NACLs)

NACLs provide an additional layer of security at the subnet level, allowing you to control traffic entering and leaving a subnet. While security groups control traffic at the instance level, NACLs operate at the subnet level.

---

#### Setup:

##### For VPC A:

- You can configure NACLs to allow traffic from VPC B (and specifically EC2 B) to reach EC2 A, but block traffic from EC2 C.  

- Ensure egress rules on VPC A’s NACL allow traffic destined to VPC B's CIDR block (where EC2 B is located).  

---

##### For VPC B:

- Configure NACLs for the subnets hosting EC2 B and C to ensure traffic from EC2 A can reach EC2 B, but EC2 C cannot communicate with EC2 A.  

- For instance:
  - Allow inbound traffic on the relevant ports from VPC A’s CIDR block (allowing EC2 A to talk to EC2 B).  
  - Block inbound traffic from VPC A’s CIDR block on the relevant ports to EC2 C.  

---

**Why:** NACLs allow you to block or permit traffic at the subnet level, providing an additional layer of security beyond what is provided by security groups.

---

### 4. Network Routing and Segmentation (Optional)

To further isolate EC2 A, B, and C, you can use PrivateLink, VPC Endpoints, or even Transit Gateway if you want to manage traffic more granularly between multiple VPCs.

---

#### For example:

- AWS Transit Gateway can be used if you have complex networking needs and multiple VPCs.  
- You can create routing policies that enforce traffic isolation between different EC2 instances.  

---

**Why:** This is an optional step, but can be useful in larger, more complex environments where more control over inter-VPC traffic is needed.

---

### 5. Testing and Validation

After the setup, ensure the following:

- EC2 A can communicate with EC2 B.  
- EC2 A cannot communicate with EC2 C (and vice versa).  

- Check the logs and test connectivity to ensure the security groups and NACLs are working as expected.  

- Use:
```bash
ping
curl
telnet
```

- Monitor logs for blocked traffic if you're using logging for NACLs.  

---

### Summary of the Setup:

- VPC Peering between VPC A (EC2 A) and VPC B (EC2 B and C) to enable inter-VPC communication.  

- Use Security Groups:
  - EC2 A’s security group allows traffic from EC2 B but not from EC2 C.  
  - EC2 B’s security group allows traffic from EC2 A but not from EC2 C.  
  - EC2 C’s security group restricts access to EC2 A.  

- (Optional) Use NACLs to further enforce traffic rules at the subnet level, controlling inbound and outbound traffic.  

- Test and validate the configuration to ensure that the traffic flows as expected between EC2 A and EC2 B but not with EC2 C.  

---

By using VPC peering, security groups, and NACLs, you can easily set up the required communication rules between EC2 instances in different VPCs while ensuring traffic isolation where necessary.
