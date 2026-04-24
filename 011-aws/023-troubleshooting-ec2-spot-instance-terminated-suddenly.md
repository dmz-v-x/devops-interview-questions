### Question  
EC2 Spot Instance terminated suddenly — How would you troubleshoot and handle it?

---

### 1. Overview

Spot Instances can be terminated by AWS when:
- Spot price exceeds your bid  
- Capacity is no longer available  

This is expected behavior, so handling it requires **resilience and fault tolerance**.

---

### 2. Step-by-Step Troubleshooting

---

### 2.1 Check Spot Price History

- Go to:
  - EC2 → Spot Requests → Pricing History  

#### Purpose:
- Identify if price exceeded your max bid  

---

### 2.2 Verify Maximum Bid Price

- If using manual bidding:
  - Increase max price  

#### Note:
- Modern AWS uses “capacity-optimized” strategy instead of bidding  

---

### 2.3 Check Interruption Notices

- AWS provides:
  - 2-minute termination warning  

#### Check:
```bash
http://169.254.169.254/latest/meta-data/spot/instance-action
```

---

### 3. Recovery and Mitigation

---

### 3.1 Use Auto Scaling Group

- Configure ASG to:
  - Automatically replace terminated instances  

---

### 3.2 Use Spot Fleet / Mixed Instances

- Combine:
  - Spot + On-Demand  

#### Benefit:
- Higher availability  

---

### 3.3 Store Data in Persistent Storage

- Use:
  - EBS volumes  
  - S3  

#### Avoid:
- Storing critical data on instance store  

---

### 4. Best Practices

- Use **stateless applications**  
- Enable **graceful shutdown using interruption notice**  
- Use **multiple instance types and AZs**  
- Use **capacity-optimized allocation strategy**  

---

### 5. Key Takeaways

- Spot instances are not guaranteed  
- Always design for failure  
- Use Auto Scaling and mixed capacity  
- Persist data outside instances  

---

### 6. Interview-Ready Summary

“If a Spot instance is terminated, I first check the spot price history to see if the price exceeded the configured limit. I also check for interruption notices. To handle this, I use Auto Scaling Groups or Spot Fleet with a mix of Spot and On-Demand instances to ensure availability. I also store critical data in persistent storage like EBS or S3. Since Spot instances can be terminated anytime, I design applications to be stateless and fault-tolerant.”
