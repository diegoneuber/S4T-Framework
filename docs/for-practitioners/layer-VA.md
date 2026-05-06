# Layer VA — Validation & Assurance

**Position in the framework:** S4T = (G, RI, CF, OS, **VA**, L)
**Drives:** Va(t) — Validation Effectiveness Score
**Primary metric:** Proportion of BAS test cases successfully detected or blocked

---

## What This Layer Does

Validation is the layer that most organisations skip — and the gap it leaves is critical. You can have a documented security policy, a complete asset inventory, a deployed SIEM, and a full set of controls, and still have no idea whether any of it actually works. Va(t) answers that question with evidence.

In the S4T risk evolution equation:

```
dR/dt = δT(t) − αC(t) − βO(t) − γVa(t)
```

Va(t) is the Validation Effectiveness Score — the proportion of simulated attack techniques your controls successfully detected or blocked. An organisation with C(t) = 0.80 (strong control coverage) and Va(t) = 0.10 (controls not validated) has a paper programme, not a real one. The Security Score formula's geometric mean structure ensures that a near-zero Va(t) dramatically suppresses the overall score regardless of how good other metrics are.

**Va(t) is the layer that makes the Security Score honest.**

The primary mechanism for computing Va(t) is **Breach and Attack Simulation (BAS)** — automated, continuous testing of your controls against real attack techniques mapped to the MITRE ATT&CK framework. BAS replaces the traditional model of annual penetration tests with continuous, automated validation.

---

## Prerequisites

Before implementing this layer, you should have:
- [ ] Wazuh deployed and tuned (from OS layer) — you need a detection platform before you can test it
- [ ] At least 30 days of SIEM operation (alert tuning completed)
- [ ] Asset inventory (from CF layer) — you need to know what systems to test
- [ ] Written authorisation for testing — even internal BAS campaigns require documented approval to avoid legal or operational issues

---

## VA Layer Components

### VA-1: Breach and Attack Simulation (BAS)

**What it is:** Automated, repeatable execution of attack techniques from the MITRE ATT&CK framework against your own environment, with the purpose of measuring whether your detection and prevention controls are effective.

**BAS is not a penetration test.** A penetration test is a point-in-time engagement performed by humans. BAS is continuous, automated, and designed to run weekly or daily. The two complement each other — BAS provides continuous coverage measurement, penetration testing provides adversarial creativity and deeper exploitation validation.

**Reference implementations:**

| Tool | Description | Licence |
|---|---|---|
| [MITRE Caldera](https://caldera.mitre.org/) | Full-featured BAS platform with MITRE ATT&CK coverage | Open source (Apache 2.0) |
| [Atomic Red Team](https://atomicredteam.io/) | Library of atomic test cases mapped to ATT&CK | Open source (MIT) |
| [OpenBAS](https://openbas.io/) | Open BAS platform by Filigran (creators of OpenCTI) | Open source |

**Recommended starting point:** Atomic Red Team with manual execution, then migrate to Caldera for automation once you understand the test cases.

**BAS deployment — step by step:**

**Step 1: Set up a test environment.** Do not run BAS directly in production without preparation. Set up a dedicated test network (or isolated VLAN) that mirrors your production environment as closely as possible. This allows you to run aggressive tests without risk of business disruption.

**Step 2: Baseline your current detection rate before making any changes.** Run your first BAS campaign before tuning Wazuh based on results. This gives you Va(0) — your true starting point.

**Step 3: Select your initial ATT&CK technique coverage.** Start with the ATT&CK techniques most commonly used in attacks against your sector. The MITRE ATT&CK Navigator ([attack.mitre.org/navigator](https://attack.mitre.org/navigator/)) allows you to filter by sector and visualise coverage.

**Priority techniques for most organisations (Initial Tier):**

| ATT&CK ID | Technique | Why it matters |
|---|---|---|
| T1078 | Valid Accounts | Credential abuse is in virtually every breach |
| T1059 | Command and Scripting Interpreter | PowerShell/bash abuse for lateral movement |
| T1486 | Data Encrypted for Impact | Ransomware |
| T1003 | OS Credential Dumping | Mimikatz and similar — credential theft |
| T1021 | Remote Services | RDP/SMB lateral movement |
| T1070 | Indicator Removal | Attackers clearing logs |
| T1105 | Ingress Tool Transfer | Downloading attack tools to target |
| T1566 | Phishing | Initial access via email |

**Step 4: Execute tests and measure results.** For each technique tested, record:
- Was the technique detected by Wazuh? (Yes / No / Partial)
- If detected, how quickly? (Time from execution to alert)
- If not detected, why not? (No rule, rule disabled, agent not running)

**Step 5: Tune your controls based on results.** Each failed detection is a finding. For each one:
1. Determine why it was not detected (missing Wazuh rule, log source not configured, agent offline)
2. Implement the fix (add rule, configure log source, restore agent connectivity)
3. Re-run the test to confirm detection now works
4. Document the improvement

**Step 6: Automate and run continuously.** Once you have a working test set and your Wazuh is tuned to detect them, automate BAS execution weekly using Caldera's scheduling. Weekly BAS runs ensure that new deployments, configuration changes, and updates have not broken existing detection rules.

---

### VA-2: Penetration Testing

**What it is:** A point-in-time, human-led assessment of your defences by a skilled adversary (internal or external) attempting to compromise your systems.

**BAS and penetration testing are complementary, not competing:**

| | BAS | Penetration Test |
|---|---|---|
| Frequency | Continuous / weekly | Annual minimum |
| Coverage | Known ATT&CK techniques | Creative adversarial exploration |
| Cost | Near-zero (open source) | Significant (external engagement) |
| Value | Continuous coverage verification | Adversarial creativity, chained exploits |
| Output | Coverage %, per-technique results | Narrative report, PoC exploits |

**S4T penetration testing requirements:**

- **Frequency:** Annual minimum; twice annually for regulated environments or internet-exposed applications
- **Scope minimum:** External perimeter (all internet-exposed services), internal network (from assumed-compromised workstation), social engineering (phishing simulation)
- **Findings integration:** All penetration test findings must be tracked in your vulnerability register with remediation SLAs assigned
- **Retest:** Critical and High findings should be retested after remediation to confirm they are resolved

**Selecting a penetration testing provider:** Request evidence of OSCP, CEH, or equivalent certification. Require a statement of work specifying scope, rules of engagement, and deliverables before engagement begins.

**For smaller organisations:** Consider purple team exercises as a cost-effective alternative — internal security team works collaboratively with an external red team, learning detection techniques in real time. More educational value than a black-box test, often at lower cost.

---

### VA-3: Continuous Control Monitoring

**What it is:** Automated, ongoing verification that your controls are operating as intended — not just that they are installed, but that they are actually running and producing results.

**The control monitoring checklist (verify weekly):**

| Control | Monitoring check |
|---|---|
| Wazuh agents | All agents show "Active" status in dashboard |
| Wazuh rules | Rule count unchanged from baseline (unexpected rule deletion = alert) |
| Log ingestion | Log volume within expected range (sudden drop = collection failure) |
| Backup jobs | Last successful backup < 24 hours ago |
| Patch compliance | No Critical CVEs > 24 hours unpatched |
| Certificate expiry | No TLS certificates expiring within 30 days |
| Firewall rules | Rule count and critical rules unchanged (compare against baseline) |
| MFA | No accounts with MFA disabled that should have it enabled |

**Automate where possible.** Wazuh can alert on many of these automatically — agent offline, log volume drops, specific rule matches. The goal is to eliminate manual weekly checks by converting them to automated alerts.

---

### VA-4: Vulnerability Remediation Validation

**What it is:** Confirming that vulnerabilities are actually fixed after patches are applied — not just that the patch was installed.

**Why this matters:** Patches sometimes fail silently. A package may report as updated but still run the vulnerable version. A configuration fix may not apply correctly. Without validation, your vulnerability SLA compliance rate measures patch attempts, not patch success.

**Remediation validation process:**

1. **Wazuh vulnerability scan after patching:** After applying a patch for a critical CVE, wait 24 hours and re-run Wazuh's vulnerability scan on the affected system. Confirm the CVE no longer appears.

2. **For web application vulnerabilities:** Re-run the specific scan that identified the vulnerability (e.g., a DAST tool or manual test) after remediation.

3. **For configuration findings:** Re-run CIS-CAT or the specific CIS Benchmark check that identified the finding.

4. **For penetration test findings:** Retest findings marked as remediated before closing them in your tracking system.

---

## Measuring Va(t)

Va(t) — Validation Effectiveness Score — is the proportion of BAS test cases successfully detected or blocked, stratified by ATT&CK tactic.

**Calculation:**

```
Va(t) = (Techniques Detected or Blocked) / (Total Techniques Tested)
```

For more precision, weight by ATT&CK tactic severity (Initial Access and Execution techniques are more critical than Exfiltration for most organisations).

**Va(t) benchmarks from the validation study:**

| Va(t) value | Interpretation |
|---|---|
| 0.00 – 0.15 | No meaningful validation in place; controls are unverified |
| 0.15 – 0.40 | Basic detection capability; significant blind spots |
| 0.40 – 0.70 | Developing validation programme; most major techniques covered |
| 0.70 – 0.85 | Strong validation; systematic coverage with active improvement |
| 0.85 – 1.00 | Mature continuous validation; optimised detection and response |

**Most organisations on first BAS run:** Va(t) ≈ 0.10 – 0.25. This is expected and not a failure — it is the accurate baseline that the rest of your improvement will be measured against.

**Monthly Va(t) tracking:**

| Month | Techniques Tested | Detected | Blocked | Va(t) | Notes |
|---|---|---|---|---|---|
| Baseline | | | | | First BAS campaign |
| Month 3 | | | | | After initial tuning |
| Month 6 | | | | | After Orchestration integration |
| Month 12 | | | | | End of first year |

---

## Integration: VA → Orchestration → OS

The most powerful use of the VA layer is closing the loop to automated response. When BAS identifies a failed detection:

1. **BAS test fails** (technique not detected by Wazuh)
2. **Security engineer reviews** the failure and determines the missing detection rule
3. **Rule is added to Wazuh** (manually, or via Shuffle SOAR if automated)
4. **BAS re-runs** to confirm detection now works
5. **Orchestration layer** can automatically create patch tickets or firewall rule updates when BAS identifies exploitable vulnerabilities

This feedback loop — VA detecting gaps, OS controls being improved, VA confirming the improvement — is the core of S4T's adaptive architecture and what distinguishes it from compliance-oriented frameworks.

---

## Common Mistakes in the VA Layer

**Running BAS in production without preparation.** Some BAS techniques can disrupt services or trigger incident responses. Always test in an isolated environment first, and obtain written authorisation before running in production.

**Treating first BAS results as a failure.** Va(0) ≈ 0.15 is typical and expected. The first BAS campaign is a diagnostic, not a performance review.

**Annual penetration tests without continuous BAS.** An annual penetration test tells you your posture on one specific day. BAS tells you continuously. Both are needed.

**Closing BAS findings without retesting.** A finding is not resolved until the test confirms it. "We applied the fix" is not evidence; a passing BAS test is.

**Not integrating VA results into the Adaptive Learning layer.** BAS results are among the most valuable inputs to the L layer. Track Va(t) trends and use them to drive your quarterly recalibration.

---

## Next Steps

After completing this layer:

1. Your Va(t) is now established — track it weekly alongside BAS execution
2. Proceed to [Layer L — Adaptive Learning](layer-L.md) to close the feedback loop and drive continuous improvement
3. Schedule your first external penetration test if not already planned

For questions, open an issue on [GitHub](https://github.com/diegoneuber/S4T-Framework/issues) or contact [feedback@sec4.tech](mailto:feedback@sec4.tech).
