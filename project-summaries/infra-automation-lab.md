# Infrastructure Automation Lab — Project Summary

## Problem
Most "infra demo" repos are toy snippets. Hiring panels and clients want to see real production patterns — modules, roles, namespaces, network policies, CI guardrails — not a single `main.tf` with an output.

## Solution
A lab repo demonstrating production-style automation:
- **Terraform** — reusable AWS VPC module + dev environment consuming it
- **Ansible** — proper role with defaults / tasks / handlers; SSH hardening, sysctl, UFW, fail2ban
- **Kubernetes** — namespace + deployment + service + HPA + PDB + NetworkPolicy under Kustomize
- **Docker** — multi-service compose with healthchecks
- **Scripts** — idempotent host bootstrap (Docker, kubectl, Terraform, Ansible)
- **CI** — terraform fmt/validate/tflint, ansible-lint, yamllint, kubeconform, shellcheck

## Impact
- Demonstrates depth across the IaC stack — not just one tool
- Patterns reusable directly in client engagements
- Linted automatically on every change

## Stack
Terraform 1.9+ · Ansible 2.16+ · Kubernetes 1.30+ · Docker · Bash · GitHub Actions

## Links
- Code: [github.com/m-aboud/infra-automation-lab](https://github.com/m-aboud/infra-automation-lab)
