# AI Infrastructure Blueprints — Project Summary

## Problem
AI workloads break traditional DC assumptions — high-density power, advanced cooling, GPU scheduling, east-west fabric, observability that understands accelerators. Architects need opinionated reference material, not vendor brochures.

## Solution
A repository of planning blueprints:
- **AI-Ready Data Center** — power, cooling, fabric, orchestration, storage, observability, governance
- **GPU Cluster Sizing** — methodology + worked example (70B model, H100 cluster)
- **Liquid Cooling Planning** — DLC vs immersion, hydraulics, leak detection, retrofit
- **AI Network Fabric** — RoCEv2 vs InfiniBand, rail-optimised topology, oversubscription
- **Operational checklists** — AI-DC readiness + GPU cluster Day-2 ops
- **K8s GPU examples** — namespace/quota, priority classes, training Job, MIG inference Deployment

## Impact
- Reusable starting point for AI infrastructure proposals and design reviews
- Codifies hard-won lessons from real planning work
- Useful as both reference material and presales artefact

## Stack
Markdown · Mermaid · Kubernetes (manifests) · NVIDIA GPU Operator / DCGM concepts

## Links
- Code: [github.com/mohammedabood/ai-infrastructure-blueprints](https://github.com/mohammedabood/ai-infrastructure-blueprints)
