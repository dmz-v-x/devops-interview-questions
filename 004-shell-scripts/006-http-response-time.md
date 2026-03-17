### Question  
How does this Shell Script check HTTP response time, and how does it work step by step?

---

### Answer  

### Complete Script  

    #!/bin/bash
    # HTTP Response Time Check Script

    URL="https://example.com"

    response_time=$(curl -o /dev/null -s -w '%{time_total}\n' "$URL")
    echo "Response time: ${response_time}s"

    # Alert if response > 2 seconds
    if (( $(echo "$response_time > 2" | bc -l) )); then
        echo "WARNING: Slow response time!" >&2
        exit 1
    fi

---

### 1. Script Overview  

This script measures the **HTTP response time** of a given URL and:

- Uses `curl` to send a request  
- Extracts total response time  
- Prints the response time  
- Triggers a warning if it exceeds **2 seconds**  

---

### 2. Code Breakdown  

---

#### Shebang  

    #!/bin/bash

- Runs the script using the **Bash shell**

---

#### Define URL  

    URL="https://example.com"

- The target endpoint to test  

---

#### Measure Response Time  

    response_time=$(curl -o /dev/null -s -w '%{time_total}\n' "$URL")

Breakdown:

1. `curl`:
   - Sends HTTP request  

2. `-o /dev/null`:
   - Discards response body  

3. `-s`:
   - Silent mode (no progress output)  

4. `-w '%{time_total}'`:
   - Prints total request time  

Example output:

    0.245

---

#### Print Response Time  

    echo "Response time: ${response_time}s"

- Displays measured time in seconds  

---

#### Compare Response Time  

    if (( $(echo "$response_time > 2" | bc -l) )); then

- Bash cannot compare floating numbers directly  
- `bc -l` is used for **floating-point comparison**  

Example:

    echo "0.245 > 2" | bc -l → 0  
    echo "3.1 > 2" | bc -l → 1  

---

#### Warning Case  

    echo "WARNING: Slow response time!" >&2
    exit 1

- Prints warning to **stderr**  
- Exits with failure status  

---

### 3. Execution Flow  

1. Script starts  
2. Sends HTTP request using `curl`  
3. Captures total response time  
4. Prints response time  
5. Compares with threshold (2 seconds)  
6. If exceeded:
   - Prints warning  
   - Exits with error  
7. Otherwise exits normally  

---

### 4. Real-World Use Cases  

---

Monitor API performance:

    ./response_check.sh

---

Used in uptime monitoring scripts  

---

CI/CD performance checks before deployment  

---

Check latency of external services  

---

---

### 5. Improvements / Best Practices  

---

#### Set Timeout for Curl  

    curl --max-time 5 ...

- Prevents hanging requests  

---

#### Track HTTP Status Code  

    curl -o /dev/null -s -w '%{http_code} %{time_total}\n' "$URL"

---

#### Retry on Failure  

    curl --retry 3 --retry-delay 2 ...

---

#### Make Threshold Configurable  

    THRESHOLD=2

---

#### Log Results  

    echo "$(date) - $response_time" >> response.log

---

### 6. Tricky Interview Questions  

---

Why use `/dev/null`?  

- Discards response body to improve performance  

---

Why use `-s`?  

- Suppresses progress and error output  

---

Why use `bc -l`?  

- Bash does not support floating-point comparison natively  

---

What is `%{time_total}`?  

- Total time taken for the request (DNS + TCP + TLS + transfer)  

---

What happens if `curl` fails?  

- May return empty or invalid value → should be handled in production  

---

### Interview Summary  

This script measures HTTP response time using `curl`, compares it against a threshold using `bc`, and triggers alerts for slow responses. It is commonly used in performance monitoring, health checks, and DevOps automation.
