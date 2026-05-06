# S4T Framework — Changelog

This document records the evolution of the S4T Framework from its operational origins in 2019 to the current version. The framework's development trajectory reflects a deliberate shift from technology-specific deployment tooling toward a technology-agnostic, mathematically formalised maturity measurement model.

---

## v3.2 — 2025 (Current)

**Status:** Active production deployment · 6 countries · 15+ organisations

**Focus:** Public tooling, international reach, and documentation

### What's new
- **S4T Assessment Tool** — publicly available at [sec4.tech/assessment](https://sec4.tech/assessment). Free, no-registration tool implementing the Security Score computation across all six framework layers. Available in English and Portuguese.
- **GitHub public repository** — framework documentation, deployment scripts, and reference implementation publicly released.
- **International deployments** — confirmed production deployments across Brazil, Chile, Peru, Argentina, United States, and Germany.
- **Deployment in regulated sectors** — validated in financial services (under Banco Central do Brasil Resolution 4,658/2018), healthcare, logistics, and professional services.
- **Coefficient defaults published** — cross-sector baseline coefficients (α = 0.35, β = 0.25, γ = 0.30, δ = 0.10) derived from the 18-month validation study made publicly available.

### Academic output
- Manuscript submitted to *Computers & Security* (Elsevier) — Manuscript No. **COSE-D-26-02084**, submitted April 25, 2026. Currently under peer review.

---

## v3.0 — December 2024

**DOI:** [10.13140/RG.2.2.16699.58408](https://doi.org/10.13140/RG.2.2.16699.58408)

**Focus:** Mathematical formalisation of the risk evolution model and empirical validation

This version represents the most significant conceptual advancement in the framework's history. The qualitative resilience architecture of v2.0 was transformed into a mathematically rigorous, continuously computable model — fulfilling the research agenda announced in the 2022 publication.

### Core innovations introduced in v3.0

**Risk Evolution Equation**
```
dR/dt = δT(t) − αC(t) − βO(t) − γVa(t)
```
Cybersecurity risk is modelled as a time-dependent trajectory governed by four measurable state variables: Threat Exposure T(t), Control Coverage C(t), Operational Maturity O(t), and Validation Effectiveness Va(t).

**Security Score**
```
S(t) = [C(t)^α · O(t)^β · Va(t)^γ] / R(t)^δ
```
A single dimensionless metric bridging operational security data and executive risk reporting. Four maturity bands: Initial (< 0.40), Developing (0.40–0.65), Mature (0.65–0.80), Optimised (≥ 0.80).

**Formal 6-tuple specification**
```
S4T = (G, RI, CF, OS, VA, L)
```

**Equilibrium analysis**
```
R* = δT* / (αC* + βO* + γVa*)
```
Quantifies the minimum achievable risk level given an organisation's threat environment and control capacity — enabling evidence-based target setting.

**Empirical validation**
18-month longitudinal observational study across five organisations in financial services, healthcare, manufacturing, and professional services:

| Metric | Pre-S4T | Post-S4T | Cohen's d | p-value |
|---|---|---|---|---|
| Control Coverage | 45% ± 8% | 82% ± 5% | 4.8 | < 0.001 |
| MTTR (hours) | 72 ± 15 | 18 ± 4 | 3.9 | 0.002 |
| Critical Vulns | 100 ± 20 | 33 ± 7 | 4.2 | < 0.001 |
| Incidents/month | 24 ± 5 | 11 ± 3 | 2.8 | 0.010 |
| Security Score | 0.38 ± 0.05 | 0.79 ± 0.04 | 7.1 | < 0.001 |

**Technology-agnostic reference implementation** — framework explicitly decoupled from any specific vendor stack. Open-source reference implementations documented per layer.

---

## v2.5 — 2023

**Focus:** Governance layer expansion and international adoption

### What's new
- **Inventory & Governance pillar** — OCS Inventory integrated as the asset visibility layer. Asset inventory formalised as a prerequisite for all other layers.
- **International expansion** — framework adopted in Germany (F H Dresden) and Argentina (Fixy Logística), expanding beyond South America.
- **Brazil multi-sector growth** — growing adoption base across logistics, communications, accounting, and construction sectors.
- **IAM controls formalised** — Identity and Access Management (MFA, PAM, SSO) standardised as OS layer requirements.

---

## v2.0 — 2022

**DOI:** [10.5281/zenodo.20054242](https://doi.org/10.5281/zenodo.20054242)

**Focus:** Formalisation as a strategic resilience framework

This version marked the framework's conceptual pivot — from an operational deployment tool toward a strategic cybersecurity architecture. The paper explicitly identified the absence of a computable, time-evolving risk metric as a structural gap in existing frameworks (ISO 27001, NIST CSF, COBIT, CIS Controls) and announced quantitative modelling as the primary direction for future work.

### Core architecture introduced in v2.0

**Five strategic domains:**
1. Governance and Leadership
2. Risk and Resilience Management
3. Security Architecture and Engineering
4. Threat Detection and Intelligence
5. Incident Response and Recovery

**Resilience lifecycle** — continuous cycle of prevention, detection, response, and recovery, treated as interdependent rather than sequential.

**Key positioning statement from the 2022 paper:**
> "Future work may include empirical validation, case studies, and quantitative resilience metrics."
> — fulfilled in v3.0 (2024)

**Differentiation from existing frameworks** — S4T articulated as an *integrating architecture* that aligns ISO 27001, NIST CSF, and CIS Controls toward measurable resilience outcomes, rather than a competing control standard.

---

## v1.5 — 2021

**Focus:** EDR/SIEM integration and deployment automation

### What's new
- **Wazuh integration** — Wazuh adopted as the primary EDR/SIEM platform within the framework.
- **Automated deployment scripts** — deploy automation reduced implementation time from days to hours. Shell scripts for Wazuh and Zabbix deployment published.
- **Detection use-cases standardised** — baseline SIEM use-cases (failed logins, privilege escalation, lateral movement) formalised as minimum requirements.
- **Incident response documentation** — initial IR runbook templates developed.

---

## v1.0 — 2020

**Focus:** First structured architecture

This version formalised the framework's four operational pillars and achieved the first production deployment in Brazil.

### Four pillars formalised
1. **Perimeter Protection** — hardened firewalls, network segmentation, IDS/IPS (pfSense, Snort/Suricata)
2. **Detection & Response** — continuous endpoint monitoring, event correlation, automated alerts (Wazuh, Zabbix)
3. **Inventory & Governance** — IT asset visibility, access policies, configuration traceability (OCS Inventory)
4. **Resilience & Recovery** — backup strategy with offsite retention, tested continuity plan, measurable RTO/RPO (Proxmox Backup Server)

**First production deployment** — framework deployed in a real production environment in Brazil, consolidating firewall, monitoring, and backup into a cohesive architecture.

---

## Origin — 2019

**Focus:** Infrastructure security research and operational tooling

The S4T Framework originated in studies of cybersecurity infrastructure for small and medium-sized Brazilian organisations. Early work focused on identifying why security investments consistently failed to translate into operational resilience — a problem the author observed across multiple client environments.

Initial output: hardening scripts and deployment automation for open-source security tooling (pfSense, Wazuh, Zabbix, Proxmox) in lab and early production environments.

**The core observation that drove the framework's eventual direction:**
Organisations were deploying individual security tools in isolation — firewall here, antivirus there, SIEM somewhere else — without a coherent architecture linking them to measurable outcomes. The problem was not the tools. The problem was the absence of a measurement model that told an organisation whether it was actually becoming more secure over time.

This observation became the founding premise of the S4T Framework.

---

## Architectural Evolution Summary

| Version | Year | Primary Focus | DOI / Reference |
|---|---|---|---|
| Origin | 2019 | Operational tooling and infrastructure hardening | — |
| v1.0 | 2020 | Four-pillar structured architecture, first production deployment | — |
| v1.5 | 2021 | EDR/SIEM integration, deployment automation | — |
| **v2.0** | **2022** | **Strategic resilience framework, conceptual formalisation** | **[10.5281/zenodo.20054242](https://doi.org/10.5281/zenodo.20054242)** |
| v2.5 | 2023 | Governance layer, international expansion | — |
| **v3.0** | **2024** | **Mathematical model, Security Score, empirical validation** | **[10.13140/RG.2.2.16699.58408](https://doi.org/10.13140/RG.2.2.16699.58408)** |
| v3.2 | 2025 | Public tooling, 6-country deployment, documentation | — |
| **v3.2+** | **2026** | **Peer-reviewed paper under review** | **COSE-D-26-02084 (Computers & Security, Elsevier)** |

---

*This changelog is maintained as part of the S4T Framework public documentation. For the complete academic treatment, see [reference/papers.md](papers.md).*
