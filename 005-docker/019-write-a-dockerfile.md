### Question  
Write a Dockerfile using Linux and a web server, and explain how to build and run it.

---

### Answer  

### Complete Dockerfile  

    # Use an official Ubuntu base image
    FROM ubuntu:20.04

    # Disable interactive prompts
    ENV DEBIAN_FRONTEND=noninteractive

    # Update and install nginx
    RUN apt-get update && \
        apt-get install -y nginx && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*

    # Copy custom HTML file (optional)
    # COPY index.html /var/www/html/index.html

    # Expose port 80
    EXPOSE 80

    # Run nginx in foreground
    CMD ["nginx", "-g", "daemon off;"]

---

### 1. Script Overview  

This Dockerfile:

- Uses **Ubuntu (Linux)** as base  
- Installs **NGINX web server**  
- Exposes port **80**  
- Runs nginx in foreground  

---

### 2. Code Breakdown  

---

#### Base Image  

    FROM ubuntu:20.04

- Starts from Ubuntu Linux  

---

#### Disable Prompts  

    ENV DEBIAN_FRONTEND=noninteractive

- Prevents installation prompts during build  

---

#### Install NGINX  

    RUN apt-get update && \
        apt-get install -y nginx

- Updates package list  
- Installs nginx  

---

#### Cleanup  

    apt-get clean && rm -rf /var/lib/apt/lists/*

- Reduces image size  

---

#### Copy HTML (Optional)  

    COPY index.html /var/www/html/index.html

- Adds custom webpage  

---

#### Expose Port  

    EXPOSE 80

- Tells Docker container will use port 80  

---

#### Start Server  

    CMD ["nginx", "-g", "daemon off;"]

- Runs nginx in foreground  
- Keeps container alive  

---

### 3. Build the Image  

    docker build -t my-nginx-server .

---

### 4. Run the Container  

    docker run -d -p 8080:80 my-nginx-server

---

### 5. Access Application  

Open in browser:

    http://localhost:8080

---

### 6. Key Concept  

- Container runs only while nginx runs  
- `daemon off;` ensures nginx stays in foreground  

---

### 7. Real-World Use Cases  

---

Host static websites  

---

Serve frontend applications  

---

Reverse proxy setups  

---

---

### 8. Tricky Interview Questions  

---

Why use `daemon off;`?  

- Keeps nginx in foreground  

---

What happens if nginx runs in background?  

- Container exits  

---

Why clean apt cache?  

- Reduce image size  

---

### Interview Summary  

This Dockerfile uses Ubuntu as the base OS, installs nginx, and runs it in the foreground to serve web content. The container exposes port 80 and can be accessed via a mapped host port, making it a simple example of running a web server in Docker.
