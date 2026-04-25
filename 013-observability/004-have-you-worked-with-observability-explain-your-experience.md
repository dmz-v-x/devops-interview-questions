### Question  
Have you worked with observability? Explain your experience.

---

### Answer  

---

### 1. Overview

- Yes, I’ve worked extensively with **observability**  
- Goal:
  - Not just detect issues  
  - But understand **why they happen**  

---

### 2. Metrics

- Used:
  - Prometheus for scraping metrics  

- Instrumented applications using:
  - Prometheus client libraries  

- Captured:
  - Request latency (p95, p99)  
  - Error rates  
  - Queue depth  

---

#### Dashboards (Grafana)

- Infrastructure:
  - CPU, memory, pod restarts  

- Application:
  - Latency, error rates  

- Business:
  - Orders, payments  

---

#### Example Alert

```text
p99 latency > 2s for 5 minutes
```

---

### 3. Logs

- Applications:
  - Emit structured JSON logs to stdout/stderr  

- Collection:
  - Fluent Bit  

- Storage:
  - Loki / ELK  

---

#### Use Case

- Debug user issue:
  - Correlate logs across services  

---

### 4. Tracing

- Tools:
  - OpenTelemetry  
  - AWS X-Ray  

- Added:
  - Trace IDs in logs  

---

#### Example

- Trace request:
  - API → Service → DB  
- Identify:
  - Slow DB query causing latency  

---

### 5. Alerting & SLOs

- Defined:
  - SLIs:
    - Latency  
    - Error rate  
    - Availability  

- Set:
  - SLOs (e.g., 99.9% requests < 200ms)  

- Alerts:
  - Prometheus Alertmanager  
  - CloudWatch  

- Integrated with:
  - Slack  
  - PagerDuty  

---

### 6. Observability Stack

- Metrics:
  - Prometheus  

- Visualization:
  - Grafana  

- Logs:
  - Fluent Bit + Loki / ELK  

- Tracing:
  - OpenTelemetry + X-Ray  

---

### 7. Outcome

- Benefits:
  - Faster MTTR  
  - Better root cause analysis  
  - Improved system visibility  

---

### 8. Key Takeaways

- Observability = Logs + Metrics + Traces  
- Enables:
  - Deep debugging  
  - Proactive monitoring  

---

### 9. Interview-Ready Summary

“Yes, I’ve built observability systems using Prometheus and Grafana for metrics, Fluent Bit with Loki or ELK for logs, and OpenTelemetry with X-Ray for distributed tracing. I instrumented applications to emit custom metrics and structured logs, created dashboards for infrastructure and business KPIs, and defined SLO-based alerts integrated with Slack and PagerDuty. This approach helped us quickly identify not just when issues occurred, but also why, significantly reducing MTTR.”
