# Presales PoC — AI-Ready Data Center for Enterprise Modernisation

**Audience:** Enterprise / public-sector customer evaluating AI infrastructure investment.
**Purpose:** Convert a strategic interest in AI into a concrete, defensible infrastructure plan.

---

## 1. Discovery questions (first meeting)

Before any architecture is drawn, get explicit answers to:

**Strategic**
- What business outcomes are you targeting with AI? (productivity, customer experience, regulatory, revenue product?)
- What's the 12-month vs 36-month ambition?
- Is this an internal capability or a service you'll offer outward?

**Workload**
- Training, fine-tuning, or inference-dominant?
- Which models / model sizes are in scope?
- Is open-weight acceptable, or are commercial APIs the bound?

**Data**
- Where does the training/RAG data live today? On-prem, cloud, both?
- Any data residency, sovereignty, or sectoral regulations?
- What's the volume? Tens of TB? Hundreds? PB?

**Existing infrastructure**
- Current DC tier and capacity headroom?
- Existing power density per rack?
- Existing cooling type and capacity?
- Cloud presence and spend?

**Organisation**
- Is there an internal AI / ML team?
- Platform engineering maturity?
- Procurement constraints (preferred vendor, government framework)?

**Constraints**
- Budget envelope (CapEx vs OpEx mix)?
- Timeline (production target)?
- Risk appetite (greenfield vs incremental)?

## 2. PoC scope proposal

A 6–10 week PoC scope to **prove the path** before committing to procurement.

### Phase 1 — Architecture & sizing (weeks 1–3)
- Refined workload sizing using [GPU cluster sizing](https://github.com/m-aboud/ai-infrastructure-blueprints/blob/main/blueprints/gpu-cluster-sizing.md) methodology
- Power / cooling fit assessment against existing DC (or new build option)
- Network fabric option paper (RoCEv2 vs IB)
- Storage tier strategy
- Capex vs cloud-burst hybrid TCO model
- **Deliverable:** Architecture document + sizing model + signed-off bill of materials option set

### Phase 2 — Hands-on validation (weeks 4–7)
- Small representative GPU node (rented or borrowed) + reference Kubernetes
- Run customer-representative workload (could be open Llama, internal data on stub model)
- DCGM observability stack live
- Measured throughput, latency, GPU utilisation, end-to-end fine-tune time
- **Deliverable:** Test report with measured numbers vs design targets

### Phase 3 — Operating model & readiness (weeks 8–10)
- Operating model recommendation (in-house, managed, hybrid)
- Skills gap & training plan
- Runbook scaffold (using [AI-DC readiness checklist](https://github.com/m-aboud/ai-infrastructure-blueprints/blob/main/checklists/ai-dc-readiness.md))
- Procurement roadmap with optionality
- **Deliverable:** Final presentation to executive sponsor with go/no-go recommendation

## 3. Success criteria

The customer should be able to answer **yes** to all of:

- "We know what we'd buy, why, and what it would cost."
- "We've seen our workload run on representative kit."
- "We know how we'd operate it and what skills we need."
- "We can defend this plan to procurement, audit, and the board."

## 4. Defensible deliverables

Every PoC artefact is reusable by the customer regardless of the outcome:

- Architecture document — vendor-neutral
- Sizing model — reproducible, parameterised
- Test report — measured, dated, with config captured
- Operating model — applies even if hardware decision changes
- Procurement roadmap — optionality preserved

## 5. Common objections & responses

| Objection | Response |
|---|---|
| "We'll just use the cloud" | TCO model includes cloud option; for sustained training workload, on-prem typically wins past month 12–18 |
| "The hardware will be obsolete in 2 years" | True; that's why phase 1 includes refresh strategy + procurement optionality |
| "We don't have the skills" | Operating model addresses this; managed-service option modeled |
| "Our DC can't handle this density" | Phase 1 explicitly models cooling and power fit; retrofit options included |
| "We're not sure AI will deliver ROI" | PoC is the cheapest way to find out before committing capex |

## 6. Closing positioning

This PoC is structured so that **the customer wins regardless of what they buy from us**. That posture builds trust faster than a vendor-driven design.

---

*Aligned to artefacts in [ai-infrastructure-blueprints](https://github.com/m-aboud/ai-infrastructure-blueprints) and [datacenter-ops-toolkit](https://github.com/m-aboud/datacenter-ops-toolkit).*
