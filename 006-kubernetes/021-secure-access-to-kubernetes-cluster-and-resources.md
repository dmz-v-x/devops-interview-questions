### Question  
You need to secure access to your Kubernetes cluster and resources. Describe your approach to Kubernetes authentication and authorization.

---

### Answer  

### 1. Authentication (Who You Are)  

Kubernetes verifies identity using multiple methods.

---

#### A. Client Certificates  

- Certificates signed by cluster CA  

Example:

    users:
    - name: dev-user
      user:
        client-certificate: /path/to/cert.crt
        client-key: /path/to/key.key

---

#### B. Token-Based Authentication  

- ServiceAccount tokens (for pods)  
- Bearer tokens (for users/automation)  

---

#### C. OIDC (Recommended for Users)  

- Integrate with:

  - Google  
  - Azure AD  
  - Keycloak  

Benefits:

- Centralized identity  
- SSO support  

---

#### D. Basic Auth (Not Recommended)  

- Only for testing  
- Avoid in production  

---

#### E. Authentication Flow  

- User sends token/certificate  
- API server verifies identity  
- Passes identity to authorization  

---

### 2. Authorization (What You Can Do)  

---

#### A. RBAC (Most Common)  

Define permissions via Roles:

    apiVersion: rbac.authorization.k8s.io/v1
    kind: Role
    metadata:
      namespace: dev
      name: pod-reader
    rules:
      - apiGroups: [""]
        resources: ["pods"]
        verbs: ["get", "watch", "list"]

Bind role:

    apiVersion: rbac.authorization.k8s.io/v1
    kind: RoleBinding
    metadata:
      name: read-pods
      namespace: dev
    subjects:
      - kind: User
        name: dev-user
        apiGroup: rbac.authorization.k8s.io
    roleRef:
      kind: Role
      name: pod-reader
      apiGroup: rbac.authorization.k8s.io

---

#### B. ABAC (Less Common)  

- Policy-based access control  
- Harder to manage at scale  

---

#### C. Webhook Authorization  

- External authorization service  
- Custom logic  

---

### 3. Best Practices  

| Aspect              | Recommendation                         |
|---------------------|----------------------------------------|
| Human users         | OIDC + RBAC                            |
| Applications        | ServiceAccounts                        |
| Least Privilege     | Minimal required permissions           |
| Multi-tenancy       | Namespaces + RBAC                      |
| Audit Logging       | Enable API server audit logs           |

---

### 4. Additional Security Layers  

---

#### Network Policies  

- Restrict pod-to-pod communication  

---

#### Pod Security / Admission Controllers  

- Enforce security rules  
- Prevent privileged containers  

---

#### Secrets Security  

- Use Secrets + encryption  
- Prefer external secret managers  

---

#### TLS Encryption  

- Secure API server communication  

---

### 5. End-to-End Flow  

1. User authenticates via OIDC / token / cert  
2. API server validates identity  
3. RBAC checks permissions  
4. Request allowed or denied  
5. Action logged via audit logs  

---

### 6. Summary  

| Layer           | Purpose                          |
|-----------------|----------------------------------|
| Authentication  | Verify identity                  |
| Authorization   | Control access                   |
| RBAC            | Define permissions               |
| Network Policy  | Control network traffic          |
| Audit Logs      | Track actions                    |

---

### 7. Key Insight  

- Security = **Authentication + Authorization + Network + Policy layers**  
- RBAC is the **core control mechanism**  

---

### Interview Summary  

To secure a Kubernetes cluster, use strong authentication mechanisms like OIDC or certificates, and enforce authorization using RBAC with least privilege principles. Combine this with network policies, secure secret management, TLS encryption, and audit logging to create a layered security model that protects both cluster access and workloads.
