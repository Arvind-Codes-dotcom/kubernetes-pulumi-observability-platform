                    User / Browser
                           │
                           ▼
          Frontend Service (LoadBalancer)
                           │
                           ▼
        ┌─────────────────────────────┐
        │     Frontend Pods (3)       │
        │                             │
        │  frontend-1                 │
        │  frontend-2                 │
        │  frontend-3                 │
        └─────────────────────────────┘
                     │
                     ▼
                Redis Leader
                     │
                     ▼
                Redis Replica


        ┌─────────────────────────────┐
        │      Monitoring Stack       │
        └─────────────────────────────┘
                     ▲
                     │
              Prometheus
                     │
                     ▼
                Grafana

                     ▲
                     │
              Kubernetes Cluster