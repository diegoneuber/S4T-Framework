# Using the S4T Assessment Tool with Client Organisations

**Audience:** MSPs and consultants conducting S4T assessments on behalf of client organisations
**Reading time:** 10 minutes

---

## Overview

The [S4T Assessment Tool](https://sec4.tech/assessment) is the fastest way to establish a client's baseline Security Score and identify which framework layers require the most attention. This guide explains how to conduct an assessment effectively, how to interpret results with clients, and how to use the output to structure your engagement.

---

## Assessment Modes

The tool offers two assessment modes. Choose based on the client's technical team availability:

### Executive Assessment (20 questions, ~5 minutes)

**Use when:**
- Initial discovery call with a non-technical executive sponsor
- Client has no dedicated IT or security staff
- You need a quick orientation before a deeper discovery session
- Prospect meeting where you want to demonstrate immediate value

**Characteristics:**
- Binary (Yes/No) questions in business language
- No technical knowledge required
- Produces layer-level scores and overall Security Score
- Lower precision than Technical mode — use as a starting point, not a final baseline

**Recommended workflow:**
Complete the Executive Assessment with the client sponsor during or immediately after the initial meeting. Share the screen and walk through questions together. The results create an immediate conversation about gaps and priorities.

---

### Technical Assessment (33 questions, ~15 minutes)

**Use when:**
- Formal engagement kickoff with IT lead or security team
- Establishing the official baseline Security Score for the client record
- Quarterly reassessment to track programme progress

**Characteristics:**
- 5-point Likert scale questions (None → Optimised)
- Requires IT knowledge to answer accurately
- Produces precise layer-by-layer scores
- This is the score to use for all formal client reporting

**Recommended workflow:**
Conduct the Technical Assessment as a facilitated session with the client's IT administrator or security lead. Go through each question together — do not send the URL and ask the client to complete it independently, as self-reported assessments tend to be optimistic. Your role is to ask follow-up questions that ensure the score reflects actual operational reality, not aspirational state.

---

## Conducting the Assessment — Facilitation Guide

### Before the session

1. **Schedule 45–90 minutes** — the 15-minute estimate assumes rapid, confident answers. Clients often need time to think, look things up, or discuss with colleagues.
2. **Request documentation in advance:** network diagrams (if any), asset lists, existing security policies, most recent penetration test report (if any)
3. **Identify the right participant:** the person who operates the systems daily (IT admin, system administrator) will give more accurate answers than the CISO or manager
4. **Prepare the share link feature** — plan to share results immediately after the session using the Assessment Tool's share link function

### During the session

**Governance layer questions** — facilitate with:
- "Do you have a written security policy? Can you show it to me?"
- "When did leadership last receive a security report? What did it cover?"
- "If I asked your CEO what your risk appetite is for a data breach, what would they say?"

**Risk Intelligence questions** — facilitate with:
- "How do you find out about new vulnerabilities affecting your systems? How quickly?"
- "Can you show me your current list of open vulnerabilities?"
- "What happens when a new critical CVE is published for software you use?"

**Control Framework questions** — facilitate with:
- "Can you show me your asset inventory? Is it complete and current?"
- "Pick any server — can you show me what security controls are on it?"
- "When did you last verify that your backups actually restore?"

**Operational Security questions** — facilitate with:
- "Show me your SIEM dashboard. What does a normal day look like?"
- "Walk me through what happens when a critical alert fires at 2am."
- "What was your last security incident? How long did it take to resolve?"

**Validation questions** — facilitate with:
- "When did you last test whether your SIEM would detect a ransomware attack?"
- "Have you ever run a penetration test? What were the findings?"
- "If I ran Mimikatz on a workstation right now, would your SIEM alert?"

**Adaptive Learning questions** — facilitate with:
- "What security metrics do you track month over month?"
- "After your last incident, what changed in your security programme?"
- "Do you have a 12-month security roadmap?"

### Red flags during facilitation

Watch for these patterns that indicate the score may be inflated:

- **"We have that"** without being able to demonstrate it. Installed ≠ operational. Always ask "can you show me?"
- **"Our vendor handles that."** Third-party managed services count only if the client can verify they are operating and receiving outputs.
- **Answering based on what they intend to have**, not what they currently have. Keep redirecting: "Right now, today — is that in place?"
- **Unanimous "high" ratings across all questions.** A perfect or near-perfect score on first assessment is almost certainly inaccurate. Probe the weakest-looking areas.

### After the session

1. Capture the share link immediately after results appear
2. Take a screenshot of the full results page (for client records)
3. Note the three lowest-scoring layers — these drive your initial recommendations
4. Schedule the findings presentation within 48 hours while the conversation is fresh

---

## Interpreting Results with Clients

### Framing the score

Avoid presenting the score as a grade or judgment. Frame it as a starting point:

> "Your current Security Score is 0.41 — you're in the Developing tier. That means you have real controls in place, which is a solid foundation. The score tells us that your biggest gaps are in Validation (0.22) and Operational Security (0.38). That's actually useful information — it tells us exactly where to focus first to move the needle most efficiently."

### Explaining the layer breakdown

Use the radar chart in the results to visualise which layers are strongest and weakest. Clients understand spider charts intuitively — the closer to the outer edge, the better.

**Key messages for each low-scoring layer:**

| Low layer | Client-facing explanation |
|---|---|
| G (Governance) | "You don't yet have a shared definition of what 'secure enough' means for your organisation. Without that, every security decision is made inconsistently." |
| RI (Risk Intelligence) | "You're not systematically monitoring for new threats relevant to your environment. You're likely finding out about vulnerabilities later than attackers do." |
| CF (Control Framework) | "You don't have complete visibility into what assets you have and what controls are on each one. That means there are blind spots — assets with no security controls." |
| OS (Operational Security) | "When something goes wrong, your response is slower than it needs to be. That window of undetected activity is your biggest operational risk." |
| VA (Validation) | "You have controls, but you don't know if they actually work. The gap between 'we have a firewall' and 'our firewall stops the attacks we'd actually face' is what Validation measures." |
| L (Adaptive Learning) | "Your programme isn't learning from its own results. Without that feedback loop, you'll plateau rather than continuously improve." |

### Handling defensive reactions

Some clients will react defensively to a low score. Prepare for:

**"That can't be right — we just passed our ISO audit."**
> "ISO audits verify that you have documented controls at a point in time. The S4T score measures whether those controls are continuously operational and validated. Many organisations pass compliance audits while still having significant operational security gaps — that's actually one of the problems the framework was designed to reveal."

**"We've never been breached, so we must be doing something right."**
> "That's great. The question the score answers is: do you know why you haven't been breached? Is it because your controls are strong, or because you haven't been targeted yet? The Validation layer specifically tests whether your controls would stop an attack — without that, you can't distinguish between 'we're secure' and 'we've been lucky.'"

**"Our IT provider takes care of all of this."**
> "That's helpful context. The score reflects the actual operational state of your security programme, regardless of who manages it. Let's look at the specific areas where you scored lower and verify with your IT provider whether those capabilities are in place."

---

## Tracking Progress Across Quarterly Assessments

Run the Technical Assessment at each quarterly review. Track results in your client record:

| Quarter | Overall | G | RI | CF | OS | VA | L | Key change |
|---|---|---|---|---|---|---|---|---|
| Q1 Baseline | 0.41 | 0.65 | 0.48 | 0.52 | 0.38 | 0.22 | 0.35 | First assessment |
| Q2 | 0.52 | 0.70 | 0.55 | 0.65 | 0.51 | 0.35 | 0.42 | Wazuh deployed, first BAS |
| Q3 | 0.61 | 0.72 | 0.60 | 0.72 | 0.62 | 0.48 | 0.55 | BAS tuning, patch SLAs |
| Q4 | 0.68 | 0.75 | 0.65 | 0.78 | 0.70 | 0.58 | 0.62 | Mature threshold crossed |

**When a layer score drops between quarters:** investigate before presenting to the client. Score declines usually indicate one of:
- A new vulnerability or incident raised R(t)
- A control that was previously counted is now known to be non-functional
- A staff change removed someone with a key skill
- A system change broke an existing control

A dropping score that is explained and being addressed is a sign of a maturing programme — it means your monitoring is revealing reality rather than hiding it.

---

## Using the Share Link Feature

After completing any assessment, the tool generates a shareable link encoding the results. Use this to:

1. **Send results to the client immediately** — share the link in the meeting follow-up email so they can review results at any time
2. **Compare across time** — keep a log of share links for each quarterly assessment; each link permanently encodes that moment's results
3. **Internal MSP record-keeping** — store share links in your client management system alongside the assessment date

**Note:** The share link encodes the scores in URL parameters — it does not store any client-identifying information on our servers. The results are fully contained in the link itself.

---

## Assessment Tool as a Sales Tool

For prospective clients, the Executive Assessment is an effective demonstration during a first meeting:

1. Ask for 10 minutes at the end of a discovery call
2. Walk through the Executive Assessment with the prospect answering questions
3. Show the results page — the immediate, visual output of a Security Score often creates more impact than any slide deck
4. Use the results to frame your proposed engagement: "Based on your score of 0.35 and the gap in your Validation layer, here's what a 12-month programme with us would look like..."

The assessment is free and requires no registration — there is no barrier to running it with any prospect.

---

*For the full implementation methodology, see [service-delivery.md](service-delivery.md). For the monthly reporting format to deliver to clients after each assessment cycle, see [reporting-template.md](reporting-template.md).*
