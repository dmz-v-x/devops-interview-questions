### Question  
How do you make a process persistent after the shell/session dies in Linux?

---

### Answer  

When a shell session ends (logout, SSH disconnect), processes started from that shell usually terminate. To keep a process running, you can use the following methods:

---

### 1. Using `nohup` (Most Common)

```bash
nohup command &
```

#### Example:
```bash
nohup python app.py &
```

#### How it works:
- `nohup` = *no hangup*  
- Prevents process from receiving SIGHUP signal  
- Output is redirected to:
```
nohup.out
```

---

### 2. Using `&` (Background Process)

```bash
command &
```

#### Limitation:
- Runs in background  
- Still tied to terminal  
- Will stop if shell closes  

---

### 3. Using `disown`

```bash
command &
disown
```

#### How it works:
- Removes process from shell job control  
- Prevents it from being killed when shell exits  

---

### 4. Using `screen` (Terminal Multiplexer)

```bash
screen
```

#### Steps:
- Start screen session  
- Run your command  
- Detach:
```
Ctrl + A, then D
```

#### Reattach:
```bash
screen -r
```

---

### 5. Using `tmux` (Modern Alternative to screen)

```bash
tmux
```

#### Detach:
```
Ctrl + B, then D
```

#### Reattach:
```bash
tmux attach
```

---

### 6. Using `systemd` (Best for Production)

Create a service:

```bash
sudo nano /etc/systemd/system/myapp.service
```

#### Example:

```ini
[Unit]
Description=My App

[Service]
ExecStart=/usr/bin/python3 /home/ubuntu/app.py
Restart=always
User=ubuntu

[Install]
WantedBy=multi-user.target
```

#### Commands:

```bash
sudo systemctl daemon-reexec
sudo systemctl enable myapp
sudo systemctl start myapp
```

---

### 7. Comparison

| Method     | Use Case                    | Persistence Level |
| ---------- | --------------------------- | ----------------- |
| `nohup`    | Simple background jobs      | Medium            |
| `disown`   | Quick fix for running jobs  | Medium            |
| `screen`   | Interactive sessions        | High              |
| `tmux`     | Advanced session handling   | High              |
| `systemd`  | Production services         | Very High         |

---

### 8. Best Practice

- Use:
  - `nohup` → quick tasks  
  - `tmux` / `screen` → interactive work  
  - `systemd` → production apps  

---

### 9. Interview-Ready Summary

“To keep a process running after the shell exits, I can use nohup or disown for simple cases. For interactive sessions, I use tmux or screen. In production environments, I prefer creating a systemd service so the process runs reliably and restarts automatically if it fails.”
