# Research

Technical research papers by **Harsh RB** (Harsh R Bagtharia) on planet-scale systems architecture and enterprise go-to-market systems. Each paper pairs a full write-up (PDF) with a condensed companion essay published on [blog.harshrb.in](https://blog.harshrb.in).

These are independent architecture studies: they synthesise publicly available systems papers, engineering documentation and vendor material into a single operational model of how the system works end to end.

## Index

| # | Paper | Domain | Published |
|---|-------|--------|-----------|
| 01 | [How Google Actually Works: Systems Architecture for Planet-Scale Computing](#01--how-google-actually-works-systems-architecture-for-planet-scale-computing) | Distributed systems · Cloud infrastructure | 21 Aug 2026 |
| 02 | [Digital Lead Generation and Lead Quality Optimization for High-Value Commercial Real Estate](#02--digital-lead-generation-and-lead-quality-optimization-for-high-value-commercial-real-estate) | B2B demand generation · Applied ML | 30 Sep 2026 |

---

## 01 — How Google Actually Works: Systems Architecture for Planet-Scale Computing

<img src="https://blog.harshrb.in/images/how_google_works.png" alt="Cover image: a datacenter aisle of server racks with the search prompt 'How Google Actually Works?'" width="720">

> Google is not one giant supercomputer. It is a composition of distributed systems built to treat hardware, network and software failure as a normal operating condition.

**Read:** [Companion essay](https://blog.harshrb.in/posts/how-google-actually-works/) · [Full paper (PDF)](https://cdn.harshrb.in/research/google/how-google-actually-works-systems-architecture-planet-scale-computing.pdf)

### Abstract

A systems-level account of Google's infrastructure stack, traced from the problem each layer was built to solve to the abstraction it exposes to the layer above. The paper argues that Google's core engineering achievement is not raw scale but **containment**: failure, stragglers, clock skew and heterogeneous hardware are absorbed by the infrastructure and hidden behind interfaces that application developers can reason about.

### Coverage

| Layer | Systems | What the paper examines |
|-------|---------|------------------------|
| Compute | **Borg** | Cluster management, resource pooling across tens of thousands of machines, isolation, and rescheduling on failure |
| Storage | **GFS → Colossus** | Evolution from commodity-hardware-scale file storage to a distributed metadata model that removes the single-namespace throughput bottleneck |
| Structured data | **Bigtable, Spanner** | Wide-column scaling on commodity servers; globally distributed relational consistency and **TrueTime**, which models time as an interval of bounded uncertainty rather than a synchronised timestamp |
| Network | **Jupiter, B4** | Multi-stage Clos-based intra-datacenter fabric for aggregate bandwidth and path diversity; software-defined WAN with application-level traffic priorities |
| AI hardware | **TPUs** | Custom accelerators at pod scale (e.g. TPU v5p: 8,960 chips per pod on a 3D-torus interconnect), where the interconnect is part of the computation rather than plumbing around it |

### Key takeaways

- Failure is designed for, not avoided — the unit of reliability is the system, not the machine.
- Abstractions (job, file, table, cell) are the actual product; hardware heterogeneity is an implementation detail.
- Network topology is a first-class design decision, not a deployment afterthought.

---

## 02 — Digital Lead Generation and Lead Quality Optimization for High-Value Commercial Real Estate

<img src="https://blog.harshrb.in/images/High-Value%20CRE%20Lead%20Generation%20Pipeline.png" alt="Cover image: acquisition channels on the left feeding a four-stage pipeline into a qualified lead record, with a Class-A office building on the right" width="720">

> In high-value CRE, lead volume is noise and lead quality is everything: 6–18 month cycles, institutional buying committees, and a single unqualified lead can consume hundreds of hours of sales bandwidth.

**Read:** [Companion essay](https://blog.harshrb.in/posts/cre-lead-generation-architecture/) · [Full paper (PDF)](https://cdn.harshrb.in/research/Digital%20Lead%20Generation%20and%20Lead%20Quality%20Optimization%20for%20High-Value%20Commercial%20Real%20Estate.pdf)

### Abstract

An end-to-end systems architecture for B2B demand generation in commercial real estate, where transaction economics make consumer-style, high-volume funnel design actively counterproductive. The paper treats the go-to-market motion as a software-defined pipeline — acquisition, capture, enrichment, qualification, handoff and attribution — with closed-loop outcome data feeding back into the model.

### The eight-stage framework

```
Traffic Acquisition ➔ Capture UX ➔ Identity Enrichment ➔ Intent Signals
➔ Hybrid Scoring ➔ Sales Handoff ➔ Lifecycle Nurturing ➔ Closed-Loop Attribution ↩
```

| Stage | Design problem | Approach examined |
|-------|----------------|-------------------|
| Acquisition | Reaching institutional buyers with genuine intent | High-intent search (SEO/PPC), account-based paid social on executive titles, domain marketplaces (CoStar, LoopNet, CREXi) |
| Capture | Form friction kills conversion | Minimal top-of-funnel fields plus **progressive profiling** that swaps known fields for deeper qualification on return visits |
| Enrichment | An email address carries no context | Firmographic/technographic resolution (ZoomInfo, Clearbit, 6sense), third-party intent (Bombora), property-database sync |
| Qualification | Routing scarce sales time | Rule-based scoring for explicit fit/penalty signals, combined with predictive models (gradient-boosted trees) estimated on closed-won CRM history |
| Validation | Preventing a model from looking good but ranking badly | **Precision@k** and **ROC-AUC** back-testing against the MQL threshold and sales SLA |
| Attribution | 10+ touchpoints over many months break first/last-click | Position-based (U-shaped), time-decay, and data-driven credit assignment (Shapley value, Markov chains) |
| Efficiency | Measuring the whole system, not one campaign | Pipeline velocity as throughput: qualified opportunities × average deal size × win rate ÷ sales-cycle length |

### Key takeaways

- Data enrichment, not creative, is the quality bottleneck: who the lead is determines whether the lead is worth a call.
- Heuristic and learned scoring are complements — rules encode policy, models encode observed behaviour.
- Attribution is an incentive system as much as a measurement system; the model chosen reallocates budget, so it must be validated.

---

## Scope and method

Both papers are literature-and-architecture syntheses, not empirical studies or peer-reviewed publications. Claims are grounded in primary systems papers (Borg, GFS, Spanner, Jupiter, TPU pod architectures), public engineering write-ups and vendor documentation; the contribution is the organising model and the system-level framing, not new measurement.

Figures, formulae and vendor comparisons referenced above are elaborated in the PDFs.

---

## Citing

```text
Harsh RB. "How Google Actually Works: Systems Architecture for Planet-Scale
Computing." 2026. https://blog.harshrb.in/posts/how-google-actually-works/

Harsh RB. "Digital Lead Generation and Lead Quality Optimization for High-Value
Commercial Real Estate." 2026.
https://blog.harshrb.in/posts/cre-lead-generation-architecture/
```

## Repository layout

```
research/
└── README.md   # index, abstracts and links for all papers
```

Paper PDFs are hosted on the CDN (`cdn.harshrb.in/research/…`) rather than versioned here; the canonical link for each paper is listed above and is stable.

## About

**Harsh RB** — [harshrb.in](https://harshrb.in) · [blog.harshrb.in](https://blog.harshrb.in) · [GitHub @Harshrb2424](https://github.com/Harshrb2424)
