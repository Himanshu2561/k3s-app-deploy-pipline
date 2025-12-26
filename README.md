# 🚀 Learning Pipeline: Platform App Deployment

Welcome to the **Platform App Deployment** project! This repository serves as a learning journey into modern DevOps practices, focusing on containerization, security hardening, and Kubernetes orchestration.

## 🏗️ Architecture Overview

This pipeline demonstrates a complete flow from development to deployment, emphasizing **Security-First** and **Infrastructure-as-Code** principles.

### 💻 Technical Stack

| Category             | Technology                       |
| :------------------- | :------------------------------- |
| **Containerization** | Docker                           |
| **Registry**         | GitHub Container Registry (GHCR) |
| **Orchestration**    | Kubernetes                       |
| **Security**         | Trivy, K8s SecurityContext       |
| **CI/CD**            | GitHub Actions                   |

---

## 🛠️ Components

### 1. Docker & GHCR

The application is containerized and hosted on **GitHub Container Registry (GHCR)**.

- **Image**: `ghcr.io/himanshu2561/platform-app`
- **Best Practices**: Using specific tags (SHA-based) for immutability and reproducibility.

### 2. Kubernetes Deployment (`deployment.yaml`)

A robust deployment configuration featuring:

- **Scalability**: Configured with `2 replicas` for high availability.
- **Health Checks**:
  - `readinessProbe`: Ensures traffic only hits healthy pods.
  - `livenessProbe`: Automatically restarts failing pods.
- **Resource Management**: Defined CPU/Memory requests and limits to ensure cluster stability.
- **Security**:
  - `runAsNonRoot: true`
  - `allowPrivilegeEscalation: false`

### 3. Kubernetes Service (`service.yaml`)

- **Type**: ClusterIP (internal exposure).
- **Port Mapping**: Forwards traffic from port `80` to container port `8000`.

---

## 🔒 Security Best Practices implemented

This project specifically focuses on "Security by Design":

- ✅ **Non-root Execution**: The container runs with a non-privileged user (UID 1000).
- ✅ **Vulnerability Scanning**: Pipeline integration with **Trivy** to catch OS and library vulnerabilities early.
- ✅ **Minimal Privileges**: Explicitly disabling privilege escalation in the pod spec.

---

## 🚀 Getting Started

### Prerequisites

- A Kubernetes cluster (Minikube, Kind, or managed K8s).
- `kubectl` configured to point to your cluster.

### Deployment Steps

1. **Create the Namespace**:

   ```bash
   kubectl create namespace platform-app
   ```

2. **Apply the Manifests**:

   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

3. **Verify the Deployment**:
   ```bash
   kubectl get pods -n platform-app
   kubectl get svc -n platform-app
   ```

---

## 📈 Learning Goals achieved

- [x] Setting up a GitHub Actions workflow for Docker builds.
- [x] Fixing Docker tag casing issues for GHCR compatibility.
- [x] Hardening Docker images based on security scan results.
- [x] Writing production-ready Kubernetes manifests.

---

## � Observability & Debugging

Useful commands for monitoring the application:

- **Check Logs**: `kubectl logs -l app=platform-app -n platform-app`
- **Check Events**: `kubectl get events -n platform-app --sort-by='.lastTimestamp'`
- **Check Health**: `kubectl describe deployment platform-app -n platform-app`

---

## 🗺️ Roadmap

- [ ] Implement Helm charts for templated deployments.
- [ ] Add Prometheus/Grafana for monitoring.
- [ ] Integrate an Ingress Controller (Nginx/Traefik).
- [ ] Set up automated Canary deployments.

---

## �📄 License

This project is for educational purposes.

---

_Built with ❤️ for the DevOps learning journey._
