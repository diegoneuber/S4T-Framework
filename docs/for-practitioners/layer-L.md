# Layer L — Adaptive Learning

**Position in the framework:** S4T = (G, RI, CF, OS, VA, **L**)
**Drives:** System recalibration, coefficient update, and continuous improvement
**Primary output:** Quarterly model recalibration, updated Security Score trajectory

---

## What This Layer Does

Adaptive Learning is what transforms S4T from a one-time implementation into a continuously improving system. Every other layer generates data — C(t) from control coverage, O(t) from operational metrics, Va(t) from BAS results, T(t) from threat intelligence. The L layer aggregates that data, identifies trends, and adjusts the programme accordingly.

Without Adaptive Learning, a security programme plateaus. You implement controls, reach a steady state, and stop improving — because there is no mechanism to identify what is working, what is not, and what needs to change. L provides that mechanism.

**The L layer operates the Monitor–Analyse–Act–Learn cycle at four cadences:**

| Cadence | Activity |
|---|---|
| **Continuous** | Metric collection from all layers |
| **Monthly** | Security Score calculation and trend analysis |
| **Quarterly** | Coefficient recalibration and strategic review |
| **Annual** | Programme roadmap update and full assessment |

---

## Prerequisites

Before this layer is meaningful, you should have:
- [ ] At least 90 days of operational data from OS layer (Wazuh metrics)
- [ ] At least one BAS campaign completed (Va(t) baseline from VA layer)
- [ ] Monthly Security Score tracking established
- [ ] Executive reporting cadence in place (from G layer)

The L layer cannot function without data from the other five layers. If you are implementing S4T for the first time, L layer activities begin at month 3 and become increasingly meaningful as your data history grows.

---

## L Layer Components

### L-1: Security Metrics Programme

**What it is:** A defined set of metrics collected consistently over time, enabling trend analysis and evidence-based decision making.

**S4T core KPI set:**

| KPI | Source | Frequency | Target |
|---|---|---|---|
| Security Score S(t) | Assessment Tool / Manual calculation | Monthly | Improving trend; Level-specific targets |
| Control Coverage C(t) | CF layer (asset × control matrix) | Monthly | > 0.80 for High criticality assets |
| MTTR (hours) | OS layer (Wazuh incident tickets) | Monthly | < 4h for P1/P2, < 24h for P3 |
| Validation Effectiveness Va(t) | VA layer (BAS results) | Monthly (after each BAS run) | > 0.70 |
| Patch SLA Compliance | OS layer (vulnerability register) | Monthly | > 90% for Critical/High |
| Critical Vulnerabilities Open | RI + OS layer | Weekly | < 5 at any time |
| MFA Coverage | G + OS layer (IAM audit) | Monthly | 100% for remote/privileged access |
| Training Completion Rate | G layer | Quarterly | 100% within 30 days of due date |
| Agent Coverage | OS layer (Wazuh Dashboard) | Weekly | 100% of in-scope endpoints |

**Metric collection discipline matters more than dashboard sophistication.** A simple spreadsheet updated monthly is more valuable than a complex dashboard that is never updated. Start simple, automate over time.

**Monthly KPI tracking template:**

```
Month: [Month Year]
Collected by: [Name]
Review date: [Date]

Security Score: [X.XX] (prev: [X.XX], Δ: [+/-X.XX])
Maturity level: [Initial / Developing / Mature / Optimised]

Layer metrics:
G: Training completion [X]% | Policy reviewed: [Y/N]
RI: Vuln SLA compliance [X]% | Critical vulns open: [N]
CF: Control coverage [X]% | Assets without full coverage: [N]
OS: MTTR [Xh] | Incidents this month: [N] P1, [N] P2, [N] P3
VA: Va(t) [X.XX] | BAS campaign run: [Y/N] | Techniques tested: [N]
L: [Notes on trends and anomalies]

Notable changes from last month:
-
-

Actions for next month:
-
-
```

---

### L-2: Post-Incident Review

**What it is:** A structured process to extract learnings from every security incident and incorporate them into programme improvements.

**Why this is non-optional:** Incidents are the most valuable source of programme improvement data you have. Every incident reveals a gap — in detection, in response, in controls, in process. An organisation that runs post-incident reviews systematically improves faster than one that resolves incidents and moves on.

**Post-incident review should happen for every P1 and P2 incident, and for any P3 incident with unusual characteristics.**

**Post-incident review template:**

```
Incident ID: [INC-XXXX]
Severity: [P1 / P2 / P3]
Date: [Date of incident]
Date of review: [Date, ideally within 5 business days of resolution]
Participants: [Names / roles]

INCIDENT SUMMARY
What happened? (2-3 sentences, factual)

TIMELINE
[Time] — [Event]
[Time] — [Detection]
[Time] — [Response action]
[Time] — [Containment]
[Time] — [Resolution]

IMPACT
Systems affected:
Data affected:
Business impact:
Total downtime (if applicable):

ROOT CAUSE ANALYSIS
Primary cause:
Contributing factors:

WHAT WORKED
(Detection, response, communication, tooling)

WHAT DID NOT WORK
(What slowed the response? What was missing?)

LESSONS LEARNED AND ACTION ITEMS
| Finding | Action | Owner | Due date |
|---|---|---|---|
| | | | |

RECURRENCE PREVENTION
Has the root cause been permanently remediated? [Y/N]
If no, what is the plan?
```

**Lessons learned repository:** Maintain a shared repository (Git, Confluence, SharePoint) of all post-incident reviews. Before responding to a new incident, check whether you have seen something similar before. Pattern recognition across incidents reveals systemic weaknesses that individual reviews might miss.

---

### L-3: Security Programme Roadmap

**What it is:** A 12-month plan for your security programme, updated quarterly, with specific milestones tied to Security Score targets.

**Why a written roadmap matters:** Security improvements compete with other IT and business priorities for budget, time, and attention. A written roadmap makes the programme visible to leadership, enables resource planning, and provides a baseline against which progress can be measured.

**Roadmap structure:**

```
S4T Programme Roadmap — [Year]
Organisation: [Name]
Current Security Score: [X.XX]
12-month target: [X.XX]

Q1 Objectives:
□ [Milestone 1] — Owner: [Name] — Target score impact: [+X.XX on C(t)]
□ [Milestone 2]
□ [Milestone 3]

Q2 Objectives:
□ [Milestone 1]
□ [Milestone 2]

Q3 Objectives:
□ [Milestone 1]
□ [Milestone 2]

Q4 Objectives:
□ [Milestone 1]
□ [Milestone 2]

Budget requirements:
[Tool/service] — [Cost] — [Layer] — [Expected score impact]

Key risks to plan:
[Risk] — [Mitigation]
```

**Setting realistic targets:** Based on the validation study, typical Security Score improvement trajectories:
- Starting at 0.25–0.35 (Initial): reach 0.50–0.60 in 12 months with consistent effort
- Starting at 0.40–0.55 (Developing): reach 0.65–0.75 in 12 months
- Starting at 0.60–0.70 (Mature): reach 0.75–0.82 in 12 months

Improvement slows as score increases — the marginal effort required to go from 0.35 to 0.50 is less than from 0.75 to 0.82.

---

### L-4: Coefficient Recalibration

**What it is:** Quarterly update of the α, β, γ, δ coefficients in the risk evolution equation based on observed performance data from your specific environment.

**The risk evolution equation:**
```
dR/dt = δT(t) − αC(t) − βO(t) − γVa(t)
```

**Default cross-sector coefficients (derived from the 18-month validation study):**
```
α = 0.35 (Control Coverage weight)
β = 0.25 (Operational Maturity weight)
γ = 0.30 (Validation Effectiveness weight)
δ = 0.10 (Threat Exposure weight)
```

**When to adjust coefficients:**

The default coefficients are calibrated for a general organisational context. Your environment may differ:
- **High threat exposure sector** (financial services, healthcare): increase δ (threat weight)
- **Compliance-heavy environment** (regulated financial institution): increase α (control coverage weight) to reflect that controls drive your risk exposure most
- **Mature detection team** (dedicated SOC): increase β (operational maturity weight) if your team's response speed is your primary differentiator

**Recalibration process (Phase 2 from the academic paper):**

After 90+ days of data, you can estimate your organisation-specific coefficients using OLS regression on your observed R(t) approximations:

1. Collect monthly observations of C(t), O(t), Va(t), and T(t) from your metrics programme
2. Estimate R(t) from your incident data: `R(t) ≈ (Critical incidents × 1.0) + (High incidents × 0.5) + (Critical vulns × 0.3)` — normalise to [0,1]
3. Fit the discretised equation: `ΔR = δΔT − αΔC − βΔO − γΔVa` using OLS regression
4. Use resulting coefficients as your organisation-specific values

For most organisations implementing S4T for the first time, the default coefficients are appropriate for the first 12 months. Recalibration becomes meaningful after 6+ months of data.

---

### L-5: Threat Model Updates

**What it is:** Quarterly review of your threat model — the set of adversaries, techniques, and scenarios most likely to affect your organisation — to ensure your controls and detection rules remain relevant as the threat landscape evolves.

**Threat model update process:**

1. **Review MITRE ATT&CK for changes:** ATT&CK is updated semi-annually. Review new techniques and sub-techniques for relevance to your environment.

2. **Review sector-specific threat reports:** Annual and quarterly threat intelligence reports for your sector (e.g., Verizon DBIR, IBM X-Force Report, CrowdStrike Global Threat Report) identify which threat actors and techniques are most active in your industry.

3. **Review your own incident history:** What techniques were used in incidents against your organisation in the past year? These are your highest-priority detection gaps.

4. **Update your BAS campaign:** Add new relevant ATT&CK techniques to your BAS coverage. Remove techniques that are no longer relevant to your environment.

5. **Update Wazuh rules:** Ensure your SIEM detection rules cover newly identified relevant techniques.

---

## The Feedback Loop in Practice

The L layer closes the loop that makes S4T a continuously improving system. Here is how the cycle operates in practice:

```
VA runs BAS campaign
    → Technique not detected (Va(t) gap identified)
        → L layer records gap in post-incident register
        → OS layer adds Wazuh detection rule
        → VA reruns test → now detected
        → C(t) and Va(t) both improve
        → Security Score rises
        → L layer records improvement in monthly metrics
        → Quarterly recalibration adjusts weights if pattern observed
        → Roadmap updated with next priority gap
```

This cycle — operating continuously across all six layers — is what the paper describes as the "Monitor–Analyse–Act–Learn" loop and what distinguishes S4T from compliance frameworks that run the cycle annually at best.

---

## Common Mistakes in the L Layer

**Collecting metrics but not acting on them.** Data without decisions is noise. Every monthly review should produce at least one action item.

**Treating the Security Score as the goal rather than the indicator.** Optimising for the score without improving the underlying security posture is Goodhart's Law applied to cybersecurity. Focus on the activities; the score will follow.

**Skipping post-incident reviews for "small" incidents.** P3 incidents often reveal systemic weaknesses. A recurring P3 issue that is never reviewed is a P1 waiting to happen.

**No written roadmap.** Without a written plan, the security programme responds only to immediate incidents. A roadmap ensures proactive improvement continues even when operations are demanding.

**Waiting for perfect data before recalibrating.** Six months of imperfect but consistent data is enough to begin coefficient recalibration. Waiting for perfect data means waiting forever.

---

## Next Steps

With all six layers implemented, your S4T programme is operational. What comes next:

1. **Month 3:** First quarterly review — how does your Score compare to baseline? What are the top three gaps?
2. **Month 6:** First coefficient recalibration attempt — do you have enough data?
3. **Month 12:** Full programme review — compare current Score to starting point, update 12-month roadmap
4. **Ongoing:** Contribute your learnings back to the S4T community via [GitHub Issues](https://github.com/diegoneuber/S4T-Framework/issues) or [feedback@sec4.tech](mailto:feedback@sec4.tech)

If you are an MSP delivering S4T to clients, see [for-msps/service-delivery.md](../for-msps/service-delivery.md) for guidance on structuring client-facing L layer reporting.
