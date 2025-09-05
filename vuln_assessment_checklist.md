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

### 🤝 WITH PERMISSION (Interview + Internal Questionnaire)

Conducted with business reps or IT staff.

### 👥 Business Profile
- **How many employees?**
  - *Why:* Scales risk exposure (more users = more potential compromise points)
  - *Risk:* Larger surface area for phishing, insider threats
  - *Value Loss:* Higher user count amplifies breach scope

- **Internal IT or outsourced?**
  - *Why:* Impacts speed of response and ownership of security
  - *Risk:* Outsourced teams may lack deep org-specific insight
  - *Value Loss:* $5,000–$250,000 (delayed patching, miscommunication)

- **BYOD policy?**
  - *Why:* Unmanaged devices introduce risk
  - *Risk:* Infected devices may bypass network controls
  - *Value Loss:* $50,000–$1M+ (malware, data leaks)

- **Documented security policy?**
  - *Why:* Defines accountability and standards
  - *Risk:* Policy gaps = no guidance, inconsistent enforcement
  - *Value Loss:* $25,000–$250,000 (HR, legal, incident mismanagement)

... [Remaining section continues in this detailed format with risk, consequence, and value loss added]

---

This checklist is designed to help guide **safe, ethical, and comprehensive assessments** for any business size. It empowers you to make **actionable, risk-based security recommendations** aligned with real-world impact.

