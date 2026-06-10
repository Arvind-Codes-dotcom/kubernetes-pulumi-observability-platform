# Troubleshooting Steps

## Overview

This document captures issues encountered during deployment and validation of the Kubernetes Guestbook Observability Platform, along with investigation steps, root cause analysis, and resolutions.

---

# Issue 1: Kubernetes Cluster Not Reachable

Running:

```bash
kubectl get nodes
```

returned:

```text
Unable to connect to the server
```

---

## Root Cause

Kubernetes was not enabled in Docker Desktop.

No local Kubernetes control plane was available.

---

## Resolution

Enabled Kubernetes within Docker Desktop.

Validation:

```bash
kubectl get nodes
```

Result:

```text
docker-desktop Ready
```

---

# Issue 2: Pulumi CLI Not Available

Running:

```bash
pulumi version
```

returned:

```text
Command not found
```

---

## Root Cause

Pulumi CLI was not installed or not available in the system PATH.

---

## Resolution

Installed Pulumi using:

```powershell
winget install Pulumi.Pulumi
```

Verified installation:

```bash
pulumi version
```

---

# Issue 3: Node.js Not Installed

Running:

```bash
node --version
npm --version
```

returned:

```text
Command not found
```

---

## Root Cause

Node.js runtime was not installed.

Pulumi TypeScript projects require Node.js and npm.

---

## Resolution

Installed Node.js LTS release.

Validated:

```bash
node --version
npm --version
```

---

# Issue 4: Guestbook Application Not Accessible

Frontend service deployed successfully.

Application was not accessible through:

```text
http://localhost:<NodePort>
```

---

## Investigation

Validated service:

```bash
kubectl describe svc frontend
```

Validated endpoints:

```bash
kubectl get endpoints frontend
```

Observed:

* Service healthy
* Endpoints available
* Pods healthy

---

## Root Cause

Docker Desktop LoadBalancer implementation behaved differently from cloud-managed Kubernetes services.

Service exposure did not function as expected through assigned NodePort.

---

## Resolution

Used Kubernetes port-forwarding:

```bash
kubectl port-forward svc/frontend 8080:80
```

Application successfully accessed through:

```text
http://localhost:8080
```

---

# Issue 5: Helm Release Timeout


Pulumi deployment failed with:

```text
context deadline exceeded
```

during monitoring stack deployment.

---

## Investigation

Checked monitoring namespace:

```bash
kubectl get pods -n monitoring
```

Observed:

* Grafana running
* Prometheus running
* Alertmanager running

---

## Root Cause

Helm release timeout occurred before all resources reported healthy status.

Monitoring components were successfully deployed despite timeout.

---

## Resolution

Validated deployment through Kubernetes resources rather than relying solely on Helm release status.

Confirmed:

* Prometheus operational
* Grafana operational
* Monitoring functional

---

# Issue 6: Node Exporter CrashLoopBackOff


Node exporter entered:

```text
CrashLoopBackOff
```

state.

---

## Investigation

Executed:

```bash
kubectl describe pod
```

Observed:

```text
path / is mounted on / but it is not a shared or slave mount
```

---

## Root Cause

Docker Desktop Kubernetes restricts host filesystem mounts required by node-exporter.

Node exporter expects Linux host mount propagation capabilities not fully available in Docker Desktop.

---

## Resolution

Documented as a local environment limitation.

Impact assessment:

* Prometheus operational
* Grafana operational
* kube-state-metrics operational
* Dashboard functionality operational

No impact to project objectives.

---

# Issue 7: Grafana Not Accessible Through LoadBalancer


Grafana service displayed:

```text
EXTERNAL-IP <pending>
```

---

## Root Cause

Docker Desktop Kubernetes does not provision cloud LoadBalancer resources.

---

## Resolution

Used port forwarding:

```bash
kubectl port-forward -n monitoring svc/kube-prometheus-stack-4b698e00-grafana 3000:80
```

Accessed Grafana through:

```text
http://localhost:3000
```

---

# Issue 8: Prometheus Verification


Validate that Prometheus was collecting Kubernetes workload metrics.

---

## Validation Queries

Pod Discovery:

```promql
kube_pod_info
```

Pod Status:

```promql
kube_pod_status_phase
```

---

## Result

Prometheus successfully discovered:

* Frontend Pods
* Redis Leader
* Redis Replica

Metrics collection confirmed operational.

---

# Lessons Learned

This implementation reinforced several operational concepts:

* Infrastructure as Code deployment workflows
* Kubernetes service troubleshooting
* Helm deployment validation
* Prometheus target verification
* Grafana dashboard creation
* Observability platform troubleshooting
* Root cause analysis methodology

---

# Summary

All major platform components were successfully deployed and validated.

Observed issues were investigated using Kubernetes diagnostics, Prometheus validation, and Helm troubleshooting techniques.

The final platform achieved the intended goals of application deployment, observability implementation, and Infrastructure as Code management.
