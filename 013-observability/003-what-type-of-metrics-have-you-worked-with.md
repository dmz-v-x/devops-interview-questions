### Question  
What types of metrics have you worked with in a DevOps environment?

---

### Answer  

---

### 1. Overview

- Metrics are typically categorized into:
  - Infrastructure metrics  
  - Application metrics  
  - Business metrics  
  - Reliability metrics (SLI/SLO)  

- Tools used:
  - Prometheus  
  - CloudWatch  
  - Grafana  

---

### 2. Infrastructure Metrics (System-Level)

---

#### Compute

- CPU utilization  
- Memory usage  
- Disk I/O  
- Network in/out  

- Kubernetes-specific:
  - Pod restarts  
  - Node pressure (OOM, disk)  

---

#### Storage

- EBS:
  - IOPS  
  - Throughput  
  - Latency  

- EFS:
  - Burst credits  

---

#### Networking

- Packet drops  
- Network errors  
- Load balancer request count  

---

#### Example Alert

```text
CPU > 80% for 5 minutes
Pod restarts exceed threshold
```

---

### 3. Application Metrics (Service-Level)

---

#### Request Metrics

- Request count  
- Latency (p95, p99)  
- Error rates (4xx, 5xx)  

---

#### Internal Metrics

- DB connections  
- Queue depth (Kafka, SQS, RabbitMQ)  

---

#### Example Alert

```text
p99 latency > 2 seconds
Error rate > 5%
```

---

### 4. Business Metrics (Product-Level)

- Orders placed  
- Payments processed  
- User signups/logins  
- Conversion rates  

---

#### Example Alert

```text
Drop in successful payments compared to baseline
```

---

### 5. Reliability Metrics (SLI/SLO)

---

#### SLI (Service Level Indicators)

- Availability  
- Latency  
- Error rate  

---

#### SLO (Objectives)

- Example:
  - 99.9% requests < 200ms  

---

#### Error Budget

- Allowed failure within SLO window  

---

### 6. Observability Setup

---

#### Collection

- Prometheus:
  - Scrapes `/metrics`  

- CloudWatch:
  - AWS infrastructure metrics  

---

#### Visualization

- Grafana dashboards:
  - Infra  
  - App performance  
  - Business KPIs  

---

#### Alerting

- Prometheus Alertmanager  
- CloudWatch Alarms  
- Integrations:
  - Slack  
  - PagerDuty  

---

#### Tracing

- Tools:
  - Jaeger  
  - AWS X-Ray  

- Purpose:
  - Debug request flow  

---

### 7. Key Takeaways

- Combine:
  - Infra + App + Business metrics  

- Focus on:
  - User experience  
  - System health  
  - Business impact  

---

### 8. Interview-Ready Summary

“I’ve worked with infrastructure metrics like CPU, memory, and pod restarts; application metrics like request latency, throughput, and error rates; and business KPIs such as orders and payments. We used Prometheus for collection, Grafana for visualization, and set up SLO-based alerts. This approach provided full visibility into system performance, user experience, and business impact.”
