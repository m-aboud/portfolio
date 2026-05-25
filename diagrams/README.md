# Diagrams

Mermaid sources for diagrams used across the portfolio. Each block can be copy-pasted into Markdown that supports Mermaid (GitHub, Notion, Obsidian, etc.).

## Hybrid cloud target state

```mermaid
flowchart TB
    subgraph Identity["Identity & access"]
        IDP[Enterprise IdP]
    end
    subgraph OnPrem["On-premise"]
        VMW[VMware vSphere]
        K8S_ONP[K8s on-prem]
    end
    subgraph Cloud["Public cloud"]
        AWS[AWS Landing Zone]
        AZR[Azure Landing Zone]
    end
    subgraph Platform["Shared platform"]
        IAC[Terraform + GitOps]
        OBS[Prometheus + Grafana + Loki]
    end
    IDP --> AWS
    IDP --> AZR
    IDP --> VMW
    Platform --> OnPrem
    Platform --> Cloud
```

## AI platform layered view

```mermaid
flowchart TB
    A[Self-service portal] --> B[Scheduler / queue]
    B --> C[Kubernetes GPU cluster]
    C --> D[NVIDIA GPU Operator]
    C --> E[Parallel FS + Object store]
    C --> F[AI fabric - RoCEv2 / IB]
    D --> G[DCGM exporter]
    G --> H[Prometheus + Grafana]
```

## SLO-driven alerting flow

```mermaid
flowchart LR
    SLI[SLI signal] --> P[Prometheus]
    P --> BR{Burn rate}
    BR -->|"Fast: 2% in 1h"| PAGE[Page on-call]
    BR -->|"Slow: 10% in 6h"| TKT[Open ticket]
    BR -->|Normal| OK[No action]
    PAGE --> RB[Runbook]
    TKT --> RB
```

## DC capacity decision flow

```mermaid
flowchart TB
    START[New workload request] --> POWER{Generator margin OK?}
    POWER -->|No| ESC1[Escalate: capacity plan]
    POWER -->|Yes| COOL{Cooling capacity OK?}
    COOL -->|No| ESC2[Escalate: cooling plan]
    COOL -->|Yes| RACK{Rack density OK?}
    RACK -->|No| ESC3[Different rack / split]
    RACK -->|Yes| OK[Approve]
```
