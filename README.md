# S4T Framework — Secure Framework for Technology

> A continuous, execution-driven cybersecurity model integrating governance, risk intelligence, and operational security into a unified adaptive system.

**Author:** Diego Neuber, CISO — [sec4.tech](https://sec4.tech) · [LinkedIn](https://www.linkedin.com/in/diegoneuber/)
**Current Version:** 3.2 (2025)
**License:** Creative Commons Attribution 4.0 International (CC BY 4.0)

[![DOI v2.0](https://img.shields.io/badge/DOI%20v2.0-10.5281%2Fzenodo.20054242-blue.svg)](https://doi.org/10.5281/zenodo.20054242)
[![DOI v3.0](https://img.shields.io/badge/DOI%20v3.0-10.13140%2FRG.2.2.16699.58408-blue.svg)](https://doi.org/10.13140/RG.2.2.16699.58408)
[![Assessment Tool](https://img.shields.io/badge/Assessment%20Tool-sec4.tech-green.svg)](https://sec4.tech/assessment)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

---

## What is S4T?

S4T (Secure Framework for Technology) was developed to address a fundamental gap in cybersecurity practice: most organizations invest in frameworks and certifications, yet remain vulnerable — because existing standards model risk as a **static snapshot** rather than a **dynamic, evolving system**.

S4T replaces periodic compliance cycles with a **continuous, self-regulating operational model**, mathematically formalizing how risk evolves over time and how interventions affect future security posture.

It has been independently discovered, evaluated, and deployed by organizations across 6 countries — including U.S.-based cybersecurity firms — without any involvement from the author.

---

## Quick Start

**1. Measure your current maturity** — take the free [S4T Assessment Tool](https://sec4.tech/assessment) (5 minutes, no registration)

**2. Read the documentation** — start with the [Getting Started guide](docs/for-practitioners/getting-started.md)

**3. Choose your path:**
- [For Executives and CISOs](docs/for-executives/overview.md) — strategic overview and business case
- [For Security Practitioners](docs/for-practitioners/getting-started.md) — hands-on implementation
- [For MSPs and Consultancies](docs/for-msps/service-delivery.md) — service delivery model

---

## The Problem S4T Solves

Traditional frameworks share three structural limitations:

| Limitation | Example |
|---|---|
| Static implementation | ISO 27001 certifies a point in time, not continuous posture |
| Governance-operations disconnect | COBIT aligns strategy but does not drive daily execution |
| Reactive threat response | CIS Controls are checklists with no predictive model |

S4T introduces a **dynamic risk model** governed by differential equations, enabling predictive modeling, continuous optimization, and real-time benchmarking.

---

## Core Architecture

The S4T Framework is formally defined as a 6-tuple:

    S4T = (G, RI, CF, OS, VA, L)

| Layer | Description | Guide |
|---|---|---|
| **G** — Governance | Strategy, risk appetite, policy framework, executive reporting | [layer-G.md](docs/for-practitioners/layer-G.md) |
| **RI** — Risk Intelligence | Threat monitoring, vulnerability contextualization, business impact | [layer-RI.md](docs/for-practitioners/layer-RI.md) |
| **CF** — Control Framework | Risk-prioritized control catalog with implementation specs | [layer-CF.md](docs/for-practitioners/layer-CF.md) |
| **OS** — Operational Security | SOC, EDR, SIEM, patch management, incident response | [layer-OS.md](docs/for-practitioners/layer-OS.md) |
| **VA** — Validation & Assurance | Continuous testing via BAS, automated red teaming | [layer-VA.md](docs/for-practitioners/layer-VA.md) |
| **L** — Adaptive Learning | Feedback aggregation, model recalibration, control optimization | [layer-L.md](docs/for-practitioners/layer-L.md) |

---

## Dynamic Risk Model

S4T formalizes cyber risk as a time-dependent trajectory:

    dR/dt = -αC(t) - βO(t) - γVa(t) + δT(t)

Where:

- C(t) = Control Coverage and Quality Index
- O(t) = Operational Maturity and Response Velocity
- Va(t) = Validation Effectiveness Score
- T(t) = Threat Exposure and Growth Rate

This enables predictive modeling, continuous optimization, and steady-state analysis.

---

## Security Score

    S(t) = C(t)^α · O(t)^β · Va(t)^γ / R(t)^δ

Default coefficients (cross-sector baseline): α = 0.35, β = 0.25, γ = 0.30, δ = 0.10

| Score | Maturity Level |
|---|---|
| < 0.40 | Initial / Firefighting |
| 0.40 – 0.65 | Developing |
| 0.65 – 0.80 | Mature |
| ≥ 0.80 | Optimized |

→ [How to calculate the Security Score](docs/for-practitioners/score-calculation.md)
→ [What the score means for your organisation](docs/for-executives/security-score.md)

---

## Empirical Validation

Results across five organizational environments (18-month longitudinal study, published in academic peer review):

| Metric | Pre-S4T | Post-S4T | Cohen's d | p-value |
|---|---|---|---|---|
| Control Coverage | 45% ± 8% | 82% ± 5% | 4.8 | < 0.001 |
| Mean Time to Respond | 72h ± 15 | 18h ± 4 | 3.9 | 0.002 |
| Critical Vulnerabilities | 100 ± 20 | 33 ± 7 | 4.2 | < 0.001 |
| Monthly Incidents | 24 ± 5 | 11 ± 3 | 2.8 | 0.010 |
| Security Score | 0.38 ± 0.05 | 0.79 ± 0.04 | 7.1 | < 0.001 |

---

## Technology-Agnostic Reference Implementation

S4T is deliberately technology-agnostic. Reference open-source implementations per layer:

| Layer | Tools |
|---|---|
| Risk Intelligence | MISP, OpenCTI |
| Operational Security | Wazuh (EDR/SIEM), Zabbix, pfSense / OPNsense |
| Validation & Assurance | MITRE Caldera, Atomic Red Team, OpenBAS |
| Orchestration | Shuffle SOAR, TheHive + Cortex |
| Infrastructure | Proxmox VE |
| Intelligence / ML | Python + Scikit-learn |

Near-zero licensing cost. Full flexibility. No vendor lock-in.

---

## Deployment in Production

The S4T Framework is deployed in production environments across 6 countries:

| Country | Organizations |
|---|---|
| Brazil | Mao Colorida Comunicacao Visual, Sideout Projects, DDiv Ambientes, Transbonfim Logistica, SendLog Logistica, ConnectLog MKT, Axis Cargo, ASXDL Logistica, Provincia Servicos Contabeis |
| Chile and Peru | Optima TI |
| Argentina | Fixy Logistica |
| United States | GSC Technologies LLC, Ultra IT LLC, Stern Security |
| Germany | F H Dresden |

Several additional organizations operate S4T in production under NDA. Formal references available upon request to [feedback@sec4.tech](mailto:feedback@sec4.tech).

---

## Documentation

Complete implementation documentation is available in the [`/docs`](docs/) directory:

| Audience | Documents |
|---|---|
| **Executives and CISOs** | [Overview](docs/for-executives/overview.md) · [Security Score guide](docs/for-executives/security-score.md) · [Roadmap template](docs/for-executives/roadmap-template.md) |
| **Security Practitioners** | [Getting Started](docs/for-practitioners/getting-started.md) · Layer guides (G, RI, CF, OS, VA, L) · [Score calculation](docs/for-practitioners/score-calculation.md) |
| **MSPs and Consultancies** | [Service delivery](docs/for-msps/service-delivery.md) · [Client assessment](docs/for-msps/client-assessment.md) · [Reporting template](docs/for-msps/reporting-template.md) |
| **Reference** | [Changelog](docs/reference/changelog.md) · [Academic papers](docs/reference/papers.md) |

---

## Version History

| Version | Year | Key Changes | DOI |
|---|---|---|---|
| Concept | 2019 | Initial experiments, hardening scripts, lab environment | — |
| v1.0 | 2020 | Four pillars formalized, first production deployment in Brazil | — |
| v1.5 | 2021 | Wazuh EDR/SIEM integration, automated deploy scripts | — |
| v2.0 | 2022 | Resilience-driven framework, academic paper published | [10.5281/zenodo.20054242](https://doi.org/10.5281/zenodo.20054242) |
| v2.5 | 2023 | Inventory and governance pillar, expansion to Germany and Argentina | — |
| v3.0 | 2024 | Dynamic risk model, Security Score, empirical validation | [10.13140/RG.2.2.16699.58408](https://doi.org/10.13140/RG.2.2.16699.58408) |
| v3.2 | 2025 | Assessment Tool, public documentation, 6-country deployment | — |

→ [Full changelog with details](docs/reference/changelog.md)

---

## Repository Structure

    S4T-Framework/
    ├── docs/
    │   ├── README.md                        # Documentation index
    │   ├── changelog.md                     # Full version history with DOIs
    │   ├── for-executives/
    │   │   ├── overview.md
    │   │   ├── security-score.md
    │   │   └── roadmap-template.md
    │   ├── for-practitioners/
    │   │   ├── getting-started.md
    │   │   ├── layer-G.md
    │   │   ├── layer-RI.md
    │   │   ├── layer-CF.md
    │   │   ├── layer-OS.md
    │   │   ├── layer-VA.md
    │   │   ├── layer-L.md
    │   │   └── score-calculation.md
    │   ├── for-msps/
    │   │   ├── service-delivery.md
    │   │   ├── client-assessment.md
    │   │   └── reporting-template.md
    │   └── reference/
    │       ├── papers.md
    │       └── changelog.md
    ├── scripts/
    │   ├── autowazuh.sh                     # Automated Wazuh deploy (EDR/SIEM)
    │   └── zabbix.sh                        # Automated Zabbix deploy (monitoring)
    ├── CHANGELOG.md
    └── README.md

---

## Academic Publications

**Published:**

- Neuber, D. (2022). *S4T Framework v2.0: A Resilience-Driven Cybersecurity Framework Integrating Governance, Risk, and Technical Controls.* Zenodo. [doi.org/10.5281/zenodo.20054242](https://doi.org/10.5281/zenodo.20054242)

- Neuber, D. (2024). *S4T Framework v3.0: A Continuous Cybersecurity Execution Model.* ResearchGate. [doi.org/10.13140/RG.2.2.16699.58408](https://doi.org/10.13140/RG.2.2.16699.58408)

- Neuber, D. (2025). Beyond Firewalls: The CISO's Path to Enterprise-Wide Cyber Resilience. *Cyber Defense Magazine.*

- Neuber, D. (2025). Cybersecurity Trends for Small and Medium Businesses in 2025. *Cyber Defense Magazine.*

- DeepBotHunter: Intelligent Botnet Detection Using Deep Learning. Accepted at ICECER 2025 (IEEE-affiliated).

- Zero Trust Architecture in Modern Enterprises. Accepted at ACDSA 2026 (IEEE proceedings).

- A Secure Virtualization-Based Backup and Disaster Recovery Architecture for SME Environments. Accepted at ICECET 2026, Rome, Italy — IEEE Conference Proceedings, July 2026.

**Under peer review:**

- Neuber, D. (2026). *S4T: A Dynamic, Feedback-Driven Cybersecurity Execution Framework with Continuous Risk Modelling and Empirical Validation.* Submitted to *Computers & Security* (Elsevier, Impact Factor 5.6, Scopus/WoS indexed). Manuscript No. COSE-D-26-02084. April 2026.

→ [Full academic reference list with abstracts](docs/reference/papers.md)

---

## Cite S4T

```
Neuber, D. (2024). S4T Framework: A Continuous Cybersecurity Execution Model (v3.0).
ResearchGate. https://doi.org/10.13140/RG.2.2.16699.58408
```

---

## Contact and Contributions

- **Feedback and questions:** [feedback@sec4.tech](mailto:feedback@sec4.tech)
- **Issues and contributions:** [GitHub Issues](https://github.com/diegoneuber/S4T-Framework/issues)
- **Assessment Tool:** [sec4.tech/assessment](https://sec4.tech/assessment)
- **Author:** Diego Neuber · [LinkedIn](https://www.linkedin.com/in/diegoneuber/) · ORCID: [0009-0001-6474-5218](https://orcid.org/0009-0001-6474-5218)

---

> "Cybersecurity can no longer be treated solely as a technical function or a compliance requirement.
> Organizational survival in the digital era depends on resilience."
> — Diego Neuber, S4T Framework v3.0 (2024)
