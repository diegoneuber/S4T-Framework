# Getting Started with S4T

This guide is for security practitioners — analysts, engineers, and security leads — who want to implement the S4T Framework in their organisation. It assumes familiarity with cybersecurity concepts but does not require expertise in any specific vendor platform.

**Time to read:** 15 minutes
**Time to complete Phase 1:** 30–90 days

---

## Before You Start

### Take the Assessment

Before reading further, take the [S4T Assessment Tool](https://sec4.tech/assessment) — it takes 5 minutes and will tell you your current Security Score and which framework layers need the most attention. This gives you a baseline and helps you prioritise where to focus first.

The assessment produces a score between 0 and 1, mapped to four maturity levels:

| Score | Level | What it means |
|---|---|---|
| < 0.40 | **Initial** | Reactive posture, no structured programme |
| 0.40 – 0.65 | **Developing** | Basic controls in place, gaps in monitoring and validation |
| 0.65 – 0.80 | **Mature** | Structured programme with continuous monitoring |
| ≥ 0.80 | **Optimised** | Adaptive, self-correcting architecture |

Most organisations implementing S4T for the first time score between 0.25 and 0.45.

---

## What You Are Building

S4T is formally defined as a 6-tuple:

```
S4T = (G, RI, CF, OS, VA, L)
```

Six layers that work together as a continuous system — not a checklist to complete once and file away.

| Layer | Code | What it does |
|---|---|---|
| Governance | G | Sets direction, risk appetite, and accountability |
| Risk Intelligence | RI | Monitors the threat landscape and vulnerability landscape |
| Control Framework | CF | Implements risk-prioritised controls across your asset base |
| Operational Security | OS | Runs continuous detection, response, and patching operations |
| Validation & Assurance | VA | Tests whether your controls actually work |
| Adaptive Learning | L | Measures outcomes, recalibrates, and improves |

The framework's central metric is the **Security Score**:

```
S(t) = [C(t)^α · O(t)^β · Va(t)^γ] / R(t)^δ
```

Where C(t), O(t), and Va(t) represent your control coverage, operational maturity, and validation effectiveness — and R(t) represents your current risk level. As the numerator grows and the denominator shrinks, your score rises.

**You do not need to compute this formula manually.** The Assessment Tool computes it for you. Understanding the structure matters because it tells you what levers to pull: improving any of the three components in the numerator, or reducing your threat exposure, will increase your score.

---

## Prerequisites

### Minimum viable starting point

S4T does not require a large security team or a significant budget. Validated deployments have been completed by teams of one to three people using exclusively open-source tooling. What you do need:

**Organisational:**
- Executive or management buy-in for at least a 12-month programme
- Someone accountable for security outcomes (does not have to be a full-time CISO)
- A risk appetite statement — even an informal one ("we cannot afford more than X hours of downtime")

**Technical:**
- An asset inventory — even an incomplete spreadsheet is a starting point
- At least one server or VM available for security tooling deployment
- Network access to endpoints for monitoring agent installation

**Skills:**
- Comfort with Linux command line
- Basic networking knowledge (VLANs, firewall rules, DNS)
- No specialised security certifications required — the framework documentation provides implementation guidance for each layer

### Technology stack

S4T is technology-agnostic. Any organisation can implement it with its existing tools. The reference open-source stack used in the validated deployments:

| Layer | Tool | Purpose |
|---|---|---|
| RI | [MISP](https://www.misp-project.org/) / [OpenCTI](https://opencti.io/) | Threat intelligence |
| OS — EDR/SIEM | [Wazuh](https://wazuh.com/) | Endpoint detection and log management |
| OS — Monitoring | [Zabbix](https://www.zabbix.com/) | Infrastructure and availability monitoring |
| OS — Firewall | [pfSense](https://www.pfsense.org/) / [OPNsense](https://opnsense.org/) | Perimeter protection |
| VA | [MITRE Caldera](https://caldera.mitre.org/) / [Atomic Red Team](https://atomicredteam.io/) | Breach and attack simulation |
| Orchestration | [Shuffle SOAR](https://shuffler.io/) | Automated response |
| Inventory | [OCS Inventory](https://ocsinventory-ng.org/) | Asset management |
| Virtualisation | [Proxmox VE](https://www.proxmox.com/) | Infrastructure platform |

This stack achieves near-zero licensing cost. You may substitute any of these tools with commercial equivalents — the framework works the same way.

---

## Implementation Phases

S4T deployment follows five phases. The timeline below assumes a small to mid-sized organisation (50–500 endpoints) with a team of two to three people.

### Phase 1 — Baseline Assessment (Months 1–3)

**Goal:** Establish where you are before doing anything else.

This phase is about measurement, not improvement. Resist the urge to start fixing things before you have a baseline — without it, you cannot measure progress.

**Activities:**

1. **Complete an asset inventory.** List every device, server, application, and user account in scope. Use OCS Inventory for automated discovery, or start with a spreadsheet. Completeness matters more than perfection.

2. **Map your existing controls.** For each of the six S4T layers, document what you currently have in place — even if the answer is "nothing." Use the layer guides ([G](layer-G.md), [RI](layer-RI.md), [CF](layer-CF.md), [OS](layer-OS.md), [VA](layer-VA.md), [L](layer-L.md)) as checklists.

3. **Establish baseline metrics.** Record your starting values for the four state variables that drive the Security Score:
   - **C(0):** What percentage of your critical assets have security controls implemented and verified?
   - **O(0):** What is your current Mean Time to Respond to incidents?
   - **Va(0):** Have you tested whether your controls detect known attack techniques? If not, Va(0) ≈ 0.
   - **T(0):** What is your current threat exposure? (Asset count, internet-exposed services, unpatched CVEs.)

4. **Take the Technical Assessment** at [sec4.tech/assessment](https://sec4.tech/assessment) — the 33-question version gives layer-by-layer scores. Save your results.

5. **Document a risk appetite statement.** Answer these questions in writing: What is the maximum acceptable downtime for critical systems? What categories of data are most sensitive? What regulatory requirements apply?

**Deliverables at end of Phase 1:**
- Asset inventory (draft)
- Baseline Security Score (from Assessment Tool)
- Risk appetite statement
- Gap analysis against each of the six layers

---

### Phase 2 — Structuring (Months 3–6)

**Goal:** Define your control roadmap and configure your tooling.

**Activities:**

1. **Prioritise controls.** Using your Phase 1 gap analysis, rank control gaps by risk impact. Use the equilibrium equation to think about priorities:
   ```
   R* = δT* / (αC* + βO* + γVa*)
   ```
   Controls that reduce your most significant threat vectors (T) or that dramatically increase C or O have the highest return on investment.

2. **Configure core tooling.** Deploy and configure your chosen tools for the OS layer first — Wazuh for EDR/SIEM is the highest-impact starting point for most organisations. Use the deployment scripts in the `/scripts` directory of this repository.

3. **Define incident response procedures.** Document your incident response plan with defined roles, escalation paths, and communication procedures. A simple one-page plan is better than no plan.

4. **Set target metrics.** Based on your baseline, define 12-month targets for C(t), O(t), and Va(t). Realistic targets for an organisation starting at Score 0.35: reach Score 0.55–0.65 (Developing to Mature transition) within 12 months.

---

### Phase 3 — Deployment (Months 6–12)

**Goal:** Implement core controls across all six layers.

This is where most of the hands-on work happens. Work through each layer guide in order — Governance first, then Risk Intelligence, then Control Framework, then Operational Security. Validation and Adaptive Learning are continuous activities that begin here and never stop.

**Priority sequence:**
1. G — Governance (sets the foundation for everything else)
2. CF — Control Framework (asset inventory and baseline controls)
3. OS — Operational Security (monitoring and detection)
4. RI — Risk Intelligence (threat context for prioritisation)
5. VA — Validation & Assurance (testing that controls work)
6. L — Adaptive Learning (measurement and improvement)

**Key milestone:** At the end of Phase 3, run a complete BAS campaign using Caldera or Atomic Red Team. This gives you your first real Va(t) measurement — the proportion of attack techniques your controls detected or blocked. Most organisations see Va(0) ≈ 0.15–0.30 on first BAS run. This is normal and expected.

---

### Phase 4 — Continuous Operation (Ongoing)

**Goal:** Run the Monitor–Analyse–Act–Learn cycle continuously.

This is the operational state S4T is designed to maintain indefinitely. The cycle runs at four cadences:

| Cadence | Activity |
|---|---|
| **Continuous** | SIEM monitoring, EDR alerting, firewall log analysis |
| **Daily** | Alert triage, vulnerability prioritisation, patch status review |
| **Weekly** | BAS campaign execution, control coverage review |
| **Monthly** | Security Score calculation, executive reporting, metric review |
| **Quarterly** | Coefficient recalibration, strategic roadmap review, full assessment |

**Monthly Security Score reporting** is the most important operational habit. Calculate your score using the Assessment Tool or manually, record it, and trend it over time. A score that is rising — even slowly — means your programme is working. A score that is flat or declining is a signal to investigate.

---

### Phase 5 — Optimisation (Quarterly)

**Goal:** Recalibrate your model and realign your strategy.

Each quarter:
1. Recalculate the risk evolution equation coefficients using observed data from the past 12 months.
2. Review your risk appetite statement — has your organisation's risk tolerance changed?
3. Update your threat intelligence — what new attack techniques are active in your sector?
4. Set new targets for the next quarter based on your current score trajectory.

---

## Common Implementation Mistakes

**Starting with tools instead of strategy.** Deploying Wazuh before defining a risk appetite statement is backwards — you will not know what to monitor for or what to do when alerts fire.

**Treating the Assessment Tool as a one-time exercise.** The score is meaningful only as a trend over time. Take it quarterly at minimum.

**Skipping the VA layer.** Most organisations implement controls without ever testing whether those controls actually detect attacks. Va(t) = 0 means your score is artificially inflated — your controls may exist on paper but fail in practice.

**Optimising for the score instead of for security.** The Security Score is a measurement instrument, not the goal. Focus on the underlying activities; the score will follow.

**Trying to reach Optimised in year one.** The validated deployments reached Mature (0.65+) within 12–18 months of programme initiation. Optimised (0.80+) typically requires 24–36 months of continuous operation.

---

## Next Steps

Once you have read this guide, proceed to the layer that your Assessment results identified as your lowest-scoring:

- [Layer G — Governance](layer-G.md)
- [Layer RI — Risk Intelligence](layer-RI.md)
- [Layer CF — Control Framework](layer-CF.md)
- [Layer OS — Operational Security](layer-OS.md)
- [Layer VA — Validation & Assurance](layer-VA.md)
- [Layer L — Adaptive Learning](layer-L.md)

If you are an MSP implementing S4T for a client organisation, see the [Service Delivery Model](../for-msps/service-delivery.md).

If you have questions or want to share results, open an issue on [GitHub](https://github.com/diegoneuber/S4T-Framework/issues) or contact [feedback@sec4.tech](mailto:feedback@sec4.tech).
