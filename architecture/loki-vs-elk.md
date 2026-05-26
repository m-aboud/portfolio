# Loki vs ELK — choosing a log stack for infrastructure & CI/CD platforms

**Author:** Mohammed Abood
**Status:** Reference / decision aid
**Date:** 2026-05-01

> A common interview question — especially in MENA banking and government, where ELK is heavily entrenched — is *"why didn't you use ELK?"*. This document is the honest answer.

## TL;DR

| If… | Use |
|---|---|
| Logs are mainly for **operational triage**, you live alongside Prometheus + Grafana, and you optimise for **cost & operational simplicity** | **Loki** |
| You need **full-text search at scale**, complex log analytics, business intelligence on log data, or your security team mandates a SIEM substrate | **Elastic Stack (ELK / Elastic Cloud)** |
| You operate **both** application logs and security analytics, and the team is fluent in JVM ops | **Both**, with clear segregation (Loki for ops, Elastic for SIEM) |

The choice is not "which is better" — it's "which problem are you solving".

## The fundamental design difference

| Dimension | Loki | Elasticsearch |
|---|---|---|
| **Indexes** | Labels only (low cardinality) | Every field by default (inverted index everywhere) |
| **Query language** | LogQL — Prometheus-like, label-first | Lucene / Elastic Query DSL — full-text first |
| **Storage cost** | ~10× cheaper at equivalent volume | High (indexes inflate storage 3-7×) |
| **Memory footprint** | Modest (Go, no JVM) | High (JVM heap, off-heap caches) |
| **Search speed (full-text)** | Slow (scan the chunk) | Fast (inverted index) |
| **Search speed (label-scoped)** | Fast | Fast |
| **Cardinality discipline** | Required — explodes the index if you put high-card values in labels | Permissive — Elastic absorbs it (at cost) |
| **Operational complexity** | Low | High (cluster sizing, JVM tuning, mapping management, snapshot lifecycle) |

## When Loki is the right answer

✅ **Most infrastructure / platform / DevOps use cases.** Logs are for **diagnosis**, not for being a primary data store. You search by *which service* and *what time*, then read raw lines. Loki was designed for exactly this.

✅ **Cost-sensitive deployments.** Loki's chunk-and-label storage routinely costs 1/5 to 1/10 of an equivalent Elastic cluster. Per-GB cloud storage costs alone are dramatic.

✅ **You're already a Grafana shop.** Native datasource, shared label conventions with Prometheus, same UI for metrics + logs + traces. The cognitive load is near-zero for an engineer who already uses Grafana.

✅ **Modest team.** Loki has roughly 1/10 the operational surface area of Elastic at HA scale. No JVM tuning, no shard/replica strategy, no index lifecycle dance.

## When ELK is the right answer

✅ **You need a SIEM substrate.** Elastic + Beats + Logstash + Elastic Security is a credible SIEM in itself, and that's where the platform genuinely shines. Loki was never designed for this.

✅ **Full-text search is the product.** Searching free-form messages — application audit trails, customer service interactions, free-text fields in app logs — favours Elastic.

✅ **Compliance frameworks demand named tooling.** Several MENA central bank IT supervisory frameworks explicitly reference Elastic; some sector audits use Elastic-specific evidence templates. Sometimes "we use ELK" is a checklist item, not a technical choice.

✅ **Business analytics on log data.** Aggregations, percentiles, terms aggregations across hundreds of millions of events — Elastic's purpose-built engine wins.

✅ **You already operate Elastic well.** A skilled Elastic team is a real asset; don't throw it away to chase a trend.

## Hybrid is legitimate

A growing pattern at mid-to-large enterprises:

- **Loki** for *operational logs* — platform, infra, application — owned by SRE / platform team
- **Elastic** for *security & compliance logs* — audit, authentication, network — owned by SecOps
- Each team operates the tool that matches its workflow; logs flow into both via separate shipping paths

This avoids the false dichotomy and matches the org chart.

## Cost reality check (illustrative)

For a steady-state infrastructure platform emitting ~500 GB/day of logs with 30-day retention:

| Cost component | Loki | Elastic (self-hosted HA) |
|---|---|---|
| Object storage (S3) | ~$5–10/month | not applicable |
| Block storage (3× cluster) | minimal — Loki is mostly object-store | ~$300–500/month |
| Compute (steady-state) | 2–4 vCPU, 8–16 GB RAM | 12–24 vCPU, 64–128 GB RAM |
| Engineer time to operate | ~0.1 FTE | ~0.5–1 FTE |

*Exact numbers vary wildly; these are order-of-magnitude.*

For Elastic Cloud (managed), you trade engineer time for SaaS cost — easier to predict but typically 3–5× Loki on like-for-like volume.

## Migration risk

If you start with **Loki** and later need Elastic-style analytics:

- Lossy: high-cardinality fields that should have been indexed will need re-extraction
- Lukewarm: structured logs (JSON) replay cleanly; free-form text replays slowly
- Mitigation: log in structured JSON from day one (you should anyway)

If you start with **Elastic** and want to move to Loki:

- Cleaner migration — Loki ingests any line-based log
- Cost wins are immediate
- Hardest part is retraining searches from Lucene to LogQL

## My recommendation for the gitops-cicd-platform stack

The bundled [`observability-platform`](https://github.com/mohammedabood/observability-platform) uses **Loki + Promtail**. The rationale:

1. The target audience is **infrastructure & platform engineers** — operational triage is the dominant use case
2. The Prometheus + Grafana stack is already there; Loki shares labels, datasource, UI
3. Cost matters in a portfolio reference; pretending it doesn't would be dishonest
4. For SIEM workloads, this stack would be paired with **Elastic Security** in a separate environment; this is documented honestly rather than shoehorning logs through one tool

If your target employer runs ELK, swap Promtail for Filebeat and Loki for an Elasticsearch index — the rest of the stack (Prometheus, Grafana, Alertmanager) stays unchanged.

## What I'd want to know in an interview

If asked *"would you migrate our ELK estate to Loki?"*, the honest first answer is **questions**, not a recommendation:

1. What's the dominant query pattern — full-text or label-scoped?
2. Who owns the cluster today, and what is their workload?
3. What compliance frameworks reference Elastic by name?
4. Is the cost picture problematic, or is it absorbed?
5. Is there an existing migration plan, or is "change for change's sake" a risk?

If the answers favour Loki, the migration is a 3–6 month programme with a clear cutover. If they don't, the right architecture decision is to **keep ELK and run it better** — not to import a trend.
