# 40. Information Technology Act & Cyber Law

## Overview

Cyber law deals with online activities and crimes like hacking, identity theft, and misuse of data. The IT Act supports legal recognition of electronic records and deals with cyber offences.

---

## Why It Matters

Businesses handle digital payments, customer data, and online operations. Cyber incidents can create legal liability and reputation damage.


## Key Principles

- Legal recognition of e-records and e-signatures
- Punishment for cyber crimes
- Responsibility for security and safe practices
- Handling unauthorized access and data misuse


## Key Terms

| Term | Definition |
|------|------------|
| **Cyber crime** | Crime using computers/internet |
| **E-signature** | Electronic signing method |
| **Data breach** | Unauthorized data leak |
| **Phishing** | Trick to steal passwords/OTPs |


## Use Case

Company adopts policies for data security and safe online transactions.


## Scenario

> Employee clicks phishing link; company email gets hacked. Business strengthens authentication and trains staff.


## Examples

- Online fraud through fake UPI link.
- Unauthorized access to customer database and leak.

---

## Audited Appendix

# Information Technology Act & Cyber Law — Audit File

---

## 1. Jargon Buster

| Term | Plain-English Definition | Why It Matters in Practice |
|---|---|---|
| **IT Act 2000** | India's primary legislation governing electronic commerce, digital transactions, and cyber offences; amended significantly in 2008 to expand scope to cover data privacy and intermediary rules | Backbone of all digital contract validity, e-signature enforceability, and cyber crime prosecution in India |
| **Cyber Crime** | Any unlawful act where a computer or network is the tool, target, or repository; ranges from hacking and phishing to identity theft and ransomware | Triggers criminal liability (imprisonment + fine) and civil compensation claims under the IT Act |
| **E-Signature / Digital Signature** | Electronic Signature = broad category (OTP, biometric, typed name); Digital Signature = specifically asymmetric-key-based cryptographic signature issued by a licensed Certifying Authority (CA) under IT Act; has full legal validity equal to wet ink | SaaS contracts, vendor agreements, MoUs signed digitally are legally enforceable only if correct signature type is used for the document class |
| **Data Breach** | Unauthorized acquisition, access, disclosure, or loss of personal data held by an organization; triggers mandatory reporting to CERT-In within 6 hours and potential compensation liability under Section 43A and DPDP Act 2023 | A single breach event can cascade into regulatory fine, civil suit, and reputational damage simultaneously |
| **Phishing** | Social engineering attack via fraudulent email/SMS/call impersonating a trusted entity to steal credentials, financial data, or install malware; prosecuted under Sec 66 (hacking), 66C (identity theft), 66D (cheating by personation) | Most frequent entry point for corporate breaches; employee awareness and MFA are primary defences |
| **CERT-In** | Indian Computer Emergency Response Team — nodal agency under Ministry of Electronics and IT (MeitY); issues cybersecurity advisories, mandates incident reporting, and coordinates national cyber crisis response | CERT-In Direction 2022 mandates 6-hour breach reporting; non-compliance = criminal liability for CISO/management |
| **Intermediary Liability** | Under Section 79 of IT Act, platforms/ISPs acting as intermediaries (hosting third-party content) get safe harbor protection — i.e., they are not liable for third-party content — provided they follow due diligence conditions | AI platforms, SaaS marketplaces, and app stores must publish terms, maintain grievance mechanisms, and act on takedown notices to retain immunity |
| **Section 43A** | Mandates body corporates (companies handling sensitive personal data) to implement "reasonable security practices"; if negligent, they are liable to pay compensation to affected persons — no cap specified in the section itself | Audit finding of missing encryption, poor access controls, or no ISMS policy directly triggers 43A exposure; compensation can be substantial |
| **DPDP Act 2023** | Digital Personal Data Protection Act — India's comprehensive data protection law; introduces consent framework, data principal rights, data fiduciary obligations, and a Data Protection Board; penalty up to INR 250 crore per violation | Overlaps with IT Act Section 43A but adds broader obligations; companies must map which law applies and ensure dual compliance |
| **Safe Harbor** | Legal protection shielding intermediaries from liability for third-party content/acts, conditional on meeting prescribed due diligence norms (Sec 79 IT Act); analogous to DMCA safe harbor in the US | Lost if platform has "actual knowledge" of unlawful content and fails to act, or if platform actively participates in or induces the unlawful act |

---

## 2. Frameworks & Mental Models

### Framework 1: Cyber Incident Response Framework (NIST CSF Adapted for India — IT Act + CERT-In Overlay)

```
IDENTIFY → PROTECT → DETECT → RESPOND → RECOVER
    |           |          |          |           |
Asset inv.  MFA, enc.  SIEM/EDR  CERT-In 6hr  RCA + patch
Data map    ISMS doc.  Anomaly   Legal notice  DPDP notice
Vendor due  Sec 43A    phishing  FIR if reqd.  Board review
diligence   policy     alerts    Preserve logs Audit report
```

**India-specific overlays:**
- IDENTIFY: Map data assets against DPDP Act "sensitive personal data" categories + IT (Reasonable Security Practices) Rules 2011 definition
- RESPOND: CERT-In Direction 2022 mandates 6-hour reporting for specified incidents (ransomware, data breach, unauthorized access, DDoS on critical infra)
- RECOVER: IT Act Section 43A compensation assessment; DPDP Act Data Protection Board complaint tracking

**Usage for PM/CISO:** Run this as a quarterly tabletop exercise. Map every product feature that handles user data to IDENTIFY column. Gap in PROTECT column = Section 43A exposure.

---

### Framework 2: IT Act Offences Taxonomy

```
CATEGORY A — Computer Crimes (Against Systems)
  Sec 43: Unauthorized access, damage, disruption → Civil compensation
  Sec 66: Hacking (dishonest/fraudulent intent) → 3 yrs imprisonment + fine
  Sec 66F: Cyber terrorism → Life imprisonment

CATEGORY B — Identity & Data Crimes
  Sec 66B: Receiving stolen computer resource → 3 yrs + fine
  Sec 66C: Identity theft (fraudulent use of electronic signature/password) → 3 yrs + 1L fine
  Sec 66D: Cheating by personation using computer → 3 yrs + 1L fine

CATEGORY C — Content Crimes
  Sec 66E: Publishing private images without consent → 3 yrs + 2L fine
  Sec 67: Publishing obscene material → 3 yrs (1st) / 5 yrs (repeat) + fine
  Sec 67A: Sexually explicit content → 5 yrs + 10L fine
  Sec 67B: Child sexual abuse material → 5 yrs + 10L fine

CATEGORY D — Data Protection / Corporate
  Sec 43A: Body corporate negligent data handling → Compensation (civil)
  Sec 72A: Disclosure of information in breach of lawful contract → 3 yrs + 5L fine
```

**Usage for audit:** Map each product feature/business process to potential offence category. A fintech app's OTP-based login failure = potential 66C vector. An AI platform generating deepfakes = 66E + 67 risk.

---

### Framework 3: Intermediary Liability Safe Harbor Conditions (Sec 79 + IT Rules 2021)

```
SAFE HARBOR GRANTED IF:
  [1] Platform publishes clear Terms of Service (ToS) and Privacy Policy
  [2] Platform does NOT initiate, select, or modify third-party content
  [3] Platform follows "due diligence" under IT (Intermediary Guidelines) Rules 2021:
       → Grievance Officer appointed, name + contact publicly available
       → Grievance resolved within 15 days (30 days for content takedown)
       → User verification for significant social media intermediaries (SSMI)
       → Proactive monitoring for prohibited content (SSMIs only)
  [4] Platform acts on court/government takedown orders promptly
  [5] No "actual knowledge" of unlawful content AND failure to act

SAFE HARBOR LOST IF:
  → Platform edits or curates content in a way that makes it complicit
  → Platform ignores valid takedown notice after receipt
  → Platform provides tools that facilitate the unlawful act
  → Court finds constructive knowledge (platform "should have known")
```

---

### Framework 4: Data Protection Compliance Framework (IT Act + DPDP Act 2023)

```
LAYER 1 — IT Act (Existing Obligations)
  Sec 43A + IT (RSP&SP) Rules 2011:
    → Implement IS/IEC 27001 or equivalent ISMS
    → Collect only necessary sensitive personal data (SPD)
    → Obtain consent before collecting SPD
    → Disclose purpose of collection

LAYER 2 — DPDP Act 2023 (New Obligations)
    → Appoint Data Protection Officer (DPO) if significant data fiduciary
    → Consent Management: granular, purpose-limited, revocable
    → Data Principal Rights: access, correction, erasure, grievance
    → Data Localisation: specific categories may require India storage
    → Cross-Border Transfer: only to countries notified by GoI
    → Children's Data: verifiable parental consent required

LAYER 3 — Enforcement Overlap
    → Breach of DPDP = Data Protection Board adjudication (penalty up to INR 250 Cr)
    → Breach of Sec 43A = Civil court compensation claim by affected individuals
    → Breach of CERT-In Direction = Sec 70B IT Act criminal liability
```

---

## 3. Formulas / Thresholds / Decision Rules

### Rule 1: CERT-In 6-Hour Breach Reporting Rule

```
TRIGGER CONDITIONS (any one):
  - Unauthorized access to IT systems / data
  - Data breach involving personal data
  - Ransomware attack (regardless of data exfiltration)
  - DDoS attack on critical infrastructure
  - Malware deployment compromising network
  - Targeted scanning/probing of critical networks
  - Breach of websites / tampering with government systems
  - Compromise of social media accounts of critical entities

TIMELINE:
  T+0:00  → Incident detected / confirmed
  T+0:06  → CERT-In initial report filed (incident.cert-in.org.in)
  T+30d   → Detailed incident report submitted
  Ongoing → Logs preserved for 180 days minimum on India servers

NON-COMPLIANCE PENALTY:
  Sec 70B(7): Up to 1 year imprisonment + fine for failure to report
```

**Decision rule for PM:** If any system alert triggers that involves customer data or unauthorized access — immediately escalate to CISO. Do NOT wait for full investigation before reporting. Report first, investigate simultaneously.

---

### Rule 2: Section 43A Compensation Trigger

```
ELEMENT 1: Is the entity a "body corporate"? (Yes = IT Act applies)
ELEMENT 2: Does it possess, deal, or handle sensitive personal data?
  SPD Categories: passwords, financial info, health info, biometric,
                  sexual orientation, medical records
ELEMENT 3: Was there negligence in implementing reasonable security practices?
  Test: Would a reasonably prudent security-conscious organization
        have implemented the control that was missing?
ELEMENT 4: Did this negligence cause wrongful loss/gain to any person?

IF ALL 4 = YES → Compensation liability triggered
  Quantum: No statutory cap; courts determine based on actual damage
  Practical range: INR 5 lakh to multi-crore for large-scale breaches
```

---

### Rule 3: Reasonable Security Practices Standard

```
PRIMARY STANDARD: IS/IEC 27001 (ISMS) — explicitly recognized in IT (RSP&SP) Rules 2011
ALTERNATIVE: DSCI Best Practices, NIST CSF with India mapping

MINIMUM CONTROLS EXPECTED (audit checklist):
  [ ] Data inventory and classification policy in place
  [ ] Access control: role-based, least privilege, MFA for admin
  [ ] Encryption: AES-256 for data at rest; TLS 1.2+ for data in transit
  [ ] Incident response plan documented and tested annually
  [ ] Employee security awareness training (documented + frequency tracked)
  [ ] Vulnerability assessment and penetration testing (VAPT) — at least annual
  [ ] Vendor/third-party security assessment before data sharing
  [ ] Privacy policy published; consent mechanism functional
  [ ] Data retention and deletion policy implemented
  [ ] CISO or equivalent role designated with reporting line to board
```

---

### Rule 4: Intermediary Due Diligence Checklist

```
FOR ALL INTERMEDIARIES:
  [ ] ToS and Privacy Policy published in English + 8th Schedule languages
  [ ] Grievance Officer: name + contact publicly available
  [ ] Grievance redressal within 15 days
  [ ] Content takedown on court/government order within prescribed time
  [ ] No editorial control over third-party user content

ADDITIONAL FOR SIGNIFICANT SOCIAL MEDIA INTERMEDIARIES (>5M users):
  [ ] Chief Compliance Officer (Indian resident, liable for non-compliance)
  [ ] Nodal Contact Person (24x7 coordination with law enforcement)
  [ ] Physical contact address in India
  [ ] Monthly compliance report published
  [ ] Proactive AI-based monitoring for prohibited content
  [ ] Traceability: preserve originator info for messaging platforms
```

---

## 4. Do / Don't

### DO — For IT/AI/SaaS Product Companies and Consulting Firms Operating in India

| # | DO |
|---|---|
| 1 | Implement IS/IEC 27001-aligned ISMS and document it — this is the legal "reasonable security practices" standard under Section 43A |
| 2 | File CERT-In incident reports within 6 hours of detecting a breach — report even if investigation is incomplete; preliminary report is acceptable |
| 3 | Appoint a Grievance Officer (name + contact on website) to maintain intermediary safe harbor under Section 79 |
| 4 | Enforce Multi-Factor Authentication (MFA) for all employee email, cloud consoles, and admin portals — phishing is the #1 entry vector |
| 5 | Conduct annual VAPT (Vulnerability Assessment and Penetration Testing) by a CERT-In empanelled security auditor |
| 6 | Map all personal data flows — including third-party SDKs, analytics tools, and cloud providers — to ensure DPDP Act compliance |
| 7 | Obtain separate, granular, purpose-specific consent for each category of sensitive personal data collected |
| 8 | Train all employees on phishing recognition, password hygiene, and data handling at onboarding and annually thereafter (document attendance) |
| 9 | Review and update vendor/SaaS contracts to include data processing agreements (DPAs) with security obligation clauses |
| 10 | Preserve system logs for minimum 180 days on servers physically located in India (CERT-In Direction 2022 requirement) |
| 11 | Engage legal counsel to assess which AI-generated content your platform produces may trigger Section 66E (private images) or 67 (obscenity) liability |
| 12 | Establish a Data Protection Board complaint response protocol under DPDP Act — designate a DPO or equivalent before enforcement begins |

---

### DON'T — For IT/AI/SaaS Product Companies and Consulting Firms Operating in India

| # | DON'T |
|---|---|
| 1 | Don't delay CERT-In reporting to wait for a complete forensic investigation — 6 hours is from detection, not investigation completion |
| 2 | Don't assume SaaS intermediary safe harbor automatically applies — actively maintain due diligence conditions or lose immunity |
| 3 | Don't store sensitive personal data without encryption — unencrypted PII storage is explicit evidence of negligence under Section 43A |
| 4 | Don't allow employees to use personal email or devices for client data without a formal BYOD policy and technical controls |
| 5 | Don't bundle consent — "by using this app you agree to everything" style consent is invalid under DPDP Act 2023 |
| 6 | Don't transfer personal data to foreign countries not yet notified by Government of India under DPDP Act — monitor the approved countries list |
| 7 | Don't ignore takedown notices (from courts, CERT-In, or government) — inaction destroys safe harbor and triggers direct liability |
| 8 | Don't collect more personal data than necessary for the stated purpose — data minimization is both a DPDP obligation and a Section 43A risk reducer |
| 9 | Don't use digital signatures interchangeably with e-signatures for high-stakes documents (loan agreements, government filings) — check the legal requirement for each document type |
| 10 | Don't allow admin/root access without MFA and privileged access management (PAM) — this is consistently the breach vector in Indian corporate incidents |
| 11 | Don't deploy AI models that process children's personal data without implementing verifiable parental consent mechanisms — DPDP Act imposes strict rules |
| 12 | Don't treat cybersecurity as an IT-only issue — Section 43A and DPDP Act create board-level liability; CISO must report to senior management with documented board oversight |

---

## 5. Metric-Driven Scenarios with Anti-Examples

### Scenario 1: SaaS Company Data Breach Response Under IT Act + DPDP Act

**Setting:** A B2B SaaS company (HR software) with 200,000 employee records of corporate clients discovers unauthorized access to its database. Data exfiltrated includes Aadhaar numbers, salary data, and health insurance details.

**Metrics:**
- Records affected: 200,000 (all qualify as sensitive personal data)
- Time of detection: Monday 9:00 AM
- CERT-In deadline: Monday 3:00 PM (6 hours from detection)
- Data Protection Board complaint risk: High (individual rights holders can file)
- Section 43A exposure: Substantial (SPD + negligence if controls inadequate)
- DPDP Act penalty exposure: Up to INR 250 crore per violation

**Correct Response:**
1. T+0: Isolate affected systems, activate incident response plan
2. T+1hr: CISO notifies management, legal counsel engaged
3. T+5hr: CERT-In preliminary report filed (incident.cert-in.org.in)
4. T+6hr: Corporate clients notified via contractual breach notification clause
5. T+24hr: Forensic team engaged, log preservation on Indian servers confirmed
6. T+72hr: Assess DPDP Act data principal notification obligations
7. T+30d: Detailed CERT-In report submitted; remediation evidence documented
8. Ongoing: Section 43A audit trail prepared (ISMS documentation, MFA logs, access controls)

**Anti-Example (Legal Exposure Quantification):**
Company waits 48 hours to file CERT-In report while "investigating." Result:
- Sec 70B(7): CISO faces 1 year imprisonment + fine
- Sec 43A: Compensation claims from 200,000 affected individuals (even INR 5,000 per person = INR 100 crore aggregate)
- DPDP Act: Data Protection Board penalty — up to INR 250 crore for failure to notify
- Client contracts: Breach of data processing agreement = contract termination + penalty clauses
- Total quantified exposure: INR 350+ crore + imprisonment of senior officers

---

### Scenario 2: AI Platform Intermediary Liability Assessment

**Setting:** An AI-powered social content platform (user-generated content + AI remix features) with 8 million Indian users receives a court order to take down a deepfake video of a private citizen. Platform delayed action for 10 days while "reviewing" the order.

**Metrics:**
- User base: 8 million (qualifies as Significant Social Media Intermediary — SSMI threshold: 5 million)
- Court order receipt: Day 0
- Action taken: Day 10
- SSMI compliance requirement: Prompt action on court orders (no specific day limit, but "expeditiously" = courts have interpreted as 24-72 hours)
- Grievance Officer response SLA: 15 days for grievances; court orders require faster action

**Correct Response:**
1. Maintain Chief Compliance Officer (Indian resident) with authority to act on orders
2. Implement 24-hour court order response protocol
3. On receipt of deepfake takedown order: immediately geo-restrict or remove content
4. File compliance affidavit with court within 24 hours
5. Notify originating user of takedown with appeal process
6. Document AI remix feature liability: if platform AI created the deepfake = platform is NOT an intermediary for that content (no safe harbor)

**Anti-Example (Legal Exposure Quantification):**
Platform's 10-day delay + AI remix involvement:
- Safe harbor LOST: Platform had "actual knowledge" of unlawful content and failed to act
- Sec 66E liability: Publishing private image without consent = 3 years imprisonment + INR 2 lakh fine for platform officers
- Contempt of court: Possible for ignoring court order
- SSMI non-compliance: MeitY can order app store removal from Indian stores
- AI-generated content: Platform IS the author if its AI created the deepfake — full criminal and civil liability
- Estimated exposure: Regulatory shutdown risk + INR 50 crore + civil suit from victim

---

### Scenario 3: Consulting Firm Email Phishing Incident

**Setting:** An employee at a 500-person IT consulting firm clicks a phishing link in a fake Microsoft 365 login email. The attacker gains access to the employee's email account, which contains client project documents including source code and financial projections. Attacker exfiltrates data over 3 days before detection.

**Metrics:**
- Breach duration: 72 hours undetected
- Data exfiltrated: Client source code (confidential), financial projections (confidential)
- CERT-In reporting deadline: 6 hours from Day-4 detection = missed by firm
- Section 72A exposure: Disclosure of information in breach of contract (3 yrs + INR 5 lakh fine)
- Client NDA breach: Contract termination + liquidated damages

**Correct Response:**
1. Immediately revoke compromised credentials and force password reset
2. Enable MFA across all M365 accounts (if not already done)
3. Preserve email logs, access logs, and exfiltration evidence on Indian servers
4. File CERT-In report within 6 hours of detection
5. Notify affected clients immediately per contractual breach notification clause
6. Engage cyber forensics firm to determine full scope
7. File police complaint under Sec 66 (hacking) and 66B (receiving stolen data)
8. Review all client contracts for data handling obligations; assess Section 43A if personal data involved
9. Implement phishing simulation training program — track click rates; target <5% click rate within 6 months
10. Deploy email security gateway with advanced threat protection

**Anti-Example (Legal Exposure Quantification):**
Firm conceals breach from clients for 2 weeks to "manage reputation":
- Sec 72A: Criminal liability for disclosure in breach of contract — 3 yrs imprisonment
- Client NDA breach: If NDA includes notification obligation (most do), immediate material breach
- Section 43A: If client data included personal data of the client's employees, compensation liability
- Professional indemnity insurance: Claim may be voided if breach concealed
- Estimated exposure: INR 25 crore client damages + regulatory action + loss of client relationships
- Key metric missed: Phishing click rate was never measured; if it had been tracked, 35% click rate would have triggered MFA deployment 6 months earlier

---

## 6. Practitioner Playbook

### 12-Step Playbook: Building an IT Act + DPDP Compliance Program for an Indian Tech Company

**Phase 1: Foundation (Months 1-2)**

**Step 1: Executive Mandate and Governance Setup**
Secure board-level resolution designating a Data Protection Officer (DPO) / CISO with direct reporting to CEO/board. Document board oversight of cybersecurity. This creates the governance trail essential for Section 43A defense ("we were not negligent; we had oversight").

**Step 2: Data Asset Inventory and Classification**
Catalog all personal data flows: what data is collected, where it is stored (Indian servers vs. cloud regions), how it is shared, with whom, and for what purpose. Classify into personal data, sensitive personal data (per IT Act), and data under DPDP Act. Output: Data Flow Diagrams (DFDs) per product line.

**Step 3: Gap Assessment Against Reasonable Security Practices**
Conduct internal audit against IS/IEC 27001 controls + CERT-In empanelled auditor's checklist. Document every gap. This gap report is your compliance roadmap and, critically, evidence that you took the "reasonable" standard seriously.

**Phase 2: Control Implementation (Months 3-5)**

**Step 4: Technical Controls Deployment**
Deploy MFA across all systems (prioritize admin, email, cloud consoles). Implement AES-256 encryption for data at rest, TLS 1.2+ for transit. Deploy SIEM for real-time log monitoring. Set up log retention for 180 days on India-located servers (CERT-In Direction compliance).

**Step 5: Policy and Process Documentation**
Draft and approve: Information Security Policy, Incident Response Policy, Data Retention and Deletion Policy, Acceptable Use Policy, Vendor Risk Management Policy. These policies are your Section 43A shield — they demonstrate the "reasonable practices" standard was institutionalized.

**Step 6: Consent Management Implementation**
Build granular consent management for each data collection touchpoint. Ensure consent is: purpose-specific, informed, freely given, and revocable. Implement DPDP Act data principal rights portal (access, correction, erasure requests with 30-day SLA).

**Step 7: Intermediary Compliance (If Platform Company)**
Appoint Grievance Officer (name + contact on website). Implement content takedown workflow with SLA tracking. If SSMI: appoint Chief Compliance Officer (Indian resident), set up 24x7 law enforcement contact channel, begin proactive monitoring implementation.

**Phase 3: Operationalization (Months 6-8)**

**Step 8: Employee Training Program**
Launch mandatory cybersecurity awareness training. Include: phishing recognition, password hygiene, data handling, incident reporting procedure. Run quarterly phishing simulations. Track click rate; target <5%. Document all training — attendance records are critical evidence for Section 43A defense.

**Step 9: Incident Response Drills**
Conduct tabletop exercises simulating: (a) ransomware attack, (b) phishing breach of email, (c) third-party vendor data exposure. Practice the CERT-In 6-hour reporting clock. Ensure CISO and legal counsel both know the reporting portal (incident.cert-in.org.in) and process.

**Step 10: Vendor Due Diligence Program**
Assess top 20 vendors/SaaS providers against security questionnaire. Require Data Processing Agreements from all vendors who access personal data. Include right-to-audit clauses. Non-compliant vendors = Section 43A risk transfer back to your organization.

**Phase 4: Continuous Compliance (Month 9 Onward)**

**Step 11: Annual VAPT and Certification Renewal**
Engage CERT-In empanelled auditor for annual penetration testing. Remediate findings within defined SLAs (Critical: 24 hrs, High: 7 days, Medium: 30 days). Maintain ISO 27001 certification if achieved. VAPT reports are your strongest evidence of ongoing reasonable security practices.

**Step 12: Regulatory Monitoring and Board Reporting**
Monitor MeitY and Data Protection Board notifications for DPDP Act rules (still being finalized). Brief board quarterly on: open vulnerabilities, incident count, training completion %, VAPT status, regulatory changes. Board minutes documenting these briefings = governance evidence that defeats negligence claims.

---

## 7. Content Critique

### Gap Analysis: Where Standard IT Act Training Falls Short

**Gap 1: DPDP Act 2023 vs. IT Act Overlap — Unclear Enforcement Hierarchy**

Standard training presents IT Act Section 43A and DPDP Act 2023 as complementary, but fails to address the critical unresolved question: when both apply to the same breach, which enforcement body takes precedence? The IT (RSP&SP) Rules 2011 under Sec 43A have never been tested in a high-stakes case alongside DPDP Act's Data Protection Board. A data breach involving sensitive personal data could theoretically trigger: (a) civil compensation suit by individuals under Sec 43A, (b) Data Protection Board penalty under DPDP Act, and (c) CERT-In criminal liability under Sec 70B. The interaction — whether triple jeopardy applies or one proceeding bars another — is legally uncharted. Practitioners need a clear escalation matrix that doesn't yet exist.

**Gap 2: Cross-Border Data Transfer Rules — Inadequate Guidance**

The DPDP Act 2023 allows personal data transfer to countries notified by the Government of India. As of 2026, the Government has not published a comprehensive whitelist/blacklist of approved countries. Standard training glosses over this by saying "follow government notifications," but fails to address: What if your SaaS provider (e.g., Salesforce, AWS) stores data in non-notified regions? Standard contractual clauses (SCCs) used in GDPR context have no equivalent under DPDP Act. Indian companies with global operations are essentially complying with a rule whose contours don't yet exist. Compliance programs must build monitoring mechanisms for GoI notifications — a process most training programs do not address.

**Gap 3: AI-Generated Content Liability — Significant Legal Blind Spot**

The IT Act was drafted before generative AI existed. Current training material maps AI platforms as "intermediaries" and assumes safe harbor applies. This is legally incorrect when: (a) the platform's AI generates the content (platform is the author, not an intermediary), (b) AI produces deepfakes (Sec 66E applies to the platform, not a third party), or (c) AI curates and amplifies harmful content (constructive knowledge + editorial control = safe harbor loss). No clear judicial precedent in India yet. EU AI Act provides useful analogical framework, but Indian practitioners are operating in a void. Audit programs need an AI content liability assessment layer separate from the standard intermediary checklist.

**Gap 4: Dark Web Monitoring Obligations — Missing from Most Compliance Programs**

CERT-In Direction 2022 implicitly requires organizations to have threat intelligence capabilities to detect their own data appearing on dark web forums. Yet no training explicitly addresses: What is the legal obligation to monitor dark web for leaked organizational data? What triggers a mandatory CERT-In report when dark web intelligence (not system logs) indicates a breach? Does finding your customer data on a dark web marketplace start the 6-hour CERT-In clock? These questions are operationally critical for SaaS companies and consulting firms handling client data, and are entirely absent from standard IT Act training curricula.

---

## 8. Quick-Recall Card

```
IT ACT + CYBER LAW — RAPID REFERENCE

CERT-In: 6 hours from detection → file preliminary report
Sec 43A: Body corporate + SPD + negligence + damage = compensation liability
Sec 66: Hacking = 3 yrs; 66C: Identity theft = 3 yrs + 1L fine
Sec 79: Intermediary safe harbor = conditional on active due diligence
DPDP Act: Penalty up to INR 250 crore per violation
Digital Signature: Asymmetric crypto + Certifying Authority = legally valid
Safe Harbor LOST if: actual knowledge + inaction OR editorial control
Reasonable Security = IS/IEC 27001 + documented ISMS + VAPT evidence
Section 72A: Employee leaks client data = 3 yrs + 5L fine (criminal)
Log retention: 180 days minimum on Indian servers (CERT-In Direction 2022)
MFA: First line of defense; absence = direct evidence of negligence
DPDP consent: Purpose-specific, informed, revocable, granular — no bundling

KEY THRESHOLDS:
  CERT-In breach report: T + 6 hours
  CERT-In detailed report: T + 30 days
  Grievance redressal: 15 days (intermediaries)
  SSMI threshold: 5 million registered users
  DPDP Act max penalty: INR 250 crore
  Children's data: Verifiable parental consent required

PHISHING INCIDENT CHECKLIST:
  [ ] Revoke credentials immediately
  [ ] Preserve logs (180 days, India servers)
  [ ] File CERT-In report within 6 hours
  [ ] Notify affected clients per contract
  [ ] File FIR under Sec 66 + 66C
  [ ] Deploy MFA if not done
  [ ] Train staff; track click rate (target <5%)

INTERMEDIARY CHECKLIST:
  [ ] ToS + Privacy Policy published
  [ ] Grievance Officer named publicly
  [ ] No editorial control on user content
  [ ] Court orders actioned promptly
  [ ] If SSMI: CCO + Nodal Officer + compliance reports
```

As a PM/Consultant/AI Lead, the one question to answer with this framework is: "If a breach or cyber incident occurred in our systems today, can we demonstrate — with documented evidence — that we implemented reasonable security practices, reported to CERT-In within 6 hours, and fulfilled all data principal obligations under both the IT Act and DPDP Act 2023?"

---

## 9. Self-Audit

<!-- Self-Audit: Topic: Information Technology Act & Cyber Law — Audit File. Date: 2026-04-20. Prepared for: Legal Aspects of Business module, Audit Management Course. Coverage assessment: All 9 mandatory sections completed. Section 1 (Jargon Buster): 10 terms covered — IT Act 2000, Cyber Crime, E-Signature/Digital Signature, Data Breach, Phishing, CERT-In, Intermediary Liability, Section 43A, DPDP Act 2023, Safe Harbor. Section 2 (Frameworks): 4 frameworks — Cyber Incident Response (NIST CSF India-adapted), IT Act Offences Taxonomy, Intermediary Safe Harbor Conditions, Data Protection Compliance Framework (IT Act + DPDP). Section 3 (Formulas/Thresholds): CERT-In 6-hour rule with trigger conditions, Section 43A 4-element compensation trigger test, Reasonable Security Practices checklist (10 controls), Intermediary due diligence checklist (SSMI + general). Section 4 (Do/Don't): 12 DOs + 12 DONTs, lens = IT/AI/SaaS product companies and consulting firms in India. Section 5 (Scenarios): 3 scenarios with metrics — SaaS data breach (quantified exposure INR 350Cr+), AI platform intermediary liability (quantified regulatory shutdown + INR 50Cr), consulting firm phishing (quantified INR 25Cr + criminal liability). Section 6 (Playbook): 12-step PM/CISO compliance program, organized in 4 phases over 9+ months. Section 7 (Critique): 4 gaps identified — DPDP vs IT Act enforcement hierarchy, cross-border transfer rules, AI-generated content liability, dark web monitoring obligations. Section 8 (Quick-Recall Card): Complete with exact mandatory phrase. Section 9 (Self-Audit): This comment. Lens consistency: IT/AI/Product/Consulting lens maintained throughout. File size: Exceeds 13,000 bytes. Exact phrase present: Confirmed — "As a PM/Consultant/AI Lead, the one question to answer with this framework is: ____." Quality flags: DPDP Act 2023 rules still being finalized as of audit date — monitor MeitY for subordinate legislation updates. CERT-In empanelled auditor requirement for VAPT is a current regulatory requirement — confirm list remains current. Cross-border transfer country whitelist not yet published by GoI — monitor for updates before advising clients on cloud region selection. -->
