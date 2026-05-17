# Kubernetes

Kubernetes (K8s) is the de facto standard for orchestrating containerized workloads
at scale. It handles scheduling, scaling, self-healing, service discovery, and
rolling updates across clusters of machines.

---

## Why Kubernetes

Running a single container with Docker is simple. Running hundreds of containers
across dozens of machines raises hard problems:
- Which machine should run which container?
- What happens when a container crashes?
- How do containers find each other?
- How do you update 50 containers with zero downtime?
- How do you scale under load?

Kubernetes solves all of these.

---

## Architecture

### Control Plane

The control plane makes global decisions about the cluster:

| Component | Role |
|-----------|------|
| **kube-apiserver** | Front door for all cluster operations; validates and processes API requests |
| **etcd** | Distributed key-value store; source of truth for all cluster state |
| **kube-scheduler** | Assigns pods to nodes based on resource needs and constraints |
| **kube-controller-manager** | Runs controllers that reconcile desired state with actual state |
| **cloud-controller-manager** | Integrates with cloud providers (load balancers, volumes, nodes) |

### Worker Nodes

Each node runs:

| Component | Role |
|-----------|------|
| **kubelet** | Agent that ensures containers in pods are running and healthy |
| **kube-proxy** | Network proxy; maintains iptables/ipvs rules for service routing |
| **container runtime** | Runs containers: containerd, CRI-O (Docker removed in 1.24) |

---

## Core Objects

### Pod

The smallest deployable unit. One or more containers that share network and storage.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
    - name: nginx
      image: nginx:1.25
      ports:
        - containerPort: 80
      resources:
        requests:
          memory: "64Mi"
          cpu: "250m"
        limits:
          memory: "128Mi"
          cpu: "500m"
      livenessProbe:
        httpGet:
          path: /health
          port: 80
        initialDelaySeconds: 10
        periodSeconds: 15
      readinessProbe:
        httpGet:
          path: /ready
          port: 80
        initialDelaySeconds: 5
        periodSeconds: 5
      env:
        - name: APP_ENV
          value: production
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: app-secrets
              key: db-password
      volumeMounts:
        - name: config-vol
          mountPath: /etc/app/config
  volumes:
    - name: config-vol
      configMap:
        name: app-config
```

**Probes**:
- `livenessProbe`: is the container alive? Restart if fails.
- `readinessProbe`: is the container ready for traffic? Remove from Service if fails.
- `startupProbe`: has the app started? Delays liveness/readiness checks.

**Resource requests vs limits**:
- `requests`: minimum guaranteed resources (used for scheduling)
- `limits`: maximum allowed resources (CPU throttled, Memory → OOMKill)

---

### Deployment

Manages a ReplicaSet (which manages Pods). The primary way to run stateless apps.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  namespace: production
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0    # Never reduce below desired count
  template:
    metadata:
      labels:
        app: myapp
        version: v1.2.3
    spec:
      containers:
        - name: myapp
          image: myapp:1.2.3
          ports:
            - containerPort: 8080
          resources:
            requests:
              memory: "256Mi"
              cpu: "100m"
            limits:
              memory: "512Mi"
              cpu: "500m"
      topologySpreadConstraints:
        - maxSkew: 1
          topologyKey: kubernetes.io/hostname
          whenUnsatisfiable: DoNotSchedule
          labelSelector:
            matchLabels:
              app: myapp
```

```bash
kubectl rollout status deployment/myapp
kubectl rollout history deployment/myapp
kubectl rollout undo deployment/myapp
kubectl rollout undo deployment/myapp --to-revision=2
kubectl set image deployment/myapp myapp=myapp:1.2.4
```

---

### StatefulSet

For stateful applications that need stable network identities and persistent storage
(databases, message queues, Elasticsearch).

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: postgres
spec:
  serviceName: postgres-headless    # Must match a headless Service
  replicas: 3
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
        - name: postgres
          image: postgres:15
          volumeMounts:
            - name: pgdata
              mountPath: /var/lib/postgresql/data
  volumeClaimTemplates:
    - metadata:
        name: pgdata
      spec:
        accessModes: [ReadWriteOnce]
        storageClassName: gp3
        resources:
          requests:
            storage: 20Gi
```

Pods get stable names: `postgres-0`, `postgres-1`, `postgres-2`.
Stable DNS: `postgres-0.postgres-headless.default.svc.cluster.local`

---

### Services

Stable network endpoint for a set of Pods.

```yaml
# ClusterIP: internal-only (default)
apiVersion: v1
kind: Service
metadata:
  name: myapp
spec:
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 8080

---
# LoadBalancer: provisions cloud load balancer
apiVersion: v1
kind: Service
metadata:
  name: myapp-lb
spec:
  type: LoadBalancer
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 8080

---
# NodePort: exposes on each node's IP
apiVersion: v1
kind: Service
metadata:
  name: myapp-nodeport
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30080     # 30000-32767
```

---

### Ingress

HTTP/HTTPS routing into the cluster. Requires an Ingress Controller (Nginx, Traefik, AWS ALB).

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  ingressClassName: nginx
  tls:
    - hosts:
        - myapp.example.com
      secretName: myapp-tls
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: myapp
                port:
                  number: 80
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: myapp-api
                port:
                  number: 8080
```

---

### ConfigMap and Secret

```yaml
# ConfigMap
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_ENV: production
  LOG_LEVEL: info
  config.yaml: |
    server:
      port: 8080
      timeout: 30s

---
# Secret (values are base64 encoded, not encrypted by default)
apiVersion: v1
kind: Secret
metadata:
  name: app-secrets
type: Opaque
data:
  db-password: cGFzc3dvcmQ=   # base64 of "password"
  api-key: YWJjMTIz
```

```bash
kubectl create secret generic app-secrets \
  --from-literal=db-password=mysecretpassword \
  --from-file=tls.crt=./cert.pem

kubectl create configmap app-config --from-file=config.yaml
```

**Secret encryption at rest**: by default secrets are base64 in etcd (not encrypted).
Enable `--encryption-provider-config` in kube-apiserver or use external-secrets-operator.

---

### Namespace

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: production
  labels:
    environment: production
```

```bash
kubectl create namespace staging
kubectl get all -n production
kubectl config set-context --current --namespace=production
```

---

### PersistentVolume and PersistentVolumeClaim

```yaml
# PVC: request for storage (usually all you need with dynamic provisioning)
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgres-data
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: gp3           # AWS gp3 EBS volumes
  resources:
    requests:
      storage: 20Gi
```

**Access modes**:
- `ReadWriteOnce` (RWO): single node read/write
- `ReadOnlyMany` (ROX): many nodes read-only
- `ReadWriteMany` (RWX): many nodes read/write (requires NFS, EFS, Ceph)

---

## RBAC

```yaml
# Role: namespace-scoped permissions
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: production
  name: pod-reader
rules:
  - apiGroups: [""]
    resources: ["pods", "pods/log"]
    verbs: ["get", "list", "watch"]

---
# RoleBinding: assign Role to a subject
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: production
subjects:
  - kind: ServiceAccount
    name: monitoring-agent
    namespace: monitoring
  - kind: User
    name: alice@example.com
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## kubectl Reference

```bash
# Context and cluster
kubectl config get-contexts
kubectl config use-context prod-cluster
kubectl config set-context --current --namespace=production

# Get resources
kubectl get pods
kubectl get pods -o wide                  # Show node and IP
kubectl get pods -l app=myapp             # Label selector
kubectl get pods --all-namespaces
kubectl get all -n production

# Describe (detailed info + events)
kubectl describe pod myapp-abc123
kubectl describe node worker-1

# Logs
kubectl logs myapp-abc123
kubectl logs myapp-abc123 -c sidecar      # Specific container
kubectl logs -f myapp-abc123              # Follow
kubectl logs --previous myapp-abc123      # Previous container instance

# Exec
kubectl exec -it myapp-abc123 -- bash
kubectl exec myapp-abc123 -- curl localhost:8080/health

# Port forward
kubectl port-forward pod/myapp-abc123 8080:8080
kubectl port-forward svc/myapp 8080:80

# Apply and delete
kubectl apply -f manifest.yml
kubectl apply -f k8s/
kubectl delete -f manifest.yml
kubectl delete pod myapp-abc123

# Scale
kubectl scale deployment myapp --replicas=5

# Resource usage
kubectl top nodes
kubectl top pods -n production

# Events
kubectl get events --sort-by=.metadata.creationTimestamp -n production

# Edit live resource
kubectl edit deployment myapp
```

---

## Helm

Helm is the package manager for Kubernetes.

```bash
# Add a chart repository
helm repo add stable https://charts.helm.sh/stable
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

# Search
helm search repo nginx
helm search hub postgresql

# Install
helm install my-nginx bitnami/nginx
helm install my-postgres bitnami/postgresql \
  --set auth.postgresPassword=mypassword \
  --set primary.persistence.size=20Gi \
  --namespace databases

# Install with values file
helm install myapp ./charts/myapp -f values.prod.yaml

# Upgrade
helm upgrade myapp ./charts/myapp -f values.prod.yaml --install

# List and status
helm list -A
helm status myapp

# Rollback
helm rollback myapp 1    # Roll back to revision 1

# Template (preview rendered manifests)
helm template myapp ./charts/myapp -f values.prod.yaml

# Uninstall
helm uninstall myapp
```

**Chart structure**:

```
my-app/
├── Chart.yaml        # Chart metadata
├── values.yaml       # Default values
├── templates/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   ├── configmap.yaml
│   └── _helpers.tpl  # Template helpers
└── charts/           # Dependency charts
```

---

## Horizontal Pod Autoscaler (HPA)

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: myapp-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp
  minReplicas: 2
  maxReplicas: 20
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
    - type: Resource
      resource:
        name: memory
        target:
          type: Utilization
          averageUtilization: 80
```

Requires `metrics-server` installed in the cluster.

---

## Troubleshooting Common Issues

### CrashLoopBackOff

```bash
kubectl describe pod myapp-abc123    # Check Events section
kubectl logs myapp-abc123
kubectl logs --previous myapp-abc123  # Logs from crashed container
```

Common causes: application crash on startup, missing env vars, missing secrets.

### Pending Pod

```bash
kubectl describe pod myapp-abc123
# Look for: "Insufficient cpu", "Insufficient memory", "no nodes available"
kubectl describe node worker-1       # Check node capacity
kubectl top nodes                    # Check actual usage
```

Common causes: insufficient cluster resources, taint/toleration mismatch, PVC not bound.

### OOMKilled

```bash
kubectl describe pod myapp-abc123   # Shows OOMKilled in Last State
```

Fix: increase memory limit or optimize application memory usage.

### Service Not Routing Traffic

```bash
kubectl get endpoints myapp         # Should show pod IPs
kubectl describe service myapp      # Check selector matches pod labels
kubectl get pods -l app=myapp       # Verify labels match
```

---

## Managed Kubernetes

| Provider | Service | Notes |
|----------|---------|-------|
| AWS | EKS | Managed control plane; node groups or Fargate (serverless nodes) |
| GCP | GKE | Best Kubernetes integration; Autopilot mode manages nodes |
| Azure | AKS | Free control plane; good Azure AD integration |

All managed services handle control plane HA, upgrades, and etcd backups.
You still manage worker nodes (unless using Fargate/Autopilot).
