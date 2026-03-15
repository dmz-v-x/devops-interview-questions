### Question
What is the difference between `curl` and `wget`?

### Answer

`curl` and `wget` are command-line tools used in Linux to **transfer data over networks**, commonly using protocols like HTTP, HTTPS, and FTP. Although they appear similar, they serve different primary purposes.

- `curl` is mainly used for **data transfer and interacting with APIs**.
- `wget` is mainly used for **downloading files from the internet**.

---

### Overview

| Feature | `curl` | `wget` |
|-------|-------|-------|
| Purpose | Transfers data from/to a server | Downloads files from the internet |
| Protocols | HTTP, HTTPS, FTP, FTPS, SCP, SFTP, LDAP, etc. | HTTP, HTTPS, FTP |
| Installation | Usually pre-installed or via package manager | Usually pre-installed or via package manager |
| Focus | Data transfer (flexible, scripting) | File downloading |
| Output | Prints response to terminal (STDOUT) by default | Saves output directly to a file |
| Resuming | Supported with `-C -` option | Supported with `-c` option |
| Recursive download | Not supported | Supported |
| Scripting | Excellent for APIs and HTTP requests | Mainly used for downloading files |

---

### The `curl` Command

Purpose: `curl` is used to **transfer data to or from a server** and is commonly used for:

- API testing
- Sending HTTP requests
- Uploading files
- Automation scripts

Default behavior: Prints the response directly to the terminal.

Syntax:

    curl [options] <URL>

Examples:

Simple GET request:

    curl https://example.com

Save output to a file:

    curl -o filename.html https://example.com

Follow redirects:

    curl -L https://short.url

Download using FTP:

    curl -u user:pass ftp://example.com/file.txt

Send POST request with data:

    curl -X POST -d "name=John&age=30" https://api.example.com/user

---

### The `wget` Command

Purpose: `wget` is primarily designed to **download files from the internet**. It supports features such as resuming downloads, recursive downloads, and background downloads.

Default behavior: Automatically saves the downloaded file in the current directory.

Syntax:

    wget [options] <URL>

Examples:

Download a single file:

    wget https://example.com/file.zip

Resume a partially downloaded file:

    wget -c https://example.com/file.zip

Download an entire website recursively:

    wget -r -np -k https://example.com/

Download in background:

    wget -b https://example.com/file.zip

Limit download speed:

    wget --limit-rate=100k https://example.com/file.zip

---

### Key Differences

| Feature | `curl` | `wget` |
|------|------|------|
| Output behavior | Prints to STDOUT by default | Automatically saves file |
| Resume downloads | `-C -` option | `-c` option |
| Recursive downloads | Not supported | Supported |
| API requests | Supports GET, POST, PUT, DELETE | Mainly for downloading files |
| Background downloads | Requires additional scripting | Supported using `-b` |
| FTP/SFTP support | Supported | Supported |

---

### Practical Use Cases

Use `curl` for:

- Testing APIs (GET, POST, PUT requests)
- Sending custom HTTP headers
- Uploading files via FTP or SFTP
- Automation and scripting tasks

Use `wget` for:

- Downloading large files
- Resuming interrupted downloads
- Downloading entire websites
- Background downloads

---

### Interview / Tricky Questions

Can `curl` download files?

Yes. It can download files using:

    curl -O <URL>

or

    curl -o filename <URL>

However, its primary purpose is **data transfer and HTTP interaction**.

---

Can `wget` send POST requests?

No. `wget` is mainly designed for **file downloading**, while `curl` is preferred for sending HTTP requests with data.

---

Which tool is better for downloading an entire website?

`wget`, because it supports **recursive downloads**.

Example:

    wget -r https://example.com

---

How do you resume a broken download?

Using `wget`:

    wget -c <URL>

Using `curl`:

    curl -C - -O <URL>

---

### Interview Summary

`curl` and `wget` are both network data transfer tools. `curl` is more flexible and commonly used for interacting with APIs and sending HTTP requests, while `wget` is optimized for downloading files, supporting features like recursive downloads, resume capability, and background downloading.
