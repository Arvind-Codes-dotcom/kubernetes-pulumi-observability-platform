# Kubernetes Guestbook Observability Platform

## Project Overview

This project demonstrates the deployment of a Kubernetes-based Guestbook application using Pulumi Infrastructure as Code (IaC) and implements observability through Prometheus and Grafana.

The implementation showcases application deployment, service exposure, monitoring, metrics collection, dashboard creation, and operational troubleshooting within a Kubernetes environment.

---

## Project Objectives

* Deploy a multi-tier application on Kubernetes
* Manage infrastructure using Pulumi (TypeScript)
* Implement Prometheus-based monitoring
* Visualize operational metrics through Grafana
* Validate workload health and observability
* Demonstrate Infrastructure as Code and SRE practices

---

## Technology Stack

### Infrastructure as Code

* Pulumi
* TypeScript

### Container Platform

* Kubernetes (Docker Desktop)

### Application Components

* Guestbook Frontend
* Redis Leader
* Redis Replica

### Observability

* Prometheus
* Grafana
* Alertmanager
* kube-state-metrics

### Supporting Tools

* Helm
* kubectl
* Node.js

---

## Architecture

```text
                    +----------------+
                    |    Grafana     |
                    +--------+-------+
                             |
                             |
                    +--------v-------+
                    |   Prometheus   |
                    +--------+-------+
                             |
                             |
+--------------------------------------------------+
|                 Kubernetes Cluster               |
|                                                  |
|   +-----------+                                 |
|   | Frontend  | (3 Replicas)                    |
|   +-----+-----+                                 |
|         |                                       |
|         v                                       |
|   +-----------+                                |
|   | Redis     |                                |
|   | Leader    |                                |
|   +-----+-----+                                |
|         |                                      |
|         v                                      |
|   +-----------+                                |
|   | Redis     |                                |
|   | Replica   |                                |
|   +-----------+                                |
|                                                  |
+--------------------------------------------------+

Provisioned using Pulumi (TypeScript)
```

---

## Key Features

### Application Deployment

* Kubernetes Guestbook application
* Multi-tier architecture
* Frontend and Redis services
* Kubernetes service discovery

### Infrastructure as Code

* Pulumi-based resource provisioning
* TypeScript infrastructure definitions
* Repeatable deployments
* Version-controlled infrastructure

### Monitoring and Observability

* Prometheus metrics collection
* Grafana dashboards
* Kubernetes workload visibility
* Operational health monitoring

### Troubleshooting and Operations

* Root cause analysis
* Kubernetes diagnostics
* Helm troubleshooting
* Monitoring validation

---

## Deployment Validation

### Application

* Frontend Replicas: 3
* Redis Leader: 1
* Redis Replica: 1

### Monitoring

* Prometheus Running
* Grafana Running
* Alertmanager Running
* kube-state-metrics Running

### Dashboard Metrics

* Guestbook Pod Count
* Running Guestbook Pods
* Pod Status Visibility

---

## Screenshots

### Application

![Guestbook Application](screenshots/application/01-guestbook-application-working.png)

### Prometheus Targets

![Prometheus Targets](screenshots/monitoring/01-prometheus-targets-healthy.png)

### Grafana Dashboard

![Grafana Dashboard](screenshots/monitoring/04-grafana-dashboard-overview.png)

---

## Deployment Instructions

Detailed deployment instructions are available in:

* docs/deployment-guide.md

---

## Monitoring Documentation

Monitoring implementation details are available in:

* docs/monitoring-setup.md

---

## Troubleshooting Guide

Operational troubleshooting documentation:

* docs/troubleshooting.md

---

## Lessons Learned

Project retrospective:

* docs/lessons-learned.md

---

## Repository Structure

```text
.
├── docs/
│   ├── 01-architecture.md
│   ├── 02-deployment-steps.md
│   ├── 03-monitoring-setup.md
│   ├── 04-troubleshooting.md
│   └── 05-lessons-learned.md
│
├── screenshots/
│   ├── application/
│   ├── kubernetes/
│   └── monitoring/
│
├── dashboards/
├── monitoring/
│
├── index.ts
├── package.json
├── Pulumi.yaml
├── Pulumi.dev.yaml
└── README.md
```

---

## Future Enhancements

* ServiceMonitor integration
* Redis Exporter deployment
* Application-level metrics
* Alertmanager notifications
* SLI/SLO implementation
* AKS deployment
* Persistent storage
* Centralized logging

---

## Skills Demonstrated

* Kubernetes Administration
* Pulumi Infrastructure as Code
* Prometheus Monitoring
* Grafana Dashboards
* Helm Deployments
* Kubernetes Troubleshooting
* Platform Observability
* Site Reliability Engineering Concepts

---

## By:

Arvind Narasimha Moorthy

Cloud Engineer | DevOps Engineer | Platform Engineering & SRE Focus
