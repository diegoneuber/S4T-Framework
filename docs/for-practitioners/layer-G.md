# Layer G — Governance

**Position in the framework:** S4T = (**G**, RI, CF, OS, VA, L)
**Drives:** The foundation for all other layers
**Primary output:** Risk appetite statement, security policy, executive alignment

---

## What This Layer Does

Governance is the first layer of S4T and the most frequently underestimated. Most organisations want to start with technology — deploy a SIEM, buy an EDR tool, run a penetration test. But technology without governance is reactive by definition: you are deploying tools without knowing what you are protecting, why, or what level of risk is acceptable.

The Governance layer answers four questions that every other layer depends on:

1. **What are we protecting?** (Assets, data, services)
2. **From what?** (Threat landscape, risk appetite)
3. **Who is responsible?** (Ownership, accountability)
4. **How do we know if it is working?** (Metrics, reporting)

Without clear answers to these questions, every other layer operates without direction. Controls are deployed for the wrong assets, incidents are escalated to the wrong people, and security investments cannot be justified to leadership because there is no baseline to measure against.

---

## Prerequisites

The Governance layer has no technical prerequisites. It requires:
- [ ] Access to business leadership (CEO, COO, or equivalent) for at least one working session
- [ ] Knowledge of which regulations apply to your organisation (LGPD, GDPR, PCI-DSS, HIPAA, sector-specific)
- [ ] Understanding of which systems are most critical to business operations

---

## G Layer Components

### G-1: Security Policy

**What it is:** A formal document defining the organisation's approach to information security — what is required, who is responsible, and what the consequences of non-compliance are.

**A security policy does not need to be long.** A three to five page document that is actually read and followed is more valuable than a 200-page document that lives in a shared drive.

**Minimum required sections:**

**1. Scope**
What systems, data, and people does this policy cover? Define clearly.
> *Example: "This policy applies to all information systems owned or operated by [Organisation Name], all employees and contractors with access to those systems, and all data classified as Confidential or above."*

**2. Information Classification**
Define at least three data classification levels and the handling requirements for each:

| Level | Definition | Examples | Requirements |
|---|---|---|---|
| Public | Approved for external distribution | Marketing materials, public website | No restrictions |
| Internal | For internal use only | Procedures, internal reports | Do not share externally |
| Confidential | Sensitive business or personal data | Customer data, financial records, PII | Encrypt at rest and in transit, access control required |
| Restricted | Highest sensitivity | Credentials, encryption keys, regulated health data | Strict need-to-know, logged access |

**3. Acceptable Use**
Define what employees may and may not do with organisational systems:
- Approved uses of company devices
- Prohibited activities (personal software installation, accessing prohibited content categories)
- Personal use policy (if permitted, under what conditions)
- Remote work requirements (VPN required for accessing internal systems)

**4. Incident Reporting**
How should employees report suspected security incidents?
- Who to contact (name, email, phone)
- What constitutes an incident worth reporting (lost device, suspicious email, unusual system behaviour)
- Response time commitment from the security team

**5. Roles and Responsibilities**
Who is accountable for security outcomes?

| Role | Responsibilities |
|---|---|
| CISO / Security Lead | Overall security programme ownership, risk reporting to leadership |
| IT Administrator | System hardening, patch management, access provisioning |
| Data Owner (per system) | Classification decisions, access approval |
| All Employees | Compliance with policy, incident reporting, security awareness |

**6. Policy Review**
Policies must be reviewed and updated. Define frequency (annually is minimum) and who approves changes.

**Template approach:** Start with a one-page summary of the five most important rules. Distribute this to all employees. The full policy document can be longer, but the one-page version is what people will actually remember.

---

### G-2: Risk Appetite Statement

**What it is:** A formal declaration of how much risk the organisation is willing to accept in pursuit of its business objectives.

**Why this is not optional:** Without a risk appetite statement, every security decision is made in a vacuum. The risk appetite statement allows you to:
- Prioritise which risks to address first (those exceeding appetite)
- Justify security investment to leadership (cost to reduce risk below appetite threshold)
- Make consistent decisions across the team (if risk exceeds appetite, it must be treated)

**Format:** The risk appetite statement should be simple enough that a business leader can understand and validate it. Avoid technical jargon.

**Risk appetite template:**

```
[Organisation Name] Risk Appetite Statement

Approved by: [Name, Title]
Date: [Date]
Review date: [Date + 12 months]

We are willing to accept:
□ LOW risk in: [e.g., customer data protection, financial system availability]
□ MEDIUM risk in: [e.g., internal communication systems, non-critical applications]
□ HIGH risk in: [e.g., experimental projects, non-production environments]

Specific thresholds:
- Maximum acceptable system downtime: [e.g., 4 hours for critical systems, 24 hours for non-critical]
- Maximum acceptable data exposure: [e.g., zero tolerance for customer PII breach]
- Regulatory compliance: [e.g., full compliance with LGPD required at all times]
- Financial threshold: [e.g., any risk with potential impact > R$500,000 requires board notification]
```

**Obtain formal sign-off.** The risk appetite statement must be approved by the CEO or board, not just the CISO. This creates the authority for the security programme to make binding decisions based on the stated appetite.

---

### G-3: Executive Reporting

**What it is:** A regular cadence of security status reporting to senior leadership, translated into business language.

**Why it matters:** Security teams that do not communicate with leadership operate without organisational support. Leaders cannot prioritise security investment if they do not understand the current risk posture or the trajectory of the programme.

**Reporting cadence:**
- **Monthly:** Security Score trend, top incidents, patch compliance rate, key risks above appetite
- **Quarterly:** Full S4T Assessment results, programme roadmap progress, budget vs outcomes review
- **Ad hoc:** Any P1 or P2 incident, any risk newly identified above risk appetite threshold

**Monthly executive report — one-page format:**

```
Security Programme Status — [Month Year]

Security Score: [X.XX] (▲/▼ from last month: [+/-X.XX])
Maturity Level: [Initial / Developing / Mature / Optimised]

This month:
✓ [Key accomplishment 1]
✓ [Key accomplishment 2]
⚠ [Key risk or open issue]

Incidents: [N] incidents this month ([N] resolved, [N] open)
Critical vulnerabilities: [N] open (SLA compliance: [X]%)
Patch compliance: [X]% (target: 90%)

Risks above appetite:
1. [Risk description] — Status: [Mitigating / Accepted / Transferring]

Next month priorities:
1. [Priority 1]
2. [Priority 2]
```

**Keep it to one page.** If you need more than one page, you are reporting at the wrong level of detail for an executive audience.

---

### G-4: Security Awareness Training

**What it is:** A regular programme to ensure all employees understand security threats, their responsibilities, and how to respond to incidents.

**Minimum programme requirements:**
- **Onboarding training:** Every new employee completes security awareness training within 30 days of joining
- **Annual refresh:** All employees complete refresher training annually
- **Phishing simulation:** At least two simulated phishing campaigns per year, with training triggered for employees who click
- **Incident reporting drill:** At least one simulated incident per year requiring employee reporting

**Measuring training effectiveness:**
- Training completion rate: target 100% within 30 days of due date
- Phishing click rate: track trend over time (improvement matters more than absolute value)
- Incident reports received: a rising number of employee reports often indicates growing security awareness, not more incidents

**For small organisations:** Free training resources include the SANS Security Awareness programme (free tier), Cybersecurity and Infrastructure Security Agency (CISA) resources, and the UK National Cyber Security Centre (NCSC) training materials.

---

### G-5: Regulatory Compliance Mapping

**What it is:** An explicit mapping of which regulations apply to your organisation and what controls each requires.

**Common regulations by sector:**

| Regulation | Sector | Key requirements |
|---|---|---|
| LGPD (Brazil) | All (personal data processors) | Data inventory, consent management, DPO appointment, breach notification |
| GDPR (EU) | All (EU data subjects) | Similar to LGPD, stricter breach notification (72 hours) |
| PCI-DSS | Payment card processing | Network segmentation, encryption, access control, penetration testing |
| HIPAA | US healthcare | PHI protection, access controls, audit logs, breach notification |
| Banco Central Res. 4,658/2018 | Brazilian financial services | Cybersecurity policy, penetration testing, incident reporting |
| ANS regulations | Brazilian healthcare | Patient data protection, system availability |
| ISO 27001 | All (voluntary certification) | ISMS implementation, risk management, audit |

**Mapping exercise:** For each applicable regulation, document:
1. Which specific requirements apply to your organisation
2. Which S4T controls address each requirement
3. Any gaps between current state and compliance requirements

This mapping serves two purposes: it demonstrates compliance to regulators and auditors, and it ensures regulatory requirements inform your control prioritisation in the CF layer.

---

## Measuring the G Layer

The Governance layer does not produce a direct numeric input to the Security Score formula (G does not appear explicitly in S4T = (G, RI, CF, OS, VA, L) as a state variable). Instead, G sets the parameters that determine what "good" looks like for all other layers — particularly the risk appetite thresholds that define target values for C(t), O(t), and Va(t).

**G layer maturity indicators:**

| Indicator | Initial | Developing | Mature | Optimised |
|---|---|---|---|---|
| Security policy | None | Draft, not approved | Approved, communicated | Reviewed annually, embedded in culture |
| Risk appetite | Implicit | Informally documented | Formally approved | Board-level with quantitative thresholds |
| Executive reporting | None | Ad hoc | Monthly, standardised | Real-time dashboard + monthly narrative |
| Security awareness | None | Annual training | Annual + phishing simulation | Continuous, metric-driven programme |
| Regulatory mapping | None | Partial awareness | Full mapping documented | Integrated into risk management |

---

## Common Mistakes in the G Layer

**Treating governance as a documentation exercise.** A security policy that no one reads and no one enforces is worse than no policy — it creates the illusion of control without the substance.

**Skipping the risk appetite statement.** Every organisation has an implicit risk appetite. Making it explicit allows consistent decision-making and prevents the security team from either over-investing in low-priority areas or under-investing in critical ones.

**Executive reporting in technical language.** Telling the CEO that "we detected 47 lateral movement events and patched 12 critical CVEs" communicates nothing useful. Translate: "Three systems were compromised by an attacker who accessed them without authorisation. We detected and contained the incident within 4 hours. The vulnerability used has been patched on all affected systems."

**Annual-only awareness training.** Security threats evolve continuously. Annual training is the minimum — supplement it with monthly security tips, phishing simulations, and communications about current threats relevant to your sector.

---

## Next Steps

After completing this layer:

1. Proceed to [Layer CF — Control Framework](layer-CF.md) to build your asset-based control programme on the governance foundation you have established
2. Use the risk appetite statement to guide prioritisation decisions in every subsequent layer
3. Schedule your first executive security briefing using the one-page report template above

For questions, open an issue on [GitHub](https://github.com/diegoneuber/S4T-Framework/issues) or contact [feedback@sec4.tech](mailto:feedback@sec4.tech).
