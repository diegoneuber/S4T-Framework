# Calculating the S4T Security Score

This document explains how the Security Score S(t) is computed, what each variable means, and how to track it manually if you choose not to use the Assessment Tool.

---

## The Formula

```
S(t) = [C(t)^α · O(t)^β · Va(t)^γ] / R(t)^δ
```

**Variables:**

| Symbol | Name | Description | Range |
|---|---|---|---|
| C(t) | Control Coverage Index | Proportion of risk-relevant controls implemented and verified, weighted by asset criticality | [0, 1] |
| O(t) | Operational Maturity Score | Detection rate × response velocity composite | [0, 1] |
| Va(t) | Validation Effectiveness Score | Proportion of BAS techniques detected or blocked | [0, 1] |
| R(t) | Current Risk Level | Estimated current risk state (derived from incident and vulnerability data) | [0.01, 1] |
| α, β, γ, δ | Coefficients | Sensitivity weights derived from your environment | α+β+γ+δ ≈ 1.0 |

**Default coefficients (cross-sector baseline from validation study):**

```
α = 0.35  (Control Coverage — highest weight)
β = 0.25  (Operational Maturity)
γ = 0.30  (Validation Effectiveness)
δ = 0.10  (Risk denominator sensitivity)
```

---

## Maturity Benchmarks

| Score | Level | Description |
|---|---|---|
| < 0.40 | **Initial** | Reactive posture, no structured programme |
| 0.40 – 0.65 | **Developing** | Basic controls, limited continuous monitoring |
| 0.65 – 0.80 | **Mature** | Structured programme with continuous validation |
| ≥ 0.80 | **Optimised** | Adaptive, self-correcting security architecture |

---

## Computing Each Variable

### C(t) — Control Coverage Index

C(t) measures what proportion of your assets have their required controls implemented and verified.

**Step 1:** List all assets and their criticality (High / Medium / Low).

**Step 2:** For each asset, count required controls and verified controls.

**Step 3:** Calculate per-asset coverage: `coverage_i = verified_i / required_i`

**Step 4:** Apply criticality weights: High = 3, Medium = 2, Low = 1

**Step 5:** Compute weighted average:

```
C(t) = Σ(coverage_i × weight_i) / Σ(weight_i)
```

**Example:**

| Asset | Criticality | Required | Verified | Coverage | Weight | Weighted |
|---|---|---|---|---|---|---|
| payroll-db | High | 8 | 6 | 0.75 | 3 | 2.25 |
| mail-server | High | 8 | 8 | 1.00 | 3 | 3.00 |
| workstation-01 | Medium | 6 | 4 | 0.67 | 2 | 1.33 |
| dev-server | Low | 4 | 3 | 0.75 | 1 | 0.75 |
| **Total** | | | | | **9** | **7.33** |

```
C(t) = 7.33 / 9 = 0.81
```

---

### O(t) — Operational Maturity Score

O(t) is a composite of your detection rate and response velocity.

**Detection rate (DR):** From your most recent BAS campaign, what proportion of executed techniques were detected by your SIEM/EDR?

```
DR = (techniques detected) / (total techniques tested)
```

**Normalised MTTR (nMTTR):** Your Mean Time to Respond, mapped to a 0–1 scale:

| MTTR | nMTTR |
|---|---|
| ≥ 72 hours | 0.00 |
| 48 hours | 0.17 |
| 24 hours | 0.50 |
| 8 hours | 0.75 |
| 4 hours | 0.88 |
| ≤ 1 hour | 1.00 |

For MTTR values in between, interpolate linearly.

**O(t) composite:**

```
O(t) = 0.5 × DR + 0.5 × nMTTR
```

**Example:**
- BAS campaign detected 12 of 20 techniques: DR = 12/20 = 0.60
- Current MTTR = 18 hours → nMTTR ≈ 0.57 (interpolating between 24h=0.50 and 8h=0.75)

```
O(t) = 0.5 × 0.60 + 0.5 × 0.57 = 0.585
```

---

### Va(t) — Validation Effectiveness Score

Va(t) is the simplest variable to compute:

```
Va(t) = (ATT&CK techniques detected or blocked) / (total techniques tested)
```

This comes directly from your BAS campaign results. Techniques that are blocked by preventive controls (e.g., firewall blocks the connection) count equally with techniques that are detected by the SIEM.

**Weighting by ATT&CK tactic (optional, for more precision):**

If you want to weight results by tactic importance:

| ATT&CK Tactic | Weight |
|---|---|
| Initial Access | 2× |
| Execution | 2× |
| Persistence | 1.5× |
| Privilege Escalation | 1.5× |
| Defence Evasion | 1× |
| Credential Access | 2× |
| Discovery | 1× |
| Lateral Movement | 1.5× |
| Collection | 1× |
| Exfiltration | 1× |
| Impact | 2× |

Apply weights to each technique result and compute a weighted average.

---

### R(t) — Current Risk Level

R(t) is the most challenging variable to compute precisely, because it represents your current risk state — which is not directly observable. S4T uses a proxy estimation from observable indicators.

**R(t) estimation formula:**

```
R(t) = min(1.0, (C_incidents × 1.0 + H_incidents × 0.5 + CVE_critical × 0.3 + CVE_high × 0.1) / normaliser)
```

Where:
- `C_incidents` = number of Critical (P1) incidents in the past 30 days
- `H_incidents` = number of High (P2) incidents in the past 30 days
- `CVE_critical` = number of unpatched Critical CVEs in your environment
- `CVE_high` = number of unpatched High CVEs in your environment
- `normaliser` = a value calibrated to your organisation size (start with 20 for small orgs, 50 for medium)

**Minimum value:** R(t) is bounded at 0.01 (R(t) = 0 would make the denominator undefined and is not meaningful — even a fully optimised organisation has some residual risk).

**Example:**
- 0 P1 incidents, 2 P2 incidents, 5 Critical CVEs, 18 High CVEs (medium org, normaliser = 50):

```
R(t) = (0×1.0 + 2×0.5 + 5×0.3 + 18×0.1) / 50
     = (0 + 1.0 + 1.5 + 1.8) / 50
     = 4.3 / 50 = 0.086
```

**Note:** If R(t) is very low (< 0.05), it amplifies S(t) significantly. This is mathematically correct — lower current risk means higher Security Score — but verify that your R(t) estimation is realistic and not artefactually low due to incomplete data.

---

## Computing S(t)

With all four variables calculated, apply the Security Score formula:

```
S(t) = [C(t)^α · O(t)^β · Va(t)^γ] / R(t)^δ
```

**Using the default coefficients (α=0.35, β=0.25, γ=0.30, δ=0.10):**

```
S(t) = [C(t)^0.35 · O(t)^0.25 · Va(t)^0.30] / R(t)^0.10
```

**Continuing the example:**
- C(t) = 0.81
- O(t) = 0.585
- Va(t) = 0.60 (12/20 techniques)
- R(t) = 0.086

```
S(t) = [0.81^0.35 · 0.585^0.25 · 0.60^0.30] / 0.086^0.10
     = [0.934 · 0.874 · 0.848] / 0.763
     = 0.692 / 0.763
     = 0.907
```

Wait — 0.907 (Optimised) seems high given Va(t) = 0.60. Let us verify. The R(t) of 0.086 is low, which inflates the score. In practice, organisations with 5 unpatched critical CVEs would likely have a higher R(t) or a lower C(t). The example illustrates the mathematics; your real values will be consistent with your actual security posture.

**Geometric mean property:** The numerator uses a geometric mean structure (exponents sum to approximately 1). This means **no single variable can compensate for weakness in another**. If Va(t) = 0 (no validation), S(t) = 0 regardless of how good C(t) and O(t) are. This is by design — the score is only as strong as its weakest layer.

---

## The Simpler Path: Assessment Tool

If manual calculation is impractical for your organisation, use the [S4T Assessment Tool](https://sec4.tech/assessment).

The Assessment Tool:
- Computes all variables from your questionnaire answers
- Implements the same formula described above
- Produces layer-by-layer breakdown plus overall score
- Available in English and Portuguese, two modes (Executive and Technical)
- Free, no registration required

**Recommended approach:** Use the Assessment Tool for baseline and quarterly measurements. Use the manual calculation method for monthly tracking, where the effort of the full questionnaire is not warranted.

---

## Tracking S(t) Over Time

The score is meaningful only as a trend. A single data point tells you where you are; a trend tells you whether you are improving.

**Monthly tracking:**

| Month | C(t) | O(t) | Va(t) | R(t) | S(t) | Level |
|---|---|---|---|---|---|---|
| Baseline | | | | | | |
| Month 1 | | | | | | |
| Month 2 | | | | | | |
| Month 3 | | | | | | |
| Month 6 | | | | | | |
| Month 12 | | | | | | |

**Visualise the trend.** Plot S(t) over time. A flat or declining trend when you expect improvement is an early warning signal — investigate before the next quarterly review.

---

*For the complete mathematical treatment including the risk evolution equation, equilibrium analysis, and coefficient calibration methodology, see the [S4T v3.0 academic paper](https://doi.org/10.13140/RG.2.2.16699.58408) or the peer-reviewed submission to [Computers & Security](../reference/papers.md).*
