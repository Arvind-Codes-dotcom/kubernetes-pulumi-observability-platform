# Deployment Steps

## Overview

This document provides deployment steps for the Kubernetes Guestbook Observability Platform.

The platform consists of:

* Guestbook Frontend Application
* Redis Leader
* Redis Replica
* Prometheus Monitoring Stack
* Grafana Visualization Layer
* Pulumi Infrastructure as Code

---

## Prerequisites

### Required Software

Made sure the following tools are present and installed:

* Docker Desktop
* Kubernetes (enabled in Docker Desktop)
* kubectl
* Pulumi CLI
* Helm
* Node.js
* npm

---

## Verify Environment

Verifying Kubernetes:

```bash
kubectl get nodes
```

Expected:

```text
docker-desktop   Ready
```

 Verifying Pulumi:

```bash
pulumi version
```

 Verifying Helm

```bash
helm version
```

Verify Node.js:

```bash
node --version
npm --version
```

---

## Project Setup

Clone repository:

```bash
git clone <repository-url>
cd kubernetes-guestbook-observability
```

Install dependencies:

```bash
npm install
```

---

## Pulumi Configuration

Initialize local Pulumi backend:

```bash
pulumi login --local
```

Create stack:

```bash
pulumi stack init dev
```

Configure deployment:

```bash
pulumi config set isMinikube false
```

Verify configuration:

```bash
pulumi config
```

---

## Deployment Validation

Preview deployment:

```bash
pulumi preview
```

Review planned resources before deployment.

---

## Deploy Guestbook Application

Deploy infrastructure:

```bash
pulumi up
```

Approve deployment when prompted.

Resources deployed:

* Frontend Deployment
* Frontend Service
* Redis Leader Deployment
* Redis Leader Service
* Redis Replica Deployment
* Redis Replica Service

---

## Verify Application Deployment

Check deployments:

```bash
kubectl get deployments
```

Check pods:

```bash
kubectl get pods
```

Check services:

```bash
kubectl get svc
```

Expected workload:

* Frontend Pods: 3
* Redis Leader Pods: 1
* Redis Replica Pods: 1

---

## Access Guestbook Application

Port forward service:

```bash
kubectl port-forward svc/frontend 8080:80
```

Access application:

```text
http://localhost:8080
```

Verify application functionality.

---

## Deploy Monitoring Stack

Monitoring components are deployed through the kube-prometheus-stack Helm chart managed by Pulumi.

Components:

* Prometheus
* Grafana
* Alertmanager
* kube-state-metrics
* Prometheus Operator

Deploy:

```bash
pulumi up
```

---

## Verify Monitoring Components

Check monitoring namespace:

```bash
kubectl get pods -n monitoring
```

Verify:

* Prometheus Running
* Grafana Running
* Alertmanager Running
* kube-state-metrics Running

---

## Access Grafana

Port forward Grafana service:

```bash
kubectl port-forward -n monitoring svc/kube-prometheus-stack-4b698e00-grafana 3000:80
```

Access:

```text
http://localhost:3000
```

Credentials:

```text
Username: admin
Password: admin123!
```

---

## Access Prometheus

Port forward Prometheus:

```bash
kubectl port-forward -n monitoring svc/kube-prometheus-stack-4b69-prometheus 9090:9090
```

Access:

```text
http://localhost:9090
```

---

## Validation Checklist

Verify:

* Kubernetes cluster healthy
* Guestbook application accessible
* Frontend pods running
* Redis services healthy
* Prometheus targets UP
* Grafana dashboards accessible
* Metrics visible in Prometheus
* Dashboard visualizations functional

---

## Cleanup

Destroy infrastructure:

```bash
pulumi destroy
```

Remove stack:

```bash
pulumi stack rm dev
```

Cleanup local Kubernetes resources:

```bash
kubectl delete namespace monitoring
```

---

## Notes:

Docker Desktop Kubernetes was used for local deployment and validation.

Grafana and Prometheus access were performed through port-forwarding due to local Kubernetes LoadBalancer limitations.

This deployment pattern can be adapted to managed Kubernetes services such as:

* Azure Kubernetes Service (AKS)
* Amazon EKS
* Google Kubernetes Engine (GKE)
