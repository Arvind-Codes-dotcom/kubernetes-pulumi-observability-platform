# Lessons Learned

## Project Overview

This project involved deploying a Kubernetes-based Guestbook application using Pulumi Infrastructure as Code and implementing observability through Prometheus and Grafana.

The implementation provided practical experience across Kubernetes operations, Infrastructure as Code, monitoring, troubleshooting, and platform observability.

---

## Key Technical Learnings

### Infrastructure as Code Beyond Terraform

Prior to this implementation, Infrastructure as Code experience was primarily focused on Terraform.

This project introduced Pulumi as an alternative Infrastructure as Code platform.

Key observations:

* Infrastructure can be defined using TypeScript.
* Existing software development practices can be applied to infrastructure management.
* Infrastructure definitions can leverage programming constructs such as variables, loops, and reusable components.
* Kubernetes resources can be managed declaratively through code.

---

### Kubernetes Resource Relationships

The project reinforced how Kubernetes components interact.

Important relationships observed:

Deployment
│
▼
ReplicaSet
│
▼
Pods

Service
│
▼
Pod Endpoints

Key takeaway:

Applications are not accessed directly through pods. Services provide stable networking and service discovery for workloads.

---

### Stateful vs Stateless Workloads

The Guestbook application demonstrates both application and data tiers.

Components:

* Frontend Application
* Redis Leader
* Redis Replica

Observations:

* Frontend workloads can scale horizontally.
* Redis introduces state management considerations.
* Multi-tier architectures require service-to-service communication.

---

### Observability as a Platform Capability

Monitoring should be treated as a platform capability rather than an afterthought.

The project demonstrated:

* Centralized metrics collection
* Dashboard-based visibility
* Operational health monitoring
* Kubernetes workload visibility

Key takeaway:

Applications are only operationally useful when teams can observe and troubleshoot them effectively.

---

### Prometheus Fundamentals

Practical experience was gained in:

* Target discovery
* Metrics collection
* PromQL queries
* Metrics validation

Example validation queries:

```promql
kube_pod_info
```

```promql
kube_pod_status_phase
```

Key takeaway:

Successful monitoring begins with validating data collection before building dashboards.

---

### Grafana Dashboard Design

Grafana was used to create operational dashboards.

Important lesson:

Effective dashboards should answer operational questions quickly.

Examples:

* How many workloads exist?
* Are workloads healthy?
* Are workloads running?
* What requires investigation?

Key takeaway:

Dashboards should prioritize operational visibility over visual complexity.

---

### Troubleshooting Methodology

Several deployment and operational issues were encountered.

Examples:

* Kubernetes connectivity issues
* Helm deployment timeouts
* Node Exporter startup failures
* Local LoadBalancer limitations

Troubleshooting approach:

1. Identify symptoms
2. Collect evidence
3. Validate assumptions
4. Determine root cause
5. Implement resolution
6. Validate outcome

Key takeaway:

Structured troubleshooting is often more valuable than tool-specific knowledge.

---

## SRE and Platform Engineering Concepts Reinforced

This implementation reinforced several Site Reliability Engineering concepts.

### Observability

Visibility into system health through metrics and dashboards.

### Reliability

Verification that application workloads remain healthy and operational.

### Automation

Infrastructure and monitoring deployment performed through code.

### Repeatability

Environment can be recreated consistently using Pulumi.

### Operational Readiness

Monitoring and dashboards provide operational visibility for deployed workloads.

---

## Production Considerations

If deployed in a production environment, the following enhancements would be recommended:

* Managed Kubernetes platform (AKS, EKS, GKE)
* External load balancing
* TLS termination
* Persistent storage
* ServiceMonitor resources
* Application-level metrics
* Alertmanager integrations
* SLI/SLO definitions
* Centralized logging
* Long-term metrics retention

---

## Career Development Value

This project provided practical exposure to:

* Kubernetes Operations
* Pulumi Infrastructure as Code
* Prometheus Monitoring
* Grafana Dashboards
* Helm Deployments
* Kubernetes Troubleshooting
* Platform Observability

These skills align closely with responsibilities commonly found in:

* Site Reliability Engineering (SRE)
* Platform Engineering
* Cloud Engineering
* DevOps Engineering

---

## Conclusion

This implementation demonstrated a complete workflow covering application deployment, infrastructure automation, observability, and troubleshooting.

The project reinforced the importance of combining infrastructure provisioning, monitoring, and operational visibility into a single platform-focused solution rather than treating them as isolated activities.
