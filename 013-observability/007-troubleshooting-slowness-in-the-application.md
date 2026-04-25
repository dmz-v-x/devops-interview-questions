### Question  
Users report slowness in the application, but logs show no errors and CPU usage is normal. How would you troubleshoot?

---

### Answer  

---

### 1. Start with Metrics (Infra + Application)

---

#### Infrastructure Metrics

- Even if CPU is fine, check:
  - Memory usage  
  - Disk I/O / latency (EBS, DB)  
  - Network throughput / packet drops  

- Possible issues:
  - Disk bottleneck  
  - Network saturation  

---

#### Application Metrics

- Check:
  - Latency (p95, p99)  
  - Error rate (even small spikes)  
  - Throughput  

- Look for:
  - Slow endpoints  
  - Increased response times  

---

#### Database Metrics

- Slow queries  
- Lock contention  
- Connection pool exhaustion  

---

#### Queue Metrics

- Kafka / SQS / RabbitMQ:
  - Queue backlog  
  - Consumer lag  

---

### 2. Use Distributed Tracing

---

- Tools:
  - Jaeger  
  - AWS X-Ray  
  - OpenTelemetry  

- Trace a request across services:

```text
API → Service → DB → External API
```

- Identify:
  - Which component is slow  

---

### 3. Check External Dependencies

---

- Third-party APIs:
  - Payment gateways  
  - External services  

- Network issues:
  - DNS latency  
  - Cross-region calls  

---

### 4. Check Kubernetes / Cloud Factors

---

- Pod-level issues:
  - CPU throttling  
  - Memory limits  

- Scaling issues:
  - HPA not scaling  

- Load balancer:
  - Retries  
  - Health checks  

---

### 5. Check Business Metrics

---

- Traffic spike  
- Large payloads  
- Specific user flows affected  

---

### 6. Deep Debugging (If Needed)

---

- Enable debug logs for sample requests  
- Run synthetic tests  
- Compare with historical baselines  

---

### 7. Observability Approach

---

- Metrics:
  - Identify latency increase  

- Logs:
  - Correlate request-level data  

- Traces:
  - Pinpoint bottleneck  

---

### 8. Key Takeaways

- CPU ≠ full system health  
- Slowness often caused by:
  - DB issues  
  - Network latency  
  - External dependencies  

---

### 9. Interview-Ready Summary

“If users report slowness but CPU and logs look normal, I’d check other infrastructure metrics like memory, disk I/O, and network usage. Then I’d analyze application latency metrics such as p95 and p99, along with database performance and queue backlogs. I’d use distributed tracing to follow requests across services and identify bottlenecks. I’d also verify external dependencies, Kubernetes throttling, and traffic patterns. In most cases, slowness is caused by database or network issues rather than CPU.”
