### Question  
What are logs, metrics, and traces in observability?

---

### Answer  

---

### 1. Logs

---

#### What They Are

- Immutable, timestamped records of events  

- Example:

```text
2025-08-21 12:00:01 ERROR PaymentService – Transaction failed for user 123
```

---

#### Use Cases

- Debugging issues  
- Root cause analysis  
- Understanding exact context  

---

#### Challenges

- High volume  
- Requires indexing/search tools (ELK, Loki)  

---

### 2. Metrics

---

#### What They Are

- Numeric data representing system state over time  

- Example:

```text
http_requests_total{status="500"} 45
```

---

#### Types (Prometheus)

- Counter  
- Gauge  
- Histogram  
- Summary  

---

#### Use Cases

- Monitoring system health  
- Alerting  
- Trend analysis  

---

#### Challenges

- Shows:
  - “What is wrong”  
- Does NOT explain:
  - “Why it is wrong”  

---

### 3. Traces 

---

#### What They Are

- Track a single request across services  

- Example flow:

```text
API → Payment Service → DB → External API
```

---

#### Use Cases

- Debug latency  
- Identify bottlenecks  
- Understand service interactions  

---

#### Challenges

- Requires instrumentation  
  - OpenTelemetry  
  - Jaeger  
  - AWS X-Ray  

---

### 4. Observability Perspective

```text
Logs   → What happened  
Metrics → What is happening  
Traces → Where and why it happened  
```

---

### 5. How They Work Together

1. Metric alert triggers  
2. Check logs for detailed context  
3. Use traces to follow request flow  

---

### 6. Key Takeaways

- Logs:
  - Detailed debugging  

- Metrics:
  - Monitoring & alerting  

- Traces:
  - Distributed system visibility  

---

### 7. Interview-Ready Summary

“Logs, metrics, and traces are the three pillars of observability. Logs provide detailed event-level information for debugging, metrics give aggregated numerical insights for monitoring and alerting, and traces show the end-to-end flow of requests across distributed systems. In practice, I use them together — for example, when a latency alert is triggered, I analyze metrics, check logs for context, and follow traces to identify the root cause.”
