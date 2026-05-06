# S4T Framework — Documentation

**S4T (Secure Framework for Technology)** is a free, open source cybersecurity framework that models organisational security maturity as a continuous, mathematically measurable process — not a periodic compliance checklist.

> *"Security that depends on a calendar is already late."*

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Version](https://img.shields.io/badge/Version-3.2-blue.svg)](reference/changelog.md)
[![Assessment Tool](https://img.shields.io/badge/Assessment%20Tool-sec4.tech-green.svg)](https://sec4.tech/assessment)
[![DOI v2.0](https://img.shields.io/badge/DOI%20v2.0-10.5281%2Fzenodo.20054242-blue.svg)](https://doi.org/10.5281/zenodo.20054242)
[![DOI v3.0](https://img.shields.io/badge/DOI%20v3.0-10.13140%2FRG.2.2.16699.58408-blue.svg)](https://doi.org/10.13140/RG.2.2.16699.58408)

---

## What is S4T?

S4T is formally defined as a 6-tuple:

```
S4T = (G, RI, CF, OS, VA, L)
```

Six integrated layers — Governance, Risk Intelligence, Control Framework, Operational Security, Validation & Assurance, and Adaptive Learning — that together produce a single computable metric: the **Security Score S(t)**.

Unlike ISO 27001, NIST CSF, or CIS Controls, S4T treats cybersecurity risk as a **time-evolving trajectory**, not a point-in-time snapshot. The framework's core innovation is the risk evolution equation:

```
dR/dt = δT(t) − αC(t) − βO(t) − γVa(t)
```

Where risk decreases as controls, operations, and validation improve — and increases as threat exposure grows. The Security Score quantifies where your organisation stands on this trajectory at any given moment.

**Empirical validation** across five organisations over 18 months demonstrated:
- Control Coverage: 45% → 82% (Cohen's d = 4.8, p < 0.001)
- Mean Time to Respond: 72h → 18h (d = 3.9, p = 0.002)
- Security Score: 0.38 → 0.79 (+108%, d = 7.1, p < 0.001)

---

## Start Here

**Not sure where to start?** Take the free [S4T Assessment Tool](https://sec4.tech/assessment) — it measures your Security Score across all six layers in 5 minutes, with no registration required. Your results will tell you exactly which section of this documentation to read first.

---

## Documentation by Audience

### 👔 For Executives and CISOs
Strategic overview, business case, and executive reporting.

| Document | Description |
|---|---|
| [What is S4T and Why It Exists](for-executives/overview.md) | The problem S4T solves and how it differs from existing frameworks |
| [Understanding the Security Score](for-executives/security-score.md) | What the score measures, what it means, and how to use it |
| [Executive Roadmap Template](for-executives/roadmap-template.md) | Template for presenting S4T adoption to leadership |

---

### 🔧 For Security Practitioners
Hands-on implementation guidance for each framework layer.

| Document | Description |
|---|---|
| [Getting Started](for-practitioners/getting-started.md) | Prerequisites, deployment phases, and first steps |
| [Layer G — Governance](for-practitioners/layer-G.md) | Strategy, policies, risk appetite, and executive alignment |
| [Layer RI — Risk Intelligence](for-practitioners/layer-RI.md) | Threat monitoring and vulnerability management |
| [Layer CF — Control Framework](for-practitioners/layer-CF.md) | Risk-prioritised controls and asset inventory |
| [Layer OS — Operational Security](for-practitioners/layer-OS.md) | SOC, EDR, SIEM, and incident response |
| [Layer VA — Validation & Assurance](for-practitioners/layer-VA.md) | Continuous testing, BAS, and control validation |
| [Layer L — Adaptive Learning](for-practitioners/layer-L.md) | Metrics, feedback, and continuous improvement |
| [Calculating the Security Score](for-practitioners/score-calculation.md) | Manual and automated score computation |

---

### 🏢 For MSPs and Consultancies
Guidance for organisations delivering S4T as a managed service.

| Document | Description |
|---|---|
| [Service Delivery Model](for-msps/service-delivery.md) | How to structure S4T as a client-facing service |
| [Client Assessment Guide](for-msps/client-assessment.md) | Using the Assessment Tool with client organisations |
| [Reporting Template](for-msps/reporting-template.md) | Monthly and quarterly reporting structure |

---

### 📚 Reference
Technical specifications, version history, and academic papers.

| Document | Description |
|---|---|
| [Mathematical Model](reference/mathematical-model.md) | Full formal specification of equations and variables |
| [Changelog](reference/changelog.md) | Version history from v1.0 (2019) to v3.2 (2025) |
| [Academic Papers](reference/papers.md) | Published research and peer review status |

---

## Technology Stack

S4T is **technology-agnostic** by design. Any organisation can implement it regardless of vendor or budget. The reference open-source stack used in validated deployments:

| Layer | Reference Implementation |
|---|---|
| Risk Intelligence | [MISP](https://www.misp-project.org/) / [OpenCTI](https://opencti.io/) |
| Operational Security | [Wazuh](https://wazuh.com/) (EDR/SIEM) · [Zabbix](https://www.zabbix.com/) · [pfSense](https://www.pfsense.org/) / [OPNsense](https://opnsense.org/) |
| Validation & Assurance | [MITRE Caldera](https://caldera.mitre.org/) · [Atomic Red Team](https://atomicredteam.io/) · [OpenBAS](https://openbas.io/) |
| Orchestration | [Shuffle SOAR](https://shuffler.io/) · [TheHive](https://thehive-project.org/) |
| Inventory | [OCS Inventory](https://ocsinventory-ng.org/) |
| Virtualisation | [Proxmox VE](https://www.proxmox.com/) |

---

## Maturity Benchmarks

| Security Score | Level | Description |
|---|---|---|
| < 0.40 | **Initial** | Reactive posture, no structured programme |
| 0.40 – 0.65 | **Developing** | Basic controls in place, limited continuous monitoring |
| 0.65 – 0.80 | **Mature** | Structured programme with continuous validation |
| ≥ 0.80 | **Optimised** | Adaptive, self-correcting security architecture |

---

## License and Citation

This framework is released under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You are free to use, adapt, and build upon it for any purpose, including commercial use, as long as you credit the original author.

**Cite as:**
```
Neuber, D. (2024). S4T Framework: A Continuous Cybersecurity Execution Model (v3.0).
ResearchGate. https://doi.org/10.13140/RG.2.2.16699.58408
```

**Academic paper under peer review:**
Neuber, D. (2026). S4T: A Dynamic, Feedback-Driven Cybersecurity Execution Framework
with Continuous Risk Modelling and Empirical Validation.
Submitted to *Computers & Security* (Elsevier). Manuscript No. COSE-D-26-02084.

---

## Contact and Contributions

- **Feedback and questions:** [feedback@sec4.tech](mailto:feedback@sec4.tech)
- **Issues and contributions:** [GitHub Issues](https://github.com/diegoneuber/S4T-Framework/issues)
- **Assessment Tool:** [sec4.tech/assessment](https://sec4.tech/assessment)
- **Author:** Diego Neuber · [LinkedIn](https://www.linkedin.com/in/diegoneuber/) · [IEEE](https://www.ieee.org/)
