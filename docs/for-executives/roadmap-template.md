# S4T Programme Roadmap Template

**Purpose:** Template for presenting a Security Score improvement roadmap to executive leadership or board
**Usage:** Customise with your organisation's actual score, targets, and timelines

---

## How to Use This Template

1. Complete the S4T Assessment at [sec4.tech/assessment](https://sec4.tech/assessment) to establish your baseline score
2. Identify your target score and timeline with your security lead
3. Fill in the sections below with your actual data
4. Present to leadership for approval and resource commitment

The roadmap should be reviewed and updated quarterly. Targets and timelines should be adjusted based on actual progress.

---

# [Organisation Name] — Cybersecurity Maturity Roadmap

**Prepared by:** [Name, Title]
**Date:** [Date]
**Review date:** [Date + 90 days]
**Approved by:** [Name, Title]

---

## Executive Summary

[Organisation Name]'s current cybersecurity maturity level is **[Initial / Developing / Mature / Optimised]**, with a Security Score of **[X.XX]** as of [Month Year]. This roadmap outlines the programme investments and milestones required to reach a Security Score of **[X.XX]** ([target level]) by [target date].

The programme is structured around the S4T Framework — an open source cybersecurity maturity model that provides a continuously updated Security Score across six capability layers. Independent validation across multiple organisations demonstrates that programmes following this framework achieve an average Security Score improvement of [X.XX] over 12–18 months.

**Investment required:** [R$ / USD amount] over [timeframe]
**Expected risk reduction:** [X]% reduction in critical vulnerabilities, MTTR from [X]h to [Y]h
**Regulatory alignment:** [List applicable regulations: LGPD, PCI-DSS, ISO 27001, etc.]

---

## Current State

### Security Score Baseline

```
Overall Score:  [X.XX]  —  [Initial / Developing / Mature / Optimised]

Layer breakdown:
  G  — Governance:           [X.XX]  [█████████░░░░░░░░░░░░░░░]
  RI — Risk Intelligence:    [X.XX]  [█████████░░░░░░░░░░░░░░░]
  CF — Control Framework:    [X.XX]  [█████████░░░░░░░░░░░░░░░]
  OS — Operational Security: [X.XX]  [█████████░░░░░░░░░░░░░░░]
  VA — Validation:           [X.XX]  [█████████░░░░░░░░░░░░░░░]
  L  — Adaptive Learning:    [X.XX]  [█████████░░░░░░░░░░░░░░░]

Assessment date: [Date]
Assessment mode: [Executive / Technical]
```

### Key Risk Indicators (current)

| Indicator | Current | Industry benchmark | Gap |
|---|---|---|---|
| Mean Time to Respond | [X hours] | < 4 hours (Mature) | [Y hours] |
| Critical vulnerabilities open | [N] | < 5 | [N-5] |
| Patch SLA compliance (Critical) | [X%] | > 90% | [gap %] |
| BAS detection rate | [X%] | > 70% (Mature) | [gap %] |
| MFA coverage (remote access) | [X%] | 100% | [gap %] |
| Asset inventory completeness | [X%] | > 95% | [gap %] |

### Primary Risks Above Risk Appetite

Based on our risk appetite statement approved [date], the following risks currently exceed our stated tolerance:

1. **[Risk description]** — Current level: [High/Medium] — Appetite: [Low/Medium] — Programme: [Mitigation plan]
2. **[Risk description]** — ...
3. **[Risk description]** — ...

---

## Target State

### 12-Month Security Score Target

```
Current:  [X.XX]  ████████░░░░░░░░░░░░░░░░
Target:   [X.XX]  ████████████████░░░░░░░░
```

**Rationale for target:** [Why this target? Regulatory requirement? Board direction? Incident response?]

### Target Key Risk Indicators

| Indicator | Current | 12-month target | How achieved |
|---|---|---|---|
| Mean Time to Respond | [X hours] | [Y hours] | OS layer — Orchestration automation |
| Critical vulnerabilities open | [N] | < 5 | RI + OS layer — Patch management SLAs |
| Patch SLA compliance | [X%] | > 90% | OS layer — Automated patching |
| BAS detection rate | [X%] | > [Y%] | VA layer — Weekly BAS campaigns |
| MFA coverage | [X%] | 100% | G + OS layer — IAM rollout |

---

## Implementation Roadmap

### Q1 — Foundation ([Month] – [Month])

**Score target at end of Q1:** [X.XX]
**Primary focus:** [e.g., Asset inventory completion and governance documentation]

| Initiative | Layer | Owner | Effort | Expected score impact |
|---|---|---|---|---|
| Complete asset inventory | CF | [Name] | [X days] | C(t): +[X.XX] |
| Approve risk appetite statement | G | [Name] | [X days] | Governance foundation |
| Deploy Wazuh on all endpoints | OS | [Name] | [X days] | O(t): +[X.XX] |
| Document incident response process | OS | [Name] | [X days] | O(t): +[X.XX] |
| Implement MFA for remote access | OS | [Name] | [X days] | C(t): +[X.XX] |

**Q1 budget:** [R$ / USD]
**Q1 dependencies:** [Any external requirements, approvals, or procurement needed]

---

### Q2 — Controls and Monitoring ([Month] – [Month])

**Score target at end of Q2:** [X.XX]
**Primary focus:** [e.g., Control implementation and continuous monitoring]

| Initiative | Layer | Owner | Effort | Expected score impact |
|---|---|---|---|---|
| Implement patch management SLAs | OS | [Name] | [X days] | O(t): +[X.XX] |
| Configure SIEM detection use-cases | OS | [Name] | [X days] | O(t): +[X.XX] |
| Deploy threat intelligence feeds | RI | [Name] | [X days] | T(t) reduction |
| Run first BAS campaign | VA | [Name] | [X days] | Va(t) baseline |
| Complete CIS hardening baseline | CF | [Name] | [X days] | C(t): +[X.XX] |

**Q2 budget:** [R$ / USD]

---

### Q3 — Validation and Improvement ([Month] – [Month])

**Score target at end of Q3:** [X.XX]
**Primary focus:** [e.g., Control validation and automated response]

| Initiative | Layer | Owner | Effort | Expected score impact |
|---|---|---|---|---|
| Automate weekly BAS campaigns | VA | [Name] | [X days] | Va(t): +[X.XX] |
| Tune Wazuh rules based on BAS | OS | [Name] | [X days] | O(t): +[X.XX] |
| Implement automated response | OS | [Name] | [X days] | O(t): +[X.XX] |
| First external penetration test | VA | [External] | [Cost] | Va(t): +[X.XX] |
| Establish monthly KPI reporting | L | [Name] | [X days] | L layer baseline |

**Q3 budget:** [R$ / USD]

---

### Q4 — Maturation and Optimisation ([Month] – [Month])

**Score target at end of Q4:** [X.XX]
**Primary focus:** [e.g., Programme maturation and adaptive learning]

| Initiative | Layer | Owner | Effort | Expected score impact |
|---|---|---|---|---|
| Coefficient recalibration (Phase 2) | L | [Name] | [X days] | Score accuracy |
| Third-party risk assessment | RI | [Name] | [X days] | T(t) reduction |
| Post-incident review process | L | [Name] | [X days] | L(t): +[X.XX] |
| Programme roadmap update (Year 2) | L | [Name] | [X days] | Strategic continuity |
| Executive security review | G | [Name] | [X days] | Governance maturity |

**Q4 budget:** [R$ / USD]

---

## Budget Summary

| Quarter | Budget | Primary allocation |
|---|---|---|
| Q1 | [R$ / USD] | Tooling (Wazuh), staff time |
| Q2 | [R$ / USD] | Configuration, intelligence feeds |
| Q3 | [R$ / USD] | BAS tooling, penetration test |
| Q4 | [R$ / USD] | Programme maturation |
| **Total Year 1** | **[R$ / USD]** | |

**Tooling costs (open source reference stack):**

| Tool | Purpose | Licence cost |
|---|---|---|
| Wazuh | EDR/SIEM | Free (open source) |
| MITRE Caldera | Breach and Attack Simulation | Free (open source) |
| MISP | Threat Intelligence | Free (open source) |
| pfSense / OPNsense | Firewall | Free (open source) |
| Proxmox VE | Virtualisation | Free (open source) |
| OCS Inventory | Asset Management | Free (open source) |
| External penetration test | Annual validation | [Vendor quote] |

**Primary costs are staff time and the annual penetration test.** The open-source reference stack achieves near-zero software licensing cost, making S4T accessible regardless of budget constraints.

---

## Risk Register (Programme Risks)

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Staff turnover during implementation | Medium | High | Document all configurations; cross-train |
| Business priority conflicts delaying implementation | High | Medium | Executive sponsorship; quarterly roadmap reviews |
| Tooling deployment issues | Low | Medium | Proof-of-concept in test environment before production |
| Scope creep beyond initial asset inventory | Medium | Medium | Define scope clearly in Q1; change control process |

---

## Governance and Reporting

**Programme sponsor:** [Name, Title]
**Programme lead (CISO / Security Lead):** [Name]
**Reporting cadence:**

| Report | Frequency | Audience | Format |
|---|---|---|---|
| Security Score report | Monthly | CISO, CIO | One-page dashboard |
| Programme status | Quarterly | Executive committee | This roadmap + progress update |
| Board security brief | Quarterly or annual | Board of directors | Executive summary |
| Incident report | Ad hoc (P1/P2) | Executive committee | Incident summary |

---

## Approval and Commitment

By approving this roadmap, the executive team commits to:

- Providing the budget outlined above for Year 1 implementation
- Allocating [X FTE / X% of IT team time] to programme activities
- Receiving and reviewing the monthly Security Score report
- Resolving escalated risks and priority conflicts within [X business days]

| Name | Title | Signature | Date |
|---|---|---|---|
| | CEO | | |
| | CIO / CTO | | |
| | CISO / Security Lead | | |
| | CFO (if budget approval required) | | |

---

*This roadmap was developed using the S4T Framework (sec4.tech). The Security Score methodology is documented in: Neuber, D. (2024). S4T Framework v3.0. DOI: [10.13140/RG.2.2.16699.58408](https://doi.org/10.13140/RG.2.2.16699.58408)*
