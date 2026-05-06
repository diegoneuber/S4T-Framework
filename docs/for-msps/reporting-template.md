# S4T Monthly Client Report — Template

**Purpose:** Monthly security programme status report delivered by MSP to client
**Frequency:** Monthly, within 5 business days of month end
**Audience:** Client CISO, CIO, or executive sponsor

---

## How to Use This Template

1. Copy this template into your reporting tool (Word, Google Docs, or PDF generator)
2. Replace all `[bracketed values]` with actual client data
3. Generate the Security Score using the Assessment Tool or manual calculation
4. Review with your internal team before sending
5. Deliver by email with the share link from the Assessment Tool if a new assessment was run this month

**Reporting cadence:**
- **Monthly:** Full report using this template
- **Quarterly:** This report + the programme roadmap review
- **Annual:** This report + full year summary + Year 2 roadmap

---

# [Client Organisation Name]
## Security Programme Report — [Month Year]

**Prepared by:** [MSP Name]
**Analyst:** [Name]
**Delivery date:** [Date]
**Report period:** [First day of month] – [Last day of month]
**Next report:** [Date]

---

## Security Score Summary

```
┌─────────────────────────────────────────────────────┐
│  SECURITY SCORE                                      │
│                                                      │
│  Current:   [X.XX]   ▲/▼ [+/-X.XX] from last month │
│  Level:     [Initial / Developing / Mature /         │
│              Optimised]                              │
│                                                      │
│  12-month target:  [X.XX]  (on track / at risk)     │
│  Months to target: [N]                               │
└─────────────────────────────────────────────────────┘
```

**Score trend (last 6 months):**

| Month | Score | Level | Change |
|---|---|---|---|
| [Month -5] | [X.XX] | | |
| [Month -4] | [X.XX] | | |
| [Month -3] | [X.XX] | | |
| [Month -2] | [X.XX] | | |
| [Month -1] | [X.XX] | | ▲/▼ |
| **[Current month]** | **[X.XX]** | | **▲/▼ [+/-X.XX]** |

---

## Layer Breakdown

| Layer | Score | vs. Last Month | Status |
|---|---|---|---|
| G — Governance | [X.XX] | [▲/▼/→] [+/-X.XX] | [🟢 On track / 🟡 Monitor / 🔴 Action needed] |
| RI — Risk Intelligence | [X.XX] | [▲/▼/→] | |
| CF — Control Framework | [X.XX] | [▲/▼/→] | |
| OS — Operational Security | [X.XX] | [▲/▼/→] | |
| VA — Validation & Assurance | [X.XX] | [▲/▼/→] | |
| L — Adaptive Learning | [X.XX] | [▲/▼/→] | |

**Lowest scoring layer this month:** [Layer name] at [X.XX]
**Recommended focus for next month:** [One-sentence action]

---

## Key Metrics

### Operational Security (OS Layer)

| Metric | This Month | Last Month | Target | Status |
|---|---|---|---|---|
| Mean Time to Respond (MTTR) | [X]h | [X]h | < 4h | [🟢/🟡/🔴] |
| Incidents — P1 (Critical) | [N] | [N] | 0 | [🟢/🔴] |
| Incidents — P2 (High) | [N] | [N] | < 2 | [🟢/🟡/🔴] |
| Incidents — P3 (Medium) | [N] | [N] | < 10 | [🟢/🟡/🔴] |
| Wazuh agent coverage | [X]% | [X]% | 100% | [🟢/🟡/🔴] |

### Risk Intelligence (RI Layer)

| Metric | This Month | Last Month | Target | Status |
|---|---|---|---|---|
| Critical vulnerabilities open | [N] | [N] | < 5 | [🟢/🟡/🔴] |
| High vulnerabilities open | [N] | [N] | < 20 | [🟢/🟡/🔴] |
| Patch SLA compliance — Critical | [X]% | [X]% | > 90% | [🟢/🟡/🔴] |
| Patch SLA compliance — High | [X]% | [X]% | > 90% | [🟢/🟡/🔴] |
| New CVEs affecting environment | [N] | [N] | N/A | Info |
| CISA KEV entries patched (if any) | [N/A or N of N] | | 100% | [🟢/🔴] |

### Control Framework (CF Layer)

| Metric | This Month | Last Month | Target | Status |
|---|---|---|---|---|
| Asset inventory completeness | [X]% | [X]% | > 95% | [🟢/🟡/🔴] |
| High-criticality assets — full control coverage | [X]% | [X]% | 100% | [🟢/🟡/🔴] |
| MFA coverage — remote access | [X]% | [X]% | 100% | [🟢/🟡/🔴] |
| MFA coverage — privileged accounts | [X]% | [X]% | 100% | [🟢/🟡/🔴] |

### Validation (VA Layer)

| Metric | This Month | Last Month | Target | Status |
|---|---|---|---|---|
| BAS campaigns run | [N] | [N] | ≥ 1 | [🟢/🔴] |
| ATT&CK techniques tested | [N] | [N] | N/A | Info |
| Detection rate (Va(t)) | [X]% | [X]% | > 70% | [🟢/🟡/🔴] |
| New gaps identified | [N] | | N/A | Info |
| Gaps from last month — resolved | [N of N] | | 100% | [🟢/🟡/🔴] |

---

## Incidents This Month

*[If no incidents: "No security incidents were recorded during this period."]*

### [INC-XXXX] — [Incident title]

| | |
|---|---|
| **Severity** | [P1 / P2 / P3] |
| **Date detected** | [Date] |
| **Date resolved** | [Date] |
| **MTTR** | [X hours] |
| **Systems affected** | [Description] |
| **Root cause** | [Brief description] |
| **Resolution** | [What was done] |
| **Recurrence prevention** | [Control or process change implemented] |

---

## Vulnerabilities — Open Items

*Top 5 open vulnerabilities by priority (see full list in vulnerability register):*

| # | CVE | CVSS | System | Days open | SLA | Status |
|---|---|---|---|---|---|---|
| 1 | [CVE-XXXX-XXXXX] | [X.X] | [hostname] | [N] | [date] | [Scheduled / In progress] |
| 2 | | | | | | |
| 3 | | | | | | |
| 4 | | | | | | |
| 5 | | | | | | |

**Vulnerabilities resolved this month:** [N] (SLA compliance: [X]%)

---

## BAS Campaign Results

*[If no BAS campaign run this month: "No BAS campaign was scheduled for this period. Next campaign: [date]."]*

**Campaign date:** [Date]
**Platform:** [Caldera / Atomic Red Team / Other]
**ATT&CK tactics covered:** [List]

| ATT&CK Tactic | Techniques Tested | Detected | Blocked | Not Detected |
|---|---|---|---|---|
| Initial Access | [N] | [N] | [N] | [N] |
| Execution | [N] | [N] | [N] | [N] |
| Persistence | [N] | [N] | [N] | [N] |
| Privilege Escalation | [N] | [N] | [N] | [N] |
| Lateral Movement | [N] | [N] | [N] | [N] |
| **Total** | **[N]** | **[N]** | **[N]** | **[N]** |

**Overall detection rate:** [X]% (Va(t) = [X.XX])

**New gaps identified (techniques not detected):**
1. [ATT&CK ID] — [Technique name] — Remediation: [Action] — Owner: [Name] — Due: [Date]
2. [ATT&CK ID] — [Technique name] — ...

**Gaps resolved from previous campaign:**
- [ATT&CK ID] — [Technique name] — Verified detected ✓

---

## Accomplishments This Month

*3–5 specific accomplishments, tied to framework layer improvements:*

1. ✅ [Accomplishment] — Layer: [G/RI/CF/OS/VA/L] — Score impact: [+X.XX on layer score]
2. ✅ [Accomplishment] — Layer: [G/RI/CF/OS/VA/L]
3. ✅ [Accomplishment]

---

## Open Risks Above Risk Appetite

*Risks currently exceeding the client's stated risk appetite. Each should have a defined treatment plan:*

| Risk | Current Level | Appetite | Treatment | Owner | Due Date |
|---|---|---|---|---|---|
| [Risk description] | High | Medium | Mitigating: [Action] | [Name] | [Date] |
| [Risk description] | | | | | |

*[If no risks above appetite: "No risks are currently identified above the organisation's stated risk appetite."]*

---

## Priorities for Next Month

| # | Priority | Layer | Owner | Expected outcome |
|---|---|---|---|---|
| 1 | [Action] | [Layer] | [MSP / Client] | [Score or metric impact] |
| 2 | [Action] | | | |
| 3 | [Action] | | | |

**Scheduled activities next month:**
- [ ] BAS campaign — [planned date]
- [ ] Vulnerability scan — [planned date]
- [ ] Quarterly review — [planned date, if applicable]
- [ ] Penetration test — [planned date, if applicable this quarter]

---

## Programme Health Summary

```
Overall programme health: [🟢 On track / 🟡 Monitor / 🔴 Action needed]

Score trajectory:  [🟢 Improving / 🟡 Stable / 🔴 Declining]
Incident trend:    [🟢 Decreasing / 🟡 Stable / 🔴 Increasing]
Patch compliance:  [🟢 > 90% / 🟡 80–90% / 🔴 < 80%]
Validation:        [🟢 > 70% / 🟡 50–70% / 🔴 < 50%]
12-month target:   [🟢 On track / 🟡 At risk / 🔴 Off track]
```

**MSP summary comment:**
*[2–3 sentences: what happened this month, what it means for the programme, and what to watch next month. Written for a non-technical reader.]*

*Example: "This month's Security Score improvement of +0.05 reflects the successful deployment of automated patch management, which brought your patch SLA compliance from 71% to 89%. The primary remaining gap is in the Validation layer — your BAS detection rate of 48% means roughly half of common attack techniques go undetected. Next month's priority is expanding BAS coverage to credential-access techniques, which are the most common initial access vector in incidents affecting your sector."*

---

## Contact and Escalation

| | |
|---|---|
| **MSP account manager** | [Name] · [email] · [phone] |
| **MSP security lead** | [Name] · [email] · [phone] |
| **Emergency / P1 incident** | [24/7 contact] |
| **Client security contact** | [Name] · [email] · [phone] |
| **Next scheduled call** | [Date and time] |

---

*Report generated using the S4T Framework assessment methodology. Security Score computed per: Neuber, D. (2024). S4T Framework v3.0. [doi.org/10.13140/RG.2.2.16699.58408](https://doi.org/10.13140/RG.2.2.16699.58408)*

---

**[MSP Logo / Name]** · Confidential — for [Client Name] only · [Date]
