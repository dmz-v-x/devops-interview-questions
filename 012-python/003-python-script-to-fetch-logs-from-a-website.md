### Question  
Python script to fetch logs from a log website and print all logs with 404: not found

---

### Answer  

---

### 1. Overview

- Goal:
  - Fetch logs from a URL  
  - Filter lines containing HTTP **404**  
  - Print matching logs  

- Tool used:
  - `requests` library  

---

### 2. Python Script

```python
import requests

# Publicly available Apache log sample
log_url = "https://raw.githubusercontent.com/elastic/examples/master/Common%20Data%20Formats/apache_logs/apache_logs"

try:
    # Fetch logs
    response = requests.get(log_url)
    response.raise_for_status()

    # Split logs into lines
    logs = response.text.splitlines()

    print("Log lines with 404 Not Found:\n")

    # Filter logs with 404 status
    for line in logs:
        if " 404 " in line:
            print(line)

except requests.exceptions.RequestException as e:
    print(f"Error fetching logs: {e}")
```

---

### 3. How It Works

- `requests.get()`  
  - Fetches log file from URL  

- `response.text.splitlines()`  
  - Converts log into list of lines  

- `" 404 " in line`  
  - Filters only HTTP 404 responses  
  - Avoids false matches  

---

### 4. Example Output

```
216.46.173.126 - - [27/May/2015:10:27:47 +0000] "GET /presentations/logstash-monitorama-2013/images/kibana-search.png HTTP/1.1" 404 146
```

---

### 5. Enhancements

- Save output to file:

```python
with open("404_logs.txt", "w") as f:
    for line in logs:
        if " 404 " in line:
            f.write(line + "\n")
```

- Count occurrences:

```python
count = sum(1 for line in logs if " 404 " in line)
print(f"Total 404 errors: {count}")
```

- Filter other status codes:
  - `" 500 "` → server errors  
  - `" 403 "` → forbidden  

---

### 6. Key Takeaways

- Useful for:
  - Log analysis  
  - Monitoring errors  
  - Debugging applications  

- Simple pipeline:
  - Fetch → Parse → Filter → Output  

---

### 7. Interview-Ready Summary

“I would use Python’s requests library to fetch logs from a URL, split them into lines, and filter for entries containing HTTP 404 status codes. This allows quick analysis of error logs and can be extended to count occurrences or write results to a file for further investigation.”
