# Observability Platform — Project Summary

## Problem
Most infrastructure teams either over-monitor (alert fatigue) or under-monitor (silent failures). The middle ground — SLO-discipline + runbook-anchored alerts + one pane of glass — is rare.

## Solution
A self-contained docker-compose stack:
- **Prometheus** (rules + 30d retention)
- **Grafana** (provisioned datasources + starter dashboard)
- **Loki + Promtail** for centralised logs
- **Alertmanager** with severity routing and inhibit rules
- **Node Exporter** + **cAdvisor** for host + container metrics
- **9 alert rules** spanning host, disk, network, container restarts
- **3 runbooks** linked from alert annotations

CI validates `promtool`, `amtool`, and compose syntax on every PR.

## Impact
- Drop-in baseline that gets a new environment to observable in minutes
- Demonstrates SLO-style alerting practice (burn rates, runbooks, inhibition)
- Reusable starting point for client environments

## Stack
Docker Compose · Prometheus · Grafana · Loki · Promtail · Alertmanager · Node Exporter · cAdvisor · GitHub Actions

## Links
- Code: [github.com/m-aboud/observability-platform](https://github.com/m-aboud/observability-platform)
