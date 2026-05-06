# S4T Framework — Service Delivery Model for MSPs

**Audience:** Managed Security Service Providers (MSSPs), IT consultancies, and vCISO practices delivering S4T to client organisations
**Reading time:** 15 minutes

---

## Overview

The S4T Framework is designed to be deliverable as a managed service. Its mathematically structured Security Score provides MSPs with a consistent, client-facing metric that communicates programme value in business language — replacing vague maturity assessments with a continuously updated, verifiable number.

This document describes how to structure S4T delivery as a client-facing service, from initial engagement through ongoing managed operations.

---

## Why S4T Works as a Managed Service

**Differentiation:** Most MSPs offer the same tool-centric services — SIEM monitoring, vulnerability scanning, patching. S4T gives you a framework-level differentiator: you are not just monitoring logs, you are managing a programme with a measurable outcome (the Security Score) that clients can understand and track.

**Repeatability:** The five-phase implementation model (Baseline → Structuring → Deployment → Continuous Operation → Optimisation) is the same across all client engagements. You build implementation capacity once and apply it across your client base.

**Ongoing revenue:** The Continuous Operation and Optimisation phases are designed to run indefinitely. Once a client is in Phase 4, monthly managed services (score reporting, BAS campaigns, patch compliance monitoring, executive reporting) create a natural recurring revenue model.

**Client retention:** The Security Score creates a visible, quantifiable demonstration of programme value each month. Clients who see their score trending from 0.38 to 0.71 over 18 months have a concrete answer to "what are we getting for this investment?" — making churn conversations much harder to initiate.

---

## Service Tiers

Structure your S4T offering across three tiers to match client size, budget, and maturity:

### Tier 1 — S4T Foundation

**Target client:** Small organisations (10–100 employees), limited IT staff, no existing security programme
**Engagement model:** Implementation project (3–6 months) + optional light managed services

**Scope:**
- Complete S4T Assessment (Executive mode) — baseline Security Score
- Asset inventory (OCS Inventory deployment)
- Wazuh deployment on all endpoints (EDR/SIEM)
- Security policy and risk appetite documentation
- Patch management SLA definition and initial implementation
- Monthly Security Score report (one-page format)
- Quarterly executive review call

**Deliverables:**
- Baseline Security Score report
- Asset inventory
- Security policy (from G layer template)
- Risk appetite statement
- Monthly one-page Security Score report

**Typical outcome after 12 months:** Score improvement from Initial (0.25–0.38) to Developing (0.48–0.58)

---

### Tier 2 — S4T Managed Programme

**Target client:** Mid-sized organisations (100–500 employees), IT team in place, some existing controls
**Engagement model:** Implementation (6–12 months) + ongoing managed services

**Scope:** Everything in Tier 1, plus:
- Full Technical Assessment (33-question mode) — layer-by-layer score
- MISP threat intelligence platform deployment and feed configuration
- Monthly BAS campaigns (Caldera or Atomic Red Team)
- SIEM tuning based on BAS results
- Incident response plan development and tabletop exercise
- Third-party risk assessment for critical vendors
- Quarterly coefficient recalibration
- Bi-annual penetration test coordination (external provider)
- Monthly executive Security Score report (expanded format)
- Quarterly board-level briefing preparation

**Deliverables:**
- Full layer-by-layer Security Score baseline
- Monthly expanded Security Score report
- Quarterly programme review presentation
- Annual penetration test integration report
- Post-incident review reports (for P1/P2 incidents)

**Typical outcome after 18 months:** Score improvement from Developing (0.40–0.55) to Mature (0.65–0.75)

---

### Tier 3 — S4T Advanced Operations

**Target client:** Larger organisations (500+ employees), regulated sectors, sophisticated threat environment
**Engagement model:** Ongoing co-managed security operations

**Scope:** Everything in Tier 2, plus:
- Continuous BAS (weekly automated campaigns via Caldera)
- Shuffle SOAR deployment for automated response orchestration
- Threat intelligence integration with SIEM (MISP → Wazuh enrichment)
- Custom Wazuh detection rule development
- Sector-specific compliance mapping (LGPD, PCI-DSS, Banco Central 4,658/2018, HIPAA, etc.)
- ML-based anomaly detection configuration (Intelligence layer)
- Monthly coefficient recalibration with OLS regression
- Custom executive dashboard (real-time Security Score)
- Dedicated security engineer point of contact

**Typical outcome after 18 months:** Score from Mature (0.65) toward Optimised (0.80+)

---

## Implementation Methodology

### Phase 1 — Discovery and Baseline (Weeks 1–4)

**Objective:** Understand the client's environment, establish the baseline Security Score, and define the engagement scope.

**Activities:**
1. Kickoff meeting with client sponsor (CISO, CIO, or equivalent) and IT lead
2. Complete S4T Technical Assessment with client security lead
3. Asset discovery scan (OCS Inventory or manual for small clients)
4. Review existing documentation (security policies, network diagrams, asset lists)
5. Interview key stakeholders: IT admin, operations lead, compliance officer
6. Identify applicable regulatory requirements
7. Document risk appetite (facilitated session with client sponsor)

**Deliverable:** Discovery Report including:
- Baseline Security Score (layer-by-layer)
- Asset inventory (draft)
- Top 5 risks above risk appetite
- Recommended service tier
- 12-month implementation roadmap

**MSP time estimate:** 16–24 hours (Tier 1), 24–40 hours (Tier 2/3)

---

### Phase 2 — Structuring and Tooling (Weeks 4–12)

**Objective:** Deploy core security tooling and establish baseline operational processes.

**Activities:**
1. Deploy Wazuh server and agents (use `/scripts/autowazuh.sh`)
2. Configure baseline SIEM detection use-cases
3. Deploy OCS Inventory for asset management
4. Configure pfSense/OPNsense if replacing existing firewall (optional, client-dependent)
5. Document security policy (use G layer template)
6. Define patch management SLAs and workflow
7. Configure MFA for remote access and privileged accounts
8. For Tier 2/3: deploy MISP and configure threat intelligence feeds

**Deliverable:** Tooling deployment report + updated asset inventory

**MSP time estimate:** 24–48 hours (Tier 1), 40–80 hours (Tier 2/3)

---

### Phase 3 — Controls Implementation (Weeks 12–24)

**Objective:** Implement the full control baseline across all six S4T layers.

**Activities:**
1. Apply CIS hardening baselines to all High criticality systems
2. Implement network segmentation (if not already in place)
3. Configure vulnerability management (Wazuh vulnerability detection + weekly reports)
4. Develop incident response plan and runbooks
5. Run first BAS campaign (Atomic Red Team) and document Va(0)
6. Tune Wazuh rules based on BAS results
7. For Tier 2/3: configure MISP → Wazuh threat intelligence integration

**Deliverable:** Control implementation report + first BAS results + updated Security Score

**MSP time estimate:** 32–60 hours (Tier 1), 60–100 hours (Tier 2/3)

---

### Phase 4 — Managed Operations (Monthly, Ongoing)

This is the recurring managed services phase. Activities are structured around four cadences:

**Weekly (MSP-led):**
- BAS campaign execution and results review (Tier 2/3)
- Critical vulnerability review — any new CISA KEV entries affecting client stack?
- Agent connectivity check — all Wazuh agents active?
- Patch SLA compliance review — any Critical CVEs past SLA?

**Monthly (MSP-led, client-reviewed):**
- Security Score calculation and trend analysis
- SIEM alert review and tuning
- Patch compliance report
- Security Score report delivered to client (see [reporting-template.md](reporting-template.md))
- Post-incident review (if applicable)

**Quarterly (MSP + client sponsor):**
- Full S4T Assessment (Technical mode)
- Layer-by-layer score comparison to previous quarter
- Coefficient recalibration (Tier 2/3, after 6+ months of data)
- Programme roadmap review and update
- Executive briefing preparation (for client board presentation)

**Annual:**
- Penetration test coordination and integration of findings
- Full programme review against 12-month roadmap
- Risk appetite statement review with client sponsor
- Year 2 roadmap development

**MSP recurring time estimate per client:**

| Tier | Weekly | Monthly | Quarterly | Annual | Total/month |
|---|---|---|---|---|---|
| Tier 1 | 1–2h | 3–4h | 8h (amortised: 2h/mo) | 16h (amortised: 1.5h/mo) | ~7–10h |
| Tier 2 | 2–4h | 6–8h | 12h (amortised: 3h/mo) | 24h (amortised: 2h/mo) | ~15–21h |
| Tier 3 | 4–8h | 10–16h | 20h (amortised: 5h/mo) | 40h (amortised: 3.5h/mo) | ~27–40h |

---

## Pricing Guidance

Pricing will vary by market and MSP positioning. The S4T framework does not prescribe pricing. The following guidance is based on typical managed security service market rates in Brazil and Latin America:

**Implementation (one-time):**
- Tier 1: R$8,000 – R$18,000
- Tier 2: R$18,000 – R$45,000
- Tier 3: R$45,000 – R$120,000+

**Managed services (monthly recurring):**
- Tier 1: R$2,500 – R$5,000/month
- Tier 2: R$5,000 – R$12,000/month
- Tier 3: R$12,000 – R$30,000+/month

**Value justification:** Frame pricing against breach risk, not against other MSP services. A Tier 2 managed programme at R$8,000/month costs R$96,000/year. A single ransomware incident at a mid-sized organisation typically costs R$200,000–R$1,000,000 in downtime, recovery, and reputational damage. The Security Score creates the reporting infrastructure to make this ROI argument continuously, not just at renewal.

---

## Multi-Client Score Management

As your S4T client base grows, you need a way to track Security Scores across all clients without manual overhead.

**Recommended approach:** Maintain a master tracking spreadsheet (or simple database) with:

| Client | Tier | Score (current) | Score (prev month) | Trend | Next action | Next review |
|---|---|---|---|---|---|---|
| Client A | 2 | 0.68 | 0.63 | ▲ +0.05 | Expand BAS coverage | 15 Jun |
| Client B | 1 | 0.44 | 0.44 | → | MTTR improvement | 22 Jun |
| Client C | 3 | 0.79 | 0.81 | ▼ -0.02 | Investigate Va(t) drop | 8 Jun |

**Clients to prioritise this month:** Any client showing a declining trend (▼) or flat trend for two consecutive months.

**Portfolio-level reporting:** For your own business purposes, tracking the distribution of client scores across maturity levels shows your programme's aggregate impact — and provides anonymised benchmark data you can share with prospective clients ("our managed clients average a Security Score of X.XX after 12 months").

---

## Common MSP Implementation Mistakes

**Starting with Tier 3 tooling for Tier 1 clients.** MISP, Caldera, and Shuffle SOAR add complexity that small clients cannot absorb. Start with Wazuh and manual BAS (Atomic Red Team); automate when the client has the operational maturity to benefit.

**Reporting tool metrics instead of programme outcomes.** "We processed 47,000 SIEM events this month" means nothing to a client. "Your Security Score improved from 0.58 to 0.64 this month, driven by a 15-percentage-point improvement in BAS detection rate" is a business outcome.

**Skipping the baseline Assessment.** Some MSPs want to start deploying tools immediately. Without a baseline Security Score, you cannot demonstrate improvement — which is the primary retention mechanism.

**Treating all clients identically.** A 30-person logistics company and a 200-person financial institution have the same S4T framework structure but very different risk profiles, regulatory requirements, and operational cadences. Customise the delivery model even if the framework is consistent.

**Not training client staff.** S4T is designed to be operated by the client's own team over time, with MSP support. Clients whose staff do not understand the framework become permanently dependent on the MSP — which creates churn risk when they find a cheaper alternative. Train clients to understand their score, read their reports, and eventually operate some activities independently.

---

## Becoming a S4T Reference Implementer

If your organisation has successfully deployed S4T for client organisations, we invite you to:

1. **Share your results** — anonymised case studies and score improvement data help the framework community improve the model
2. **Contribute to the documentation** — implementation experience from MSPs is the most valuable input for improving the practitioner guides
3. **List your organisation** — MSPs with confirmed S4T deployments can be listed as reference implementers on sec4.tech

Contact [feedback@sec4.tech](mailto:feedback@sec4.tech) or open an issue on [GitHub](https://github.com/diegoneuber/S4T-Framework/issues) to connect with the S4T community.
