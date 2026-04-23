### Question  
How do you add a new plugin in Jenkins?

---

### 1. Overview

Plugins in Jenkins are used to **extend functionality**, such as:
- Integrating with tools (Git, Docker, Kubernetes)  
- Adding new features (pipelines, notifications, security)  

Jenkins provides multiple ways to install plugins.

---

### 2. Methods to Add a Plugin

---

### 2.1 Using Jenkins UI (Most Common)

#### Steps:

1. Go to:
```
Manage Jenkins → Manage Plugins
```

2. Navigate to:
- **Available** tab → to install new plugins  
- **Installed** tab → to view existing plugins  

3. Search for the plugin (e.g., Git, Docker, Pipeline)

4. Select the plugin checkbox  

5. Click:
- **Install without restart** (recommended)  
  OR  
- **Download now and install after restart**

---

#### Key Points:
- Automatically installs dependencies  
- Easy and user-friendly  

---

### 2.2 Using Jenkins CLI

#### Command:
```
java -jar jenkins-cli.jar install-plugin <PLUGIN_NAME>
```

#### Example:
```
java -jar jenkins-cli.jar install-plugin git
```

#### Requirements:
- Jenkins CLI jar file  
- Proper authentication  

---

#### Key Points:
- Useful for automation/scripts  
- Common in DevOps pipelines  

---

### 2.3 Using Plugin File (.hpi / .jpi)

#### Steps:
1. Download plugin file manually  
2. Go to:
```
Manage Jenkins → Manage Plugins → Advanced
```

3. Upload the `.hpi` or `.jpi` file  

---

#### Use Case:
- Offline environments  
- Restricted networks  

---

### 3. Restart Jenkins (If Required)

- Some plugins require restart  

#### Restart options:
```
Manage Jenkins → Restart Jenkins
```

---

### 4. Best Practices

- Install only required plugins  
- Keep plugins updated  
- Check compatibility with Jenkins version  
- Avoid plugin conflicts  

---

### 5. Key Takeaways

- UI method is most commonly used  
- CLI is useful for automation  
- Manual upload works in offline setups  

---

### 6. Interview-Ready Summary

“To add a plugin in Jenkins, I usually go to Manage Jenkins → Manage Plugins, search for the required plugin in the Available tab, and install it. Alternatively, plugins can be installed using the Jenkins CLI with the install-plugin command or by uploading a .hpi file in the Advanced section. The UI method is the most common and user-friendly approach.”
