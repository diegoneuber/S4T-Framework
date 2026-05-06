# Understanding the S4T Security Score

**Audience:** CISOs, board members, and anyone who receives Security Score reports
**Reading time:** 8 minutes

---

## What the Score Measures

The S4T Security Score is a single number between 0 and 1 that captures the overall effectiveness of your cybersecurity programme at a given point in time.

It is computed from four measurable dimensions of your security posture:

| Dimension | What it captures | Example indicator |
|---|---|---|
| **Control Coverage** | Do you have the right controls in place? | 82% of assets have required controls implemented and verified |
| **Operational Maturity** | How fast do you detect and respond to threats? | Mean Time to Respond: 18 hours |
| **Validation Effectiveness** | Do your controls actually work when tested? | 73% of simulated attack techniques were detected or blocked |
| **Current Risk Level** | How much active risk are you carrying right now? | 3 critical unpatched vulnerabilities, 2 high-severity incidents this month |

These four dimensions are combined using a mathematically structured formula that ensures **no single dimension can compensate for weakness in another**. A perfect control coverage score cannot offset a validation effectiveness of zero — the framework does not allow paper security programmes to score well.

---

## The Four Maturity Levels

```
0 ────────────────────────────────────────────────────── 1
│         │                    │              │           │
0        0.40                 0.65           0.80         1
│         │                    │              │           │
Initial   Developing           Mature         Optimised
```

### Initial (< 0.40)

Your security programme is reactive. Incidents are handled as they arise. You likely have some tools in place but they are not integrated, not monitored continuously, and not tested to verify they work. You are exposed to a wide range of common attack techniques.

**What this level looks like:** Annual antivirus scans, no centralised logging, no formal incident response process, patches applied when convenient rather than on a schedule.

**Priority action:** Complete an asset inventory and deploy a SIEM (centralised log management). These two steps have the highest impact on moving from Initial to Developing.

---

### Developing (0.40 – 0.65)

You have a security programme. Basic controls are in place, monitoring exists, and someone is responsible for security outcomes. However, your controls have not been tested to confirm they detect real attacks, and your response processes are not yet mature enough to respond within business-acceptable timeframes.

**What this level looks like:** Wazuh or equivalent deployed, policies documented, some patch management in place — but no BAS testing, MTTR measured in days rather than hours, significant coverage gaps on less-visible assets.

**Priority action:** Run your first Breach and Attack Simulation campaign to discover what your controls actually detect. This single activity typically reveals gaps that no other assessment method would find.

---

### Mature (0.65 – 0.80)

You have a structured programme that continuously monitors your environment, validates your controls, and responds to incidents within operationally acceptable timeframes. Your controls have been tested and shown to detect the majority of common attack techniques. New vulnerabilities are patched within defined SLAs.

**What this level looks like:** Wazuh with tuned detection rules, weekly BAS campaigns, MTTR under 4 hours for critical incidents, 90%+ patch SLA compliance, monthly executive reporting.

**Priority action:** Focus on the Adaptive Learning layer — coefficient recalibration, post-incident reviews, and programme roadmap updates — to continue improving systematically rather than plateauing at Mature.

---

### Optimised (≥ 0.80)

Your security architecture is adaptive and largely self-correcting. Controls are continuously validated and automatically updated when gaps are identified. Incidents are detected and contained rapidly, with minimal business impact. Your programme generates evidence of its own effectiveness.

**What this level looks like:** Automated orchestration responding to BAS failures without human intervention, MTTR under 1 hour for critical incidents, > 85% BAS detection coverage, quarterly coefficient recalibration, board-level security score reporting.

**Priority action:** Sustain and extend. The primary risk at this level is programme decay — the threat landscape evolves, staff turns over, and systems change. The Adaptive Learning layer's quarterly recalibration is what prevents regression.

---

## How to Read a Score Report

A monthly Security Score report should contain at minimum:

```
Security Score — [Month Year]
──────────────────────────────────────────────────────
Overall Score:  0.72  ▲ +0.04 from last month
Maturity Level: Mature

Layer breakdown:
  G  — Governance           0.85  ████████████████████░░░░
  RI — Risk Intelligence    0.71  █████████████████░░░░░░░
  CF — Control Framework    0.80  ████████████████████░░░░
  OS — Operational Security 0.68  █████████████████░░░░░░░
  VA — Validation           0.58  ██████████████░░░░░░░░░░  ← lowest
  L  — Adaptive Learning    0.74  ██████████████████░░░░░░

Key facts:
  MTTR (this month):     22h  (target: < 4h)
  Patch SLA compliance:  88%  (target: > 90%)
  BAS detection rate:    61%  (up from 54% last month)
  Critical vulns open:    4   (down from 9 last month)

Top priority for next month:
  → VA layer: expand BAS campaign to Credential Access techniques
    (currently 0% coverage of T1003, T1078)
──────────────────────────────────────────────────────
```

**What to look for as a board member or executive:**

1. **Is the score trending upward?** Month-over-month improvement indicates a functioning programme. A flat or declining score despite investment is a signal to investigate.

2. **Which layer has the lowest score?** That is where the most risk is concentrated and where investment will have the highest return.

3. **Is MTTR decreasing?** Mean Time to Respond is the single most operationally important metric. A MTTR above 24 hours means attackers have an extended window to cause damage after initial compromise.

4. **Is BAS detection rate above 70%?** Below 70%, more than 30% of common attack techniques go undetected by your controls. This is significant operational risk regardless of how good other metrics look.

---

## What the Score Does Not Capture

The Security Score is a powerful tool, but it is important to understand its boundaries.

**It does not guarantee you will not be breached.** An Optimised score (0.80+) means your programme is structured, validated, and continuously improving — not that you are invulnerable. Sophisticated, well-resourced attackers can compromise even mature security programmes.

**It reflects your programme, not your vendors' security.** If a SaaS provider you depend on is breached, your Security Score does not capture that risk. Third-party risk management (part of the RI layer) addresses this, but the score itself is an internal measure.

**It is only as honest as the data feeding it.** A score computed from self-reported questionnaire answers is less reliable than one computed from automated system data (Wazuh dashboards, BAS platform results, vulnerability scanner outputs). As your programme matures, aim to replace questionnaire-based inputs with automated data sources.

**The Va(t) component is the most important honesty check.** Validation effectiveness cannot be fabricated — it comes from a simulated attack campaign that either detected or did not detect each technique. If your Va(t) is low, your score reflects that accurately regardless of what other metrics show.

---

## Using the Score for Decision Making

### Prioritising investment

The layer breakdown shows which capability areas contribute most to your current score gap. Investment directed at your lowest-scoring layer typically yields the highest return per unit of spend.

**Example:** Organisation with overall score 0.58 and layer breakdown showing VA at 0.25. The score formula's geometric mean structure means that Va(t) = 0.25 is suppressing the overall score significantly more than other layers. Investment in a BAS programme (VA layer) will yield a larger score improvement per dollar than the same investment directed at an already-strong Governance layer.

### Communicating risk to leadership

The Security Score provides a language for communicating risk that does not require technical expertise to understand:

- "Our score is 0.48 — we are in the Developing tier. Our target for this financial year is 0.65, which requires improving our Validation layer from 0.25 to 0.60."
- "Our MTTR is 22 hours. If an attacker achieves initial access today, they have 22 hours of undetected activity before we typically respond."
- "Our BAS detection rate is 61%. This means roughly 4 in 10 attack techniques commonly used against our sector would not be detected by our current controls."

### Setting programme targets

Use the score trajectory to set programme milestones with leadership accountability:

| Timeline | Target | Owner | Investment required |
|---|---|---|---|
| Q2 2025 | Score 0.55 (top of Developing) | CISO | BAS platform setup, VA layer |
| Q4 2025 | Score 0.65 (Mature threshold) | CISO + IT | Full OS layer deployment |
| Q2 2026 | Score 0.72 (mid-Mature) | CISO | Automated orchestration, L layer maturation |

---

## Frequently Asked Questions

**"How does our score compare to industry peers?"**
The S4T Assessment Tool aggregates anonymous scores across all assessments. As the dataset grows, industry benchmarks by sector will be published. Currently, the Mature threshold (0.65) represents a programme that detects and responds to the majority of common attacks — a reasonable target for any organisation handling sensitive data.

**"Can the score be gamed?"**
The geometric mean structure of the formula makes gaming difficult. Inflating one dimension does not materially improve the overall score if other dimensions are weak. The Va(t) component — which comes from actual attack simulation results — is particularly resistant to gaming because it reflects real detection capability, not documented capability.

**"How often should we report the score to the board?"**
Quarterly is the recommended cadence for board-level reporting. Monthly reporting is appropriate for the CISO and relevant executives. Ad hoc reporting should occur for any significant score change (> ±0.05 in a month) or for any P1 security incident.

**"What is a realistic improvement rate?"**
From the validation study: organisations starting at Initial level improved by approximately 0.10–0.15 points in the first six months, and a further 0.10–0.20 points in months 6–18. Improvement rate typically slows as score increases — going from 0.30 to 0.50 is faster than going from 0.70 to 0.80.

---

*For the technical methodology behind the Security Score, see the [score calculation guide](../for-practitioners/score-calculation.md) or the [academic papers](../reference/papers.md).*
