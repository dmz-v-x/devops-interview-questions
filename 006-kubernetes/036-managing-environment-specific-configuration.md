### Question  
You need to deploy a Kubernetes application across multiple environments (dev, staging, production) with different configurations. How would you manage environment-specific configurations in Kubernetes?

---

### Answer  

### 1. Use ConfigMaps (Non-Sensitive Config)  

- Store environment-specific settings  

Example (dev):

    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: myapp-config
      namespace: dev
    data:
      LOG_LEVEL: DEBUG
      API_ENDPOINT: https://dev-api.example.com

- Create separate ConfigMaps per environment  

---

### 2. Use Secrets (Sensitive Data)  

- Store:

  - Passwords  
  - API keys  
  - Tokens  

Example:

    apiVersion: v1
    kind: Secret
    metadata:
      name: myapp-secret
      namespace: production
    type: Opaque
    data:
      DB_PASSWORD: cHJvZF9wYXNz

---

### 3. Inject Config into Pods  

---

#### Environment Variables  

    envFrom:
      - configMapRef:
          name: myapp-config
      - secretRef:
          name: myapp-secret

---

#### Volume Mount (Optional)  

- For file-based configs  

---

### 4. Use Separate Namespaces  

Create isolation:

    kubectl create namespace dev
    kubectl create namespace staging
    kubectl create namespace prod

Benefits:

- Environment isolation  
- Easier RBAC control  

---

### 5. Use Helm (Templating)  

- Manage configs via values files  

Example:

    helm install myapp ./chart -f values-dev.yaml --namespace dev
    helm install myapp ./chart -f values-prod.yaml --namespace prod

- Each environment has different values  

---

### 6. Use Kustomize (Overlays)  

Structure:

    base/
    overlays/
      dev/
      staging/
      prod/

- Patch environment-specific configs  
- Avoid duplication  

---

### 7. Best Practices  

- Do NOT hardcode configs  
- Encrypt secrets:

  - Sealed Secrets  
  - SOPS  
  - Vault  

- Use:

  - Namespaces + RBAC  
  - GitOps for consistency  

---

### 8. Summary  

| Component     | Purpose                                |
|---------------|----------------------------------------|
| ConfigMap     | Non-sensitive config                   |
| Secret        | Sensitive data                         |
| Namespace     | Environment isolation                  |
| Helm          | Templating per environment             |
| Kustomize     | Overlay-based config management        |

---

### 9. Key Insight  

- Separate:
  - Code → same across environments  
  - Config → different per environment  

---

### Interview Summary  

To manage environment-specific configurations in Kubernetes, use ConfigMaps for non-sensitive data and Secrets for sensitive data, combined with namespaces for isolation. Tools like Helm and Kustomize help manage environment-specific variations without duplicating manifests, ensuring consistency and scalability across dev, staging, and production.
