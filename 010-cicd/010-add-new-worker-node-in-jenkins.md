### Question  
How do you add a new worker node in Jenkins?

---

### 1. Overview

A **worker node (agent)** in Jenkins is used to:
- Execute build jobs  
- Distribute workload  
- Improve scalability and performance  

The Jenkins master (controller) delegates tasks to these agents.

---

### 2. Step-by-Step Process to Add a New Worker Node

---

### 2.1 Navigate to Nodes Section

- Login to Jenkins UI  
- Go to:

```
Manage Jenkins → Manage Nodes and Clouds → New Node
```

---

### 2.2 Create a New Node

#### Steps:
- Enter a **Node Name**  
- Select:
  - **Permanent Agent**  

Click **OK**

---

### 2.3 Configure Node Details

Fill in the required configuration:

#### Basic Settings:
- **Number of executors** → Number of parallel builds  
- **Remote root directory** → e.g., `/home/jenkins`  
- **Labels** → e.g., `linux`, `docker`, `java`  
- **Usage**:
  - Use this node as much as possible  
  - Only build jobs with matching label  

---

### 2.4 Configure Launch Method (SSH - Most Common)

#### Select:
- **Launch agents via SSH**

#### Provide:
- Host (IP/DNS of agent machine)  
- Credentials (SSH key or username/password)  

---

### 2.5 Save and Launch

- Click **Save**  
- Jenkins will attempt to connect and launch the agent  

#### Status:
- If successful → Node shows as **online**  

---

### 3. Alternative Ways to Add Agents

---

### 3.1 JNLP (Agent initiated connection)

- Agent connects to Jenkins using a secret key  
- Useful when:
  - Agent cannot be accessed via SSH  
  - Behind firewall  

---

### 3.2 Docker Agents

- Dynamically spin up containers as agents  
- Useful for:
  - Ephemeral builds  
  - Clean environments  

---

### 3.3 Cloud Agents (AWS, Kubernetes)

- Auto-scale agents using:
  - AWS EC2 plugin  
  - Kubernetes plugin  

---

### 4. Prerequisites

- Java installed on agent machine  
- Network connectivity between master and agent  
- Proper SSH access (if using SSH method)  

---

### 5. Key Benefits of Worker Nodes

- Load distribution  
- Faster build execution  
- Isolation of environments  
- Scalability  

---

### 6. Key Takeaways

- Add node via **Manage Jenkins → Nodes → New Node**  
- Configure using **SSH / JNLP / Cloud methods**  
- Assign labels for better job targeting  

---

### 7. Interview-Ready Summary

“To add a new worker node in Jenkins, I go to Manage Jenkins → Manage Nodes → New Node, provide a name, and select ‘Permanent Agent’. Then I configure details like executors, labels, and remote directory. I typically use SSH as the launch method by providing the agent’s IP and credentials. Once saved, Jenkins connects to the agent and brings it online for executing builds.”
