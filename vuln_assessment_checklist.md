# 🛡️ Comprehensive Vulnerability Assessment & Business Profile Checklist

> ⚠️ **Disclaimer:** This assessment is observational and advisory only. It does not replace a certified audit (e.g., ISO27001, PCI-DSS) and does not authorize active testing unless explicitly agreed upon. Results are provided based on the available context and public information at the time of review.

---

## 🧑‍🏫 Assessment Roles & Involvement

| Role             | Description                                   |
|------------------|-----------------------------------------------|
| Lead Assessor     | Reviews findings, validates recommendations  |
| Student Analyst   | Performs checklist interviews and recon steps under supervision |
| Client POC        | Provides context, approvals, and answers     |

> ⚠️ Students do not perform technical testing without permission. All findings are reviewed by a certified practitioner.

---

## ✅ Free Vulnerability Assessment Checklist

### 🔍 WITHOUT PERMISSION (Passive External Recon Only)

These tests rely entirely on publicly available data. **No scans or system interaction.**

---

### 🔎 Domain & DNS Intelligence
- **Check DNS records (A, MX, TXT, NS, CNAME)**
  - *Why:* Identify exposed infrastructure, third-party services, and phishing risk
  - *Security Risk:* DNS records may expose internal or sensitive infrastructure
  - *Consequence:* Attackers can impersonate services or direct traffic to malicious servers
  - *Potential Value Loss:* $5,000–$250,000+ (brand damage, phishing attacks)

- **Subdomain enumeration (crt.sh, Subfinder, Amass)**
  - *Why:* Uncover forgotten or misconfigured web assets
  - *Security Risk:* Unmonitored assets often have weak or outdated security
  - *Consequence:* Exposed admin panels, dev servers, or test environments
  - *Potential Value Loss:* $10,000–$500,000 (data leaks, initial access points)

- **WHOIS lookup**
  - *Why:* Reveal domain ownership, expiration, registrar exposure
  - *Security Risk:* Leaked PII or outdated records could enable domain hijacking
  - *Consequence:* Attackers could take over expired domains or use contact info for phishing
  - *Potential Value Loss:* $2,000–$100,000 (reputation, domain recovery)

### 🌐 Web & Server Exposure
- **SSL/TLS test via SSLLabs**
  - *Why:* Check for outdated protocols and misconfigurations
  - *Security Risk:* Weak encryption or missing HSTS can allow MITM attacks
  - *Consequence:* User data interception, session hijacking
  - *Potential Value Loss:* $10,000–$1M+ (compliance fines, customer loss)

- **Shodan or Censys scan**
  - *Why:* Discover open services and exposed infrastructure
  - *Security Risk:* Attackers use these to find unpatched or exposed services
  - *Consequence:* Ransomware or botnet entry via known CVEs
  - *Potential Value Loss:* $50,000–$2M+ (service downtime, data breach)

- **Google Dorking for leaks (`site:example.com ext:sql|log`)**
  - *Why:* Identify exposed configs or sensitive logs
  - *Security Risk:* Leaked databases or error logs may expose credentials or internal logic
  - *Consequence:* SQLi or logic abuse via reverse-engineered structures
  - *Potential Value Loss:* $25,000–$1M+ (DB dump, insider data exposed)

- **GitHub public repo search (API keys, .env files)**
  - *Why:* Employees may leak keys inadvertently
  - *Security Risk:* Leaked secrets enable unauthorized API or cloud access
  - *Consequence:* Privileged access, customer data leakage
  - *Potential Value Loss:* $50,000–$3M+ (data theft, resource abuse)

### 🔐 Credential Intelligence
- **HaveIBeenPwned domain check**
  - *Why:* Identify breached employee emails
  - *Security Risk:* Credentials may be reused elsewhere (SSO, VPN)
  - *Consequence:* Account compromise, phishing campaigns
  - *Potential Value Loss:* $10,000–$500,000 (access escalation, brand damage)

- **Hunter.io, Email format discovery**
  - *Why:* Reveal employee email naming conventions
  - *Security Risk:* Enables spearphishing and credential guessing
  - *Consequence:* Targeted phishing, CEO fraud
  - *Potential Value Loss:* $20,000–$1M+ (fraudulent transactions, data exfiltration)

### ☁️ Cloud Service Exposure
- **Public S3/Blob storage discovery**
  - *Why:* Misconfigured cloud storage is a common breach vector
  - *Security Risk:* Anyone can download sensitive files if access is public
  - *Consequence:* Data breach, intellectual property loss
  - *Potential Value Loss:* $100,000–$5M+ (legal fines, IP theft)

- **Look for exposed Jenkins, Grafana, Kibana, AWS dashboards**
  - *Why:* These reveal config data and can be used for privilege escalation
  - *Security Risk:* Default creds or open dashboards = attacker pivot points
  - *Consequence:* Full infrastructure compromise
  - *Potential Value Loss:* $500,000–$10M+ (ransomware, data theft, extortion)

---

## 🧾 NIST-Aligned Business Profile Checklist

### 🔐 Identity & Access Management (NIST: PR.AC, ID.AM)

- **Unique user accounts for all staff**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: PR.AC-1  
  *Risk:* Shared accounts = no traceability

- **MFA enabled on email, VPN, cloud admin, privileged users**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: PR.AC-7  
  *Risk:* Credential compromise via phishing

- **Password policy and manager use**  
  🔹 Priority: MEDIUM  
  ✅ NIST Mapping: PR.AC-1, PR.AC-4  
  *Risk:* Reuse or weak credentials

- **Onboarding/Offboarding includes access removal**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: ID.AM-3, PR.AC-4  
  *Risk:* Former employees retain access

---

### 🌐 Zero Trust & Network Controls (NIST: PR.AC-5, SP 800-207)

- **Network segmentation and access control between systems**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: PR.AC-5  
  *Risk:* Lateral movement after breach

- **Device health checked before access (e.g., MDM)**  
  🔹 Priority: MEDIUM  
  ✅ NIST Mapping: PR.IP-3, PR.AC-6  
  *Risk:* Infected or jailbroken devices bypass controls

- **Re-authentication for critical access actions**  
  🔹 Priority: MEDIUM  
  ✅ NIST Mapping: PR.AC-11  
  *Risk:* Session hijacking

---

### 🧱 Remote Access & VPN (NIST: PR.AC, DE.CM)

- **VPN required for all remote access**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: PR.AC-3  
  *Risk:* Exposure of internal services

- **VPN uses MFA, no split tunneling**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: PR.AC-7, PR.AC-6  
  *Risk:* Split tunnel = data exfiltration risk

- **VPN logs and session activity reviewed**  
  🔹 Priority: MEDIUM  
  ✅ NIST Mapping: DE.CM-7  
  *Risk:* Missed unauthorized access attempts

---

### 🖥️ Endpoint & Device Controls (NIST: PR.IP, PR.DS)

- **All company endpoints enrolled in MDM/EDR**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: PR.IP-1, PR.DS-1  
  *Risk:* Rogue or unmanaged devices

- **Full disk encryption enforced**  
  🔹 Priority: MEDIUM  
  ✅ NIST Mapping: PR.DS-1  
  *Risk:* Physical data loss

- **USB use restricted or monitored**  
  🔹 Priority: LOW  
  ✅ NIST Mapping: PR.IP-1  
  *Risk:* Data exfiltration via removable media

---

### ☁️ Cloud & SaaS Risk Review (NIST: ID.RA, PR.DS)

- **Public cloud storage buckets audited**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: PR.DS-1, PR.IP-4  
  *Risk:* Leaked PII, data breach

- **IAM permissions regularly reviewed**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: PR.AC-4, PR.AC-5  
  *Risk:* Excessive privileges

- **Key rotation enforced and logged**  
  🔹 Priority: MEDIUM  
  ✅ NIST Mapping: PR.AC-6, DE.CM-1  
  *Risk:* Credential reuse or secret leaks

---

### 📄 Policy, Training, and Governance (NIST: ID.GV, PR.AT)

- **Written security policy with role ownership**  
  🔹 Priority: MEDIUM  
  ✅ NIST Mapping: ID.GV-1, ID.GV-2  
  *Risk:* Undefined expectations

- **Annual security awareness training**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: PR.AT-1, PR.AT-2  
  *Risk:* Human error, phishing

- **Incident Response Plan with contact list**  
  🔹 Priority: HIGH  
  ✅ NIST Mapping: RS.RP-1, RS.CO-1  
  *Risk:* Uncoordinated response to attack

---

### 📊 Risk Matrix Summary

| Category               | Example Threat               | Impact   | Likelihood | Risk Level |
|------------------------|-------------------------------|----------|-------------|------------|
| Identity & Access Mgmt | Orphaned admin account        | High     | Medium      | High       |
| Cloud Misconfig        | Public S3 bucket with PII     | Critical | Medium      | High       |
| Endpoint Security      | Infected BYOD laptop          | High     | High        | Critical   |
| No Logging/SIEM        | No logs to trace intrusion    | Critical | High        | Critical   |
| Email Exposure         | User email in data breach     | Medium   | High        | Medium     |

---

## 🛠️ Suggested Actions

| Issue                 | Priority | Recommendation                                    | Owner       | Due       |
|----------------------|----------|--------------------------------------------------|-------------|-----------|
| No MFA on VPN        | High     | Enforce 2FA on VPN access                        | IT Admin    | Immediate |
| Public cloud bucket  | High     | Set proper access policies or remove exposure   | Cloud Team  | 3 Days    |
| Missing IR Plan      | High     | Draft and test IR plan with key contacts        | CISO        | 2 Weeks   |

---

## 🔢 Optional NIST Maturity Scorecard

| NIST CSF Function | Score (1–5) | Notes                            |
|-------------------|--------------|----------------------------------|
| Identify          | 3            | Assets known, risks undocumented |
| Protect           | 2            | Gaps in MFA and policy           |
| Detect            | 1            | No central monitoring/log review |
| Respond           | 2            | Plan exists, untested            |
| Recover           | 4            | Validated backup process         |

> Score Guide: 1 = None, 3 = Partial, 5 = Fully Mature & Tested

---

## ✅ Summary
This checklist serves as a professional and educational tool:
- For cybersecurity startups offering value-first services
- For student analysts learning real frameworks
- For businesses needing a structured starting point



[Continue with NIST-aligned assessment checklist from this point forward — already contained in existing document content below.]

