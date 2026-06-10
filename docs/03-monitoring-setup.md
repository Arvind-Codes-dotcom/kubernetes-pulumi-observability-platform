# Monitoring and Observability Setup

## Overview

This document describes the monitoring and observability implementation for the Kubernetes Guestbook Observability Platform.

The monitoring stack was deployed using the Prometheus Community kube-prometheus-stack Helm chart and managed through Pulumi IaC.

---

## Objective

The observability implementation was designed to provide:

* Application visibility
* Workload health monitoring
* Pod lifecycle visibility
* Cluster metrics collection
* Dashboard-based operational monitoring

---

## Monitoring Architecture

Monitoring Stack:

Kubernetes Cluster
│
├── Guestbook Frontend
├── Redis Leader
├── Redis Replica
│
▼
Prometheus
│
▼
Metrics Collection
│
▼
Grafana
│
▼
Dashboards and Visualization

---

## Components

### Prometheus

Prometheus serves as the central metrics collection platform.

Responsibilities:

* Metrics scraping
* Metrics storage
* Target discovery
* Query execution

Deployment Method:

* kube-prometheus-stack Helm chart
* Managed through Pulumi

---

### Grafana

Grafana provides visualization and operational dashboards.

Responsibilities:

* Dashboard creation
* Metrics visualization
* Operational monitoring
* Troubleshooting support

Access Method:

```text
http://localhost:3000
```

Credentials:

```text
Username: admin
Password: admin123!
```

---

### Alertmanager

Alertmanager was deployed as part of the monitoring stack.

Responsibilities:

* Alert aggregation
* Alert routing
* Alert suppression
* Notification management

Note:

Alerting workflows were not configured as part of this implementation.

---

### kube-state-metrics

kube-state-metrics exposes Kubernetes object state metrics.

Collected Information:

* Pod status
* Deployment status
* Replica counts
* Namespace information
* Service information

These metrics are consumed by Prometheus and visualized in Grafana.

---

## Metrics Validation

### Prometheus Target Validation

Prometheus target validation was performed through:

Status → Targets

Validation Results:

* Prometheus targets discovered successfully
* Targets reported UP status
* Metrics collection operational

---

### Prometheus Query Validation

The following validation queries were executed:

#### Pod Discovery

```promql
kube_pod_info
```

Purpose:

* Verify pod discovery
* Verify workload visibility

Observed Workloads:

* Frontend Pods
* Redis Leader
* Redis Replica

---

#### Pod Status

```promql
kube_pod_status_phase
```

Purpose:

* Validate workload health
* Verify running state

Result:

Application pods reported Running status.

---

## Grafana Dashboard

A custom dashboard was created to provide operational visibility.

Dashboard Components:

### Guestbook Pod Count

Query:

```promql
count(kube_pod_info{namespace="default"})
```

Purpose:

Displays total application workload count.

---

### Running Guestbook Pods

Query:

```promql
count(kube_pod_status_phase{namespace="default",phase="Running"} == 1)
```

Purpose:

Displays healthy running workloads.

---

### Guestbook Pod Status

Query:

```promql
kube_pod_status_phase{namespace="default",phase="Running"}
```

Purpose:

Provides visibility into individual workload status.

---

## Operational Workflow

Application Deployment
│
▼
Kubernetes Scheduling
│
▼
Metrics Collection
│
▼
Prometheus Storage
│
▼
Grafana Visualization
│
▼
Operational Monitoring

---

## Observability Outcomes

The monitoring implementation provides visibility into:

* Pod health
* Workload availability
* Kubernetes object status
* Application deployment state
* Operational platform status

---

## Challenges Encountered

### Node Exporter Deployment

Issue:

Prometheus Node Exporter experienced startup failures within Docker Desktop Kubernetes.

Observed Error:

```text
path / is mounted on / but it is not a shared or slave mount
```

Root Cause:

Docker Desktop Kubernetes host mount limitations prevented node-exporter from accessing required filesystem paths.

Impact:

* Prometheus remained operational
* Grafana remained operational
* kube-state-metrics remained operational
* Application monitoring functionality was unaffected

Resolution:

The issue was documented as a local Kubernetes platform limitation and did not impact observability objectives.

---

## Future Enhancements

Potential improvements include:

* ServiceMonitor implementation
* Redis Exporter integration
* Application-level metrics exposure
* Alertmanager notification configuration
* SLI/SLO dashboard creation
* Kubernetes alerting policies
* Long-term metrics retention

---

## Summary

The monitoring stack successfully delivered application and platform observability through Prometheus and Grafana while demonstrating Infrastructure as Code, Kubernetes monitoring, and operational visibility practices commonly used in cloud-native environments.
