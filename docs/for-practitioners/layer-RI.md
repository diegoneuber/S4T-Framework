# Layer RI — Risk Intelligence

**Position in the framework:** S4T = (G, **RI**, CF, OS, VA, L)
**Drives:** T(t) — Threat Exposure and Growth Rate (inverse: reduces T(t) by enabling proactive response)
**Primary output:** Contextualised threat intelligence informing control prioritisation

---

## What This Layer Does

Risk Intelligence is the layer that keeps your security programme connected to the real world. Without it, you are defending against a static, historical picture of the threat landscape. With it, your controls are continuously informed by what attackers are actually doing — right now, in your sector, against your technology stack.

In the S4T risk evolution equation:

```
dR/dt = δT(t) − αC(t) − βO(t) − γVa(t)
```

T(t) represents Threat Exposure — the rate at which new risks are introduced to your environment. RI does not directly reduce T(t) (your threat exposure is determined by your attack surface, not your intelligence capability), but it determines how quickly and accurately you respond to changes in T(t). An organisation with strong RI detects a new critical CVE affecting their stack within hours and patches within 24. An organisation with no RI discovers the same CVE weeks later — often after it has been exploited.

**RI has two distinct functions:**
1. **External intelligence** — what is happening in the threat landscape outside your organisation
2. **Internal intelligence** — what is happening on your own systems (vulnerability posture, asset exposure)

Both are required. External intelligence without internal context tells you what attackers are doing but not whether you are exposed. Internal intelligence without external context tells you what vulnerabilities you have but not which ones attackers are actively exploiting.

---

## Prerequisites

Before implementing this layer, you should have:
- [ ] Asset inventory (from CF layer) — you need to know what you have before you can assess what threats are relevant
- [ ] Wazuh deployed (from OS layer) — the primary platform for internal vulnerability intelligence
- [ ] At least one team member with time to review intelligence feeds regularly (30–60 minutes per week minimum)

---

## RI Layer Components

### RI-1: Threat Intelligence Feeds

**What it is:** Structured data about current threats — malicious IP addresses, domains, file hashes, attack techniques, and vulnerability disclosures — ingested from external sources and used to enrich your detection and response.

**Tier 1 — Free, always-on feeds (implement these first):**

| Feed | Content | Integration |
|---|---|---|
| [CISA Known Exploited Vulnerabilities (KEV)](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) | CVEs being actively exploited in the wild | Manual review weekly; API available |
| [Abuse.ch URLhaus](https://urlhaus.abuse.ch/) | Malicious URLs and domains | MISP integration |
| [Abuse.ch MalwareBazaar](https://bazaar.abuse.ch/) | Malware file hashes | MISP integration |
| [Feodo Tracker](https://feodotracker.abuse.ch/) | C2 server IPs (banking trojans, ransomware) | Wazuh integration, pfSense blocklist |
| [AlienVault OTX](https://otx.alienvault.com/) | Community threat intelligence (free tier) | MISP integration |
| [Emerging Threats Open](https://rules.emergingthreats.net/open/) | Suricata/Snort IDS rules | pfSense / Suricata integration |
| NVD CVE Feed | All new CVE disclosures | Wazuh vulnerability detection (built-in) |

**Tier 2 — Sector-specific intelligence (implement based on your sector):**

- **Financial services (Brazil):** CERT.br feeds, Banco Central threat communications
- **Healthcare:** HHS HC3 (US), ANS communications (Brazil)
- **General:** [CERT.br](https://www.cert.br/) incident reports (Brazil), ENISA threat landscape (EU)

**Reference implementation:** [MISP (Malware Information Sharing Platform)](https://www.misp-project.org/)

MISP is the recommended threat intelligence platform for S4T deployments. It aggregates multiple feeds, normalises indicators, and integrates with Wazuh to automatically enrich SIEM alerts with threat context.

**MISP integration with Wazuh:**

1. Deploy MISP (Docker deployment recommended for small organisations)
2. Configure MISP to pull from Tier 1 feeds automatically
3. Configure Wazuh to query MISP for IP/domain enrichment on alerts
4. Result: when Wazuh detects a connection to an external IP, it automatically queries MISP and flags if the IP is in a known-malicious list

---

### RI-2: Vulnerability Management

**What it is:** A systematic process for identifying, prioritising, and tracking remediation of vulnerabilities in your environment.

**Vulnerability management has three stages:**
1. **Discovery** — finding vulnerabilities before attackers do
2. **Prioritisation** — deciding which to fix first
3. **Tracking** — ensuring fixes are applied within SLA

**Discovery:**

Wazuh's vulnerability detection module continuously scans agents for installed package versions and correlates against the NVD CVE database. No additional scanner is required for endpoint vulnerability discovery.

For web applications and external-facing services, complement Wazuh with:
- [OpenVAS](https://www.openvas.org/) — network and service vulnerability scanning (open source)
- Manual review of internet-exposed services (check [Shodan](https://www.shodan.io/) for your IP ranges to see what attackers see)

**Prioritisation — S4T vulnerability scoring:**

Do not treat all CVEs equally. Prioritise using this decision framework:

```
Priority = CVSS Score × Exploitability Factor × Asset Criticality Factor
```

| Factor | Definition | Values |
|---|---|---|
| CVSS Score | Base severity from NVD | 0.0 – 10.0 |
| Exploitability | Is this CVE in CISA KEV or actively exploited? | 3× if yes, 1× if no |
| Asset Criticality | How critical is the affected system? | 3× High, 2× Medium, 1× Low |

**Example:** A CVSS 7.5 vulnerability on a high-criticality system with a known exploit in the wild:
```
Priority = 7.5 × 3 × 3 = 67.5 (Immediate action)
```

The same vulnerability on a low-criticality dev server without known exploitation:
```
Priority = 7.5 × 1 × 1 = 7.5 (Schedule within 30 days)
```

**Patch SLAs by priority:**

| Priority Score | Patch SLA |
|---|---|
| ≥ 50 (Critical with exploitation) | 24 hours |
| 20–49 (High priority) | 7 days |
| 5–19 (Medium priority) | 30 days |
| < 5 (Low priority) | 90 days |

**Tracking:**

Maintain a vulnerability register — a living document (or Wazuh report) showing:
- All open vulnerabilities above your priority threshold
- Assigned owner for each remediation
- Target patch date
- Actual patch date (when resolved)
- SLA compliance rate

Track SLA compliance monthly. Target: > 90% of critical and high priority vulnerabilities patched within SLA.

---

### RI-3: Business Impact Analysis

**What it is:** A structured assessment of which systems are most critical to business operations, and what the impact of a security incident affecting each system would be.

**Why RI needs BIA:** Threat intelligence without business context produces generic prioritisation. BIA allows you to weight threats by their potential business impact — a vulnerability on your payment processing system is more urgent than the same vulnerability on your internal wiki, even if the CVSS score is identical.

**BIA for security purposes — simplified format:**

For each High and Medium criticality asset, document:

| Asset | Business function | Impact if unavailable | Max tolerable downtime | Data sensitivity | Dependent systems |
|---|---|---|---|---|---|
| payroll-db-01 | Payroll processing | Employees not paid | 4 hours | Restricted (employee PII) | payroll-app-01 |
| mail-server-01 | Internal/external communications | Business communications halted | 1 hour | Internal + Confidential | None |
| ecommerce-01 | Customer sales | Revenue loss ~R$50K/hour | 30 minutes | Confidential (customer data, payments) | payment-gateway, inventory-db |

The BIA output feeds directly into the CF layer's asset criticality classification and the RI layer's vulnerability prioritisation.

---

### RI-4: Third-Party and Supply Chain Risk

**What it is:** Assessment and monitoring of security risks introduced by vendors, suppliers, and technology providers.

**Why this matters:** A significant proportion of breaches involve third parties with access to systems or data. Your security programme is only as strong as its weakest supply chain link.

**Minimum third-party risk process:**

1. **Inventory your critical third parties:** Who has access to your systems or data? Identify all vendors, SaaS providers, managed service providers, and contractors.

2. **Classify by risk:** For each third party, assess:
   - Do they have access to Confidential or Restricted data?
   - Do they have remote access to your systems?
   - What happens to your operations if their service is disrupted?

3. **Require security evidence:** For high-risk third parties, request:
   - Evidence of ISO 27001 certification or SOC 2 report
   - Answers to a security questionnaire (CAIQ from the Cloud Security Alliance is a good template)
   - Contractual security requirements (data protection, breach notification obligations)

4. **Monitor for third-party incidents:** Subscribe to threat intelligence about your critical vendors. If a major SaaS provider you use suffers a breach, you need to know immediately and assess your exposure.

---

## Measuring the RI Contribution to T(t)

T(t) — Threat Exposure and Growth Rate — is reduced by RI through faster, more accurate response to new threats. The primary RI metrics are:

**Vulnerability aging:** Average number of days between CVE publication and patch application for Critical and High severity vulnerabilities affecting your environment. Target: < 7 days for Critical, < 30 days for High.

**Threat intelligence coverage:** What percentage of your security controls are informed by current threat intelligence (e.g., Wazuh rules updated with current IOCs, firewall blocklists current). Target: daily update cadence for IP/domain blocklists.

**Intelligence-to-action time:** When a new critical threat relevant to your environment is identified (e.g., a new CVE affecting software you use), how long does it take from intelligence receipt to remediation action? Track this for each critical vulnerability.

The Assessment Tool computes your RI layer score from your answers to the RI-layer questions. Track it quarterly alongside your Security Score.

---

## Common Mistakes in the RI Layer

**Subscribing to too many feeds without capacity to process them.** Three well-integrated feeds that are actually reviewed are more valuable than 20 feeds that generate noise. Start with CISA KEV, Wazuh's built-in CVE detection, and one sector-specific feed.

**CVSS score as the only prioritisation criterion.** A CVSS 9.5 vulnerability with no public exploit on a low-criticality system is less urgent than a CVSS 7.0 vulnerability on a critical system with active exploitation. Always weight by exploitability and asset criticality.

**Treating vulnerability management as a quarterly activity.** New critical CVEs are disclosed daily. Vulnerability management must be a weekly (for new discoveries) and daily (for CISA KEV updates) activity.

**Ignoring supply chain risk.** Third-party compromises are a leading cause of significant breaches. Every vendor with access to your systems or data is a potential attack vector.

**No business impact analysis.** Without BIA, every vulnerability is equally urgent. BIA is what transforms a list of CVEs into a prioritised remediation backlog.

---

## Next Steps

After completing this layer:

1. Your threat intelligence is now feeding into Wazuh alerts — watch for the first intelligence-enriched alert to validate the integration
2. Proceed to [Layer VA — Validation & Assurance](layer-VA.md) to test whether your OS and CF controls actually detect the threats your RI feeds are reporting
3. Review your vulnerability register weekly — the first 30 days will reveal the most significant gaps

For questions, open an issue on [GitHub](https://github.com/diegoneuber/S4T-Framework/issues) or contact [feedback@sec4.tech](mailto:feedback@sec4.tech).
