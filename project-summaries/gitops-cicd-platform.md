# GitOps CI/CD Platform — Project Summary

## Problem
Most teams operate CI/CD as a collection of disconnected tools: a Jenkinsfile here, a Helm chart there, secrets pasted into pipeline variables, no signing, no provenance, no policy at the cluster edge. The result is brittle deploys, untraceable artefacts, and audit findings nobody can close.

## Solution
A complete, opinionated reference platform showing how modern teams ship to production:

- **Terraform** provisions an EKS cluster and bootstraps Argo CD, Argo Rollouts, Kyverno, and External Secrets Operator via Helm — one apply, full platform
- **GitHub Actions CI** builds a multi-stage distroless container, scans it with Trivy, generates a CycloneDX SBOM, signs the image with Cosign (keyless OIDC), and attests SLSA build provenance
- **Argo CD** uses the **app-of-apps** pattern via ApplicationSet, generating one Application per environment overlay automatically
- **Kustomize** drives dev/staging/prod variation — no template hell
- **Argo Rollouts** runs production deploys as a 5 → 25 → 50 → 100% canary with **Prometheus-backed analysis** that auto-rolls-back on success-rate regression
- **Kyverno** enforces admission policies at the cluster: required labels, no `:latest`, signed images, dropped capabilities
- **External Secrets Operator** syncs secrets from AWS Secrets Manager — zero plaintext in Git
- **Renovate** keeps every layer (Terraform, GitHub Actions, Helm, Python, container base) automatically up to date

## Impact
- Demonstrates end-to-end thinking — infrastructure, CI, CD, security, policy, observability — not a single tool
- Shows SLSA-aligned supply-chain practice that increasingly appears in enterprise security questionnaires
- Reusable architecture pattern: drop in a different cloud module, point Argo CD at a different repo, ship the same way
- Three ADRs capture the **reasoning** behind choices — the artefact that signals "architect" rather than "operator"

## Stack
Terraform 1.9+ · AWS EKS · Argo CD 2.13+ · Argo Rollouts · Kustomize · Kyverno · External Secrets Operator · Cosign (Sigstore) · Trivy · Syft · GitHub Actions · Renovate · pre-commit · FastAPI (sample app)

## Links
- Code: [github.com/m-aboud/gitops-cicd-platform](https://github.com/m-aboud/gitops-cicd-platform)
- ADRs: [docs/adr/](https://github.com/m-aboud/gitops-cicd-platform/tree/main/docs/adr)
- Runbooks: [docs/runbooks/](https://github.com/m-aboud/gitops-cicd-platform/tree/main/docs/runbooks)
