# S4T Framework — Academic Papers and Research

This page documents the academic research underpinning the S4T Framework, in chronological order of development.

---

## Published Work

### S4T Framework v2.0 (2022)
**Title:** S4T Framework v2.0: A Resilience-Driven Cybersecurity Framework Integrating Governance, Risk, and Technical Controls
**Author:** Diego Neuber
**Year:** 2022
**Repository:** Zenodo (CERN)
**DOI:** [10.5281/zenodo.20054242](https://doi.org/10.5281/zenodo.20054242)
**License:** CC BY 4.0

**Abstract:** Introduces S4T as a resilience-driven cybersecurity framework integrating governance, enterprise risk management, and applied security engineering into a unified strategic model. Positions cyber resilience as a core business capability rather than a technical function. Identifies the absence of a computable, time-evolving risk metric as a structural gap in existing frameworks and announces quantitative modelling as the primary direction for future work.

**Citation:**
```
Neuber, D. (2022). S4T Framework v2.0: A Resilience-Driven Cybersecurity Framework
Integrating Governance, Risk, and Technical Controls. Zenodo.
https://doi.org/10.5281/zenodo.20054242
```

---

### S4T Framework v3.0 (2024)
**Title:** S4T Framework: A Continuous Cybersecurity Execution Model
**Author:** Diego Neuber
**Year:** 2024
**Repository:** ResearchGate
**DOI:** [10.13140/RG.2.2.16699.58408](https://doi.org/10.13140/RG.2.2.16699.58408)
**License:** CC BY 4.0

**Abstract:** Introduces the mathematical formalisation of the S4T Framework, fulfilling the research agenda announced in v2.0. Core innovations include: (1) a differential equation modelling risk as a time-dependent trajectory (dR/dt = δT(t) − αC(t) − βO(t) − γVa(t)); (2) the Security Score metric S(t) = [C(t)^α · O(t)^β · Va(t)^γ] / R(t)^δ enabling longitudinal benchmarking; (3) formal 6-tuple specification S4T = (G, RI, CF, OS, VA, L); and (4) empirical validation across five organisations over 18 months demonstrating statistically significant improvements (Security Score: 0.38 → 0.79, Cohen's d = 7.1, p < 0.001).

**Citation:**
```
Neuber, D. (2024). S4T Framework: A Continuous Cybersecurity Execution Model (v3.0).
ResearchGate. https://doi.org/10.13140/RG.2.2.16699.58408
```

---

## Under Peer Review

### Computers & Security submission (2026)
**Title:** S4T: A Dynamic, Feedback-Driven Cybersecurity Execution Framework with Continuous Risk Modelling and Empirical Validation
**Author:** Diego Neuber
**Journal:** *Computers & Security* (Elsevier)
**ISSN:** 0167-4048
**Indexing:** Scopus, Web of Science
**Manuscript Number:** COSE-D-26-02084
**Submitted:** April 25, 2026
**Status:** Under editorial review

**Abstract:** Static governance frameworks such as ISO 27001, NIST CSF 2.0, COBIT 2019, and CIS Controls v8 model organisational cyber risk as a periodic snapshot rather than a time-evolving process, creating a structural gap between compliance posture and operational security. This paper introduces S4T (Secure Framework for Technology), a continuous cybersecurity execution model that addresses this gap by: (i) formalising risk dynamics through a differential equation with four measurable state variables; (ii) integrating automated Breach and Attack Simulation (BAS) as the primary control validation mechanism; (iii) coupling an Orchestration layer for automated response with an Intelligence layer for adaptive model recalibration; and (iv) defining a composite, dimensionless Security Score enabling longitudinal benchmarking. An 18-month longitudinal observational study across five Brazilian organisations demonstrates statistically significant improvements across all primary risk indicators.

**Keywords:** cybersecurity framework; dynamic risk modelling; continuous validation; breach and attack simulation; security score; feedback control; cyber resilience

> *This page will be updated when a publication decision is received.*

---

## How to Cite S4T

For general use of the framework, cite the most recent published version:

```
Neuber, D. (2024). S4T Framework: A Continuous Cybersecurity Execution Model (v3.0).
ResearchGate. https://doi.org/10.13140/RG.2.2.16699.58408
```

For the foundational conceptual architecture (v2.0):
```
Neuber, D. (2022). S4T Framework v2.0: A Resilience-Driven Cybersecurity Framework
Integrating Governance, Risk, and Technical Controls. Zenodo.
https://doi.org/10.5281/zenodo.20054242
```

---

## Related Reading

These external works are referenced in the S4T v3.0 mathematical model and provide useful background:

- **Gordon & Loeb (2002)** — Economic theory of optimal security investment. *ACM TISSEC*, 5(4), 438–457. Foundational work on security investment under static assumptions.
- **Wang et al. (2013)** — k-zero day safety: a network security metric. *IEEE TDSC*, 11(1), 30–44. Direct mathematical precursor to S4T's risk evolution equation.
- **Fielder et al. (2016)** — Decision support approaches for cyber security investment. *Decision Support Systems*, 86, 13–23. Demonstrates that dynamic programming outperforms greedy allocation under realistic threat models.
- **NIST CSF 2.0 (2024)** — [doi.org/10.6028/NIST.CSWP.29](https://doi.org/10.6028/NIST.CSWP.29) — Framework whose limitations S4T addresses.
- **MITRE ATT&CK** — [attack.mitre.org](https://attack.mitre.org) — Adversary behaviour taxonomy used for BAS coverage mapping in the VA layer.
