### Question  
What is the difference between Monitoring and Observability?

---

### Answer  

---

### 1. Definitions

---

#### Monitoring

- Collects:
  - Predefined metrics and logs  

- Purpose:
  - Detect known issues  

- Example:
  - CPU > 80% → trigger alert  

- Answers:
  - “Is the system working?”  

---

#### Observability

- Uses:
  - Logs + Metrics + Traces  

- Purpose:
  - Diagnose unknown issues  

- Example:
  - Trace a request across services → find bottleneck  

- Answers:
  - “Why is the system not working?”  

---

### 2. Core Difference

```text
Monitoring → Known problems (alerts you expect)  
Observability → Unknown problems (debugging new issues)
```

---

### 3. Practical Example

- Monitoring:
  - Alert: High latency detected  

- Observability:
  - Trace request → find slow DB query  
  - Correlate logs → identify root cause  

---

### 4. Comparison Table

| Aspect            | Monitoring                        | Observability                             |
|------------------|----------------------------------|-------------------------------------------|
| **Purpose**      | Detect known issues              | Diagnose unknown issues                   |
| **Scope**        | Predefined metrics/alerts        | Logs + Metrics + Traces                   |
| **Question**     | “Is it working?”                 | “Why is it not working?”                  |
| **Approach**     | Reactive alerts                  | Exploratory debugging                     |
| **Tools**        | CloudWatch, Nagios, Zabbix       | ELK, Datadog, Prometheus, X-Ray           |

---

### 5. Key Takeaways

- Monitoring:
  - Alert-driven  
  - Limited to known scenarios  

- Observability:
  - Deep system insight  
  - Helps debug unexpected issues  

---

### 6. Interview-Ready Summary

“Monitoring focuses on collecting predefined metrics and setting alerts to detect known issues, answering whether a system is working or not. Observability goes a step further by using logs, metrics, and traces together to understand why a system is failing, even for issues that were not anticipated. In short, monitoring tells you that something is wrong, while observability helps you understand why it’s wrong.”
