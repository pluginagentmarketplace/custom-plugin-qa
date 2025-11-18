---
name: docker-kubernetes-mastery
description: Master Docker containerization, Kubernetes orchestration, and modern DevOps practices. Learn container management, deployment strategies, and infrastructure automation.
---

# Docker & Kubernetes Mastery

## Quick Start

### Docker Basics
```dockerfile
# Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install --production

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]
```

### Docker Compose
```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: app
      POSTGRES_PASSWORD: secret
```

### Kubernetes Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: app
  template:
    metadata:
      labels:
        app: app
    spec:
      containers:
      - name: app
        image: myapp:1.0
        ports:
        - containerPort: 3000
```

## Docker Fundamentals

### Images & Containers
- Dockerfile best practices
- Image layers and caching
- Multi-stage builds
- Image size optimization
- Registry management (Docker Hub, ECR, GCR)
- Image versioning and tagging

### Container Lifecycle
- Container creation and startup
- Process management (PID 1)
- Signal handling (SIGTERM)
- Graceful shutdown
- Resource limits (CPU, memory)
- Logging and monitoring

### Networking
- Container networking
- Port mapping
- Docker bridge networks
- Custom networks
- DNS in Docker
- Service discovery

### Volumes & Persistence
- Volume types (named, bind, tmpfs)
- Volume drivers
- Data persistence strategies
- Backup and restore
- Volume permissions

### Docker Compose
- Service definitions
- Multi-container orchestration
- Environment variables
- Health checks
- Networking between services
- Volume management

## Kubernetes

### Core Concepts
- Pods: Smallest deployable unit
- Services: Network abstraction
- Deployments: Application management
- StatefulSets: Stateful applications
- DaemonSets: Node-level services
- Jobs and CronJobs: Batch processing

### Pod Management
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp
spec:
  containers:
  - name: app
    image: myapp:1.0
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
        port: 8080
      initialDelaySeconds: 30
      periodSeconds: 10
```

### Deployments
- Rolling updates
- Blue-green deployments
- Canary deployments
- Rollback strategies
- Revision history
- Update strategies

### Services & Networking
- ClusterIP: Internal service
- NodePort: External access
- LoadBalancer: Cloud load balancer
- Ingress: HTTP(S) routing
- Service mesh (Istio, Linkerd)
- Network policies

### Storage
- PersistentVolumes (PV)
- PersistentVolumeClaims (PVC)
- Storage classes
- Stateful data management
- Backup strategies
- Data replication

### Configuration Management
- ConfigMaps: Non-sensitive data
- Secrets: Sensitive data
- Environment variables
- Volume mounting
- Secret encryption at rest
- GitOps for configuration

### Cluster Administration
- Node management
- RBAC: Role-based access control
- Pod Security Policies
- Network policies
- Resource quotas
- Namespace isolation

### Monitoring & Logging
- Prometheus for metrics
- Grafana for visualization
- ELK Stack for logs
- Distributed tracing
- Alerts and notifications
- Performance analysis

## Container Registries

### Docker Hub
- Public repositories
- Private repositories
- Image organizations
- Automated builds
- Webhooks

### Enterprise Registries
- Private Docker Registry
- Harbor: Enterprise container registry
- AWS ECR: Elastic Container Registry
- Google Container Registry (GCR)
- Azure Container Registry (ACR)

### Image Management
- Image scanning and security
- Access control
- Retention policies
- Vulnerability detection
- Image signatures

## Container Security

### Image Security
- Minimal base images (Alpine)
- Layer scanning
- Vulnerability scanning
- Build security
- Image signing and verification

### Runtime Security
- Container isolation
- Seccomp profiles
- AppArmor/SELinux
- Root vs rootless containers
- Privileged mode restrictions
- Network policies

### Secrets Management
- Kubernetes Secrets
- HashiCorp Vault
- Cloud provider secret stores
- Encryption at rest
- Rotation strategies

## CI/CD with Containers

### Build Pipelines
- Multi-stage builds for optimization
- Docker buildkit
- Build caching strategies
- Parallel builds
- Security scanning in CI

### Deployment Pipelines
```yaml
# GitHub Actions example
name: Deploy
on: [push]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Build
        run: docker build -t myapp:${{ github.sha }} .
      - name: Deploy
        run: kubectl set image deployment/app app=myapp:${{ github.sha }}
```

## Orchestration Best Practices

### High Availability
- Multiple replicas
- Pod disruption budgets
- Anti-affinity rules
- Resource requests/limits
- Health checks
- Automatic restart

### Scaling
- Horizontal Pod Autoscaling (HPA)
- Vertical Pod Autoscaling (VPA)
- Cluster autoscaling
- Load balancing
- Sharding strategies

### Cost Optimization
- Right-sizing containers
- Resource requests accuracy
- Spot instances
- Reserved instances
- Multi-tenancy
- Container consolidation

## Advanced Topics

### Service Mesh
- Istio: Advanced traffic management
- Linkerd: Lightweight service mesh
- Circuit breaking
- Retry policies
- Rate limiting
- Observability

### Serverless on Kubernetes
- Knative: Serverless runtime
- Function frameworks
- Event-driven architecture
- Auto-scaling to zero

### GitOps
- ArgoCD: Declarative deployment
- Flux: GitOps operator
- Infrastructure as code
- Version control for deployment
- Automated sync

## Best Practices

✅ Use minimal base images (Alpine)
✅ Don't run as root
✅ Use health checks
✅ Set resource requests/limits
✅ Use multi-stage builds
✅ Scan images for vulnerabilities
✅ Use namespaces for isolation
✅ Implement RBAC
✅ Regular updates and patching
✅ Monitor and log everything

❌ Don't store secrets in images
❌ Don't use latest tags in production
❌ Don't run privileged containers
❌ Don't skip security policies
❌ Don't hardcode configuration
❌ Don't neglect resource limits
❌ Don't trust any image source

## Related Skills
- System Architecture
- Security & Best Practices
- Backend Development

## Next Steps
Containerize applications, deploy to Kubernetes, and master container orchestration at scale.
