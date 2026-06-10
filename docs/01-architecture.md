# Architecture Overview

## Summary

This project demonstrates the deployment of a containerized Guestbook application on Kubernetes using Pulumi Infrastructure as Code (IaC). The environment includes application deployment, service exposure, monitoring, metrics collection, and visualization through Prometheus and Grafana.

---

## Objective

The objective of this implementation is to simulate a production-style Kubernetes platform where:

* Applications are deployed through Infrastructure as Code.
* Services are exposed through Kubernetes networking.
* Metrics are collected centrally.
* Operational visibility is provided through dashboards.
* Platform components can be managed consistently and repeatably.

---

## Architecture Components

### Kubernetes Cluster

Docker Desktop Kubernetes was used as the local Kubernetes platform.

Responsibilities:

* Container orchestration
* Scheduling workloads
* Service discovery
* Resource management

---

### Guestbook Frontend

Frontend application exposed through a Kubernetes LoadBalancer service.

Deployment Characteristics:

* 3 frontend replicas
* High availability through replica distribution
* Service abstraction for traffic routing

---

### Redis Leader

Primary Redis instance responsible for handling write operations.

Deployment Characteristics:

* Single replica
* Internal ClusterIP service

---

### Redis Replica

Read replica used to simulate distributed application architecture.

Deployment Characteristics:

* Single replica
* Internal ClusterIP service

---

### Pulumi

Pulumi TypeScript is used to provision and manage Kubernetes resources.

Managed Resources:

* Deployments
* Services
* Namespace
* Monitoring Stack

Benefits:

* Version-controlled infrastructure
* Repeatable deployments
* Declarative resource management

---

### Prometheus

Prometheus is responsible for collecting cluster and application metrics.

Monitored Components:

* Kubernetes workloads
* Cluster resources
* Application pods
* Services

---

### Grafana

Grafana provides visualization and operational dashboards.

Dashboard Metrics:

* Pod Count
* Running Pods
* Pod Status
* Cluster Health

---

## High-Level Architecture

User
│
▼
Guestbook Frontend Service
│
▼
Frontend Pods (3 Replicas)
│
▼
Redis Leader
│
▼
Redis Replica

Prometheus
│
▼
Collects Kubernetes Metrics

Grafana
│
▼
Visualizes Operational Metrics

Pulumi
│
▼
Provisioning and Lifecycle Management

---

## Observability Flow

Kubernetes Components
│
▼
Prometheus Scraping
│
▼
Metrics Storage
│
▼
Grafana Dashboards
│
▼
Operational Visibility

---

## Outcome

The platform demonstrates a complete Kubernetes deployment lifecycle including application hosting, monitoring, observability, and Infrastructure as Code management using modern cloud-native tooling.
