### Question  
You’ve received a CSV file with a list of usernames and passwords to create users on a Linux system.  

Task:  
Write a shell script to:  
- Create each user with the specified password  
- Force password change on first login  

---

### Answer  

---

### 1. Sample CSV File

```
username,password
alice,Password@123
bob,Secure@456
carol,DevOps@789
```

---

### 2. Shell Script

```bash
#!/bin/bash

INPUT="users.csv"

# Check if the file exists
if [[ ! -f "$INPUT" ]]; then
  echo "CSV file not found!"
  exit 1
fi

# Skip header and read each line
tail -n +2 "$INPUT" | while IFS=',' read -r username password; do

  # Check if user already exists
  if id "$username" &>/dev/null; then
    echo "User '$username' already exists. Skipping..."
    continue
  fi

  # Create the user
  useradd "$username"

  # Set the password
  echo "${username}:${password}" | chpasswd

  # Force password change on first login
  chage -d 0 "$username"

  echo "User '$username' created successfully."

done
```

---

### 3. How to Execute

```bash
chmod +x create_users.sh
sudo ./create_users.sh
```

- Requires **root privileges** to create users  

---

### 4. Script Breakdown

- `IFS=',' read -r username password`  
  - Splits CSV into username and password  

- `useradd "$username"`  
  - Creates a new Linux user  

- `chpasswd`  
  - Sets password securely via stdin  

- `chage -d 0 "$username"`  
  - Forces password reset on first login  

- `id "$username"`  
  - Checks if user already exists  

---

### 5. Enhancements (Best Practices)

- Create home directory:

```bash
useradd -m "$username"
```

- Set default shell:

```bash
useradd -m -s /bin/bash "$username"
```

- Add logging:

```bash
echo "$(date) - Created user: $username" >> user_creation.log
```

- Validate input format before processing  

---

### 6. Key Takeaways

- Automates bulk user creation  
- Ensures security with forced password reset  
- Prevents duplicate user creation  

---

### 7. Interview-Ready Summary

“I would write a shell script that reads the CSV file line by line, creates users using useradd, sets passwords using chpasswd, and forces password reset on first login using chage -d 0. I would also include checks to avoid duplicate users and ensure the script runs with root privileges.”
