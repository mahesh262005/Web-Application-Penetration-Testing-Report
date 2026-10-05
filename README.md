# Web-Application-Penetration-Testing-Report


## 📌 Project Overview

This project presents a black-box Web Application Penetration Testing assessment of the **Altoro Mutual Online Banking Application** hosted on `testfire.net`.

The assessment was performed using the **OWASP Top 10:2021** framework and focused on identifying, validating, and documenting web application security vulnerabilities.

The target is an intentionally vulnerable training application used for cybersecurity education and security testing practice.

---

## 🎯 Objectives

The main objectives of this assessment were:

- Identify security vulnerabilities in the web application.
- Assess authentication and authorization mechanisms.
- Test input validation and injection vulnerabilities.
- Identify broken access-control issues.
- Assess business-logic security.
- Evaluate session and transport security.
- Validate identified vulnerabilities using controlled Proof-of-Concept testing.
- Map vulnerabilities to the OWASP Top 10:2021.
- Assess the potential impact of identified vulnerabilities.
- Provide remediation recommendations.

---

## 🧪 Assessment Information

| Category | Details |
|---|---|
| Target | Altoro Mutual / `testfire.net` |
| Target IP | `65.61.137.117` |
| Assessment Type | Black-Box Web Application Penetration Test |
| Testing Platform | Kali Linux |
| Standard | OWASP Top 10:2021 |
| Methodology | OWASP Web Security Testing Guide |
| Assessment Window | 03–04 October 2026 |
| Tester | Mahesh — Security Researcher |
| Engagement Type | Portfolio / Training Engagement |

---

## 🔍 Scope

The assessment focused on the following application and infrastructure components:

- `testfire.net`
- `www.testfire.net`
- `demo.testfire.net`
- `demo2.testfire.net`
- `altoro.testfire.net`
- `ftp.testfire.net`
- `localhost.testfire.net`
- `evil.testfire.net`

The assessment included both unauthenticated and authenticated testing.

### Ports Identified

- TCP/80 — HTTP
- TCP/443 — HTTPS
- TCP/8080 — HTTP Alternate

The environment identified Apache Tomcat / Coyote JSP Engine components.

---

# 🔎 Methodology

The assessment followed a structured penetration-testing workflow.

## 1. Reconnaissance & Information Gathering

Initial reconnaissance was performed to understand the target's attack surface.

Activities included:

- DNS enumeration
- WHOIS information gathering
- Subdomain enumeration
- Port scanning
- Service detection
- Web technology identification
- WAF detection
- TLS/SSL configuration assessment

---

## 2. Application Mapping

The web application was manually explored to identify important functionality and attack surfaces.

Areas examined included:

- Login functionality
- Search functionality
- Account functionality
- Transaction history
- Fund transfer functionality
- Application pages
- Authentication workflows

Burp Suite Proxy was used to intercept and analyze HTTP requests and responses.

---

## 3. Vulnerability Identification

Testing was performed against:

- Authentication controls
- Authorization controls
- Input validation
- Session handling
- Business logic
- Security headers
- Transport security
- Error handling
- Logging and monitoring controls

---

## 4. Exploitation & Validation

Potential vulnerabilities were validated using controlled testing techniques.

Tools included:

- Burp Suite Repeater
- Burp Suite Intruder
- SQLMap
- Custom HTML Proof-of-Concept
- Manual request manipulation

Only controlled validation was performed against the authorized training target.

---

## 5. Reporting

Confirmed vulnerabilities were documented with:

- Vulnerability description
- Evidence
- Proof of Concept
- Impact
- Severity
- OWASP Top 10 mapping
- Remediation recommendations

---

# 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| Nmap | Port and service enumeration |
| WHOIS | Domain information gathering |
| dig | DNS resolution |
| Subfinder | Subdomain enumeration |
| WhatWeb | Web technology fingerprinting |
| WAFW00F | WAF detection |
| sslscan | TLS/SSL security assessment |
| Burp Suite Community | Web application testing |
| Burp Repeater | Manual request manipulation |
| Burp Intruder | Authentication and brute-force testing |
| SQLMap | SQL Injection validation |
| Custom HTML PoC | Clickjacking validation |

---

# 🌐 Reconnaissance Results

## Port & Service Enumeration

Nmap identified the following accessible services:

- Port 80 — HTTP
- Port 443 — HTTPS
- Port 8080 — HTTP Alternate

The scan identified web services associated with Apache Tomcat / Coyote.

---

## Subdomain Enumeration

Subfinder identified multiple subdomains associated with the target.

Identified subdomains included:

- `www`
- `demo`
- `demo2`
- `altoro`
- `ftp`
- `localhost`
- `evil`

This demonstrated a broader application footprint that could increase the overall attack surface.

---

## DNS Enumeration

DNS resolution identified the target IP:

`65.61.137.117`

---

## WAF Detection

WAFW00F testing did not identify a Web Application Firewall protecting the target.

---

## TLS Assessment

SSL/TLS testing identified several weaknesses:

- TLS 1.0 enabled
- TLS 1.1 enabled
- TLS 1.3 unavailable
- 1024-bit DHE parameters
- Missing fallback SCSV

---

# 🚨 Vulnerability Summary

A total of **13 distinct findings** were identified.

| # | Finding | OWASP Category | Severity | CVSS |
|---|---|---|---|---|
| 1 | SQL Injection — Authentication Bypass | A03: Injection | Critical | 9.8 |
| 2 | Broken Access Control — IDOR Fund Transfer | A01: Broken Access Control | Critical* | 8.1 |
| 3 | No Lockout / Brute Force + Username Enumeration | A07: Identification & Authentication Failures | High | 7.5 |
| 4 | Cleartext Credentials over HTTP | A02: Cryptographic Failures | High | 7.4 |
| 5 | Reflected Cross-Site Scripting | A03: Injection | Medium | 6.1 |
| 6 | Verbose Server Error / Stack Trace | A05: Security Misconfiguration | Medium | 5.3 |
| 7 | Clickjacking | A05: Security Misconfiguration | Medium | 4.3 |
| 8 | Weak TLS Configuration | A02: Cryptographic Failures | Medium | 5.9 |
| 9 | Outdated Tomcat Component | A06: Vulnerable & Outdated Components | Low | 5.0 |
| 10 | Information Disclosure | A05: Security Misconfiguration | Low | 3.1 |
| 11 | Insecure Design — No Transaction Limits | A04: Insecure Design | High | 7.1 |
| 12 | Missing Anti-CSRF Protection | A08: Software & Data Integrity Failures | Medium | 6.5 |
| 13 | Logging & Monitoring Failures | A09: Security Logging & Monitoring Failures | Medium | N/A |

### Risk Distribution

- 🔴 Critical: 2
- 🟠 High: 3
- 🟡 Medium: 6
- 🟢 Low: 2

**Total Findings: 13**

> Finding #2 received a CVSS score of 8.1 but was treated as critical from a business-impact perspective because the issue affected financial transaction functionality.

---

# 🔥 Detailed Findings Summary

## 1. SQL Injection — Authentication Bypass

### OWASP

**A03 — Injection**

### Severity

**Critical — CVSS 9.8**

The login functionality was found vulnerable to SQL Injection through the user-input parameter.

A crafted SQL Injection payload was able to bypass authentication and provide access to the banking dashboard.

### Impact

- Authentication bypass
- Unauthorized access
- Potential access to sensitive banking functionality
- Potential chaining with other vulnerabilities

### Remediation

- Use prepared statements.
- Use parameterized SQL queries.
- Implement server-side input validation.
- Apply least-privilege database permissions.
- Use additional defensive controls such as WAF protection.

---

# 2. Broken Access Control — IDOR in Fund Transfer

### OWASP

**A01 — Broken Access Control**

### Severity

**Critical Business Impact — CVSS 8.1**

The fund-transfer functionality accepted client-controlled parameters including:

- `fromAccount`
- `toAccount`
- `transferAmount`

The application did not properly enforce server-side ownership and authorization checks.

### Demonstrated Impact

The assessment demonstrated unauthorized manipulation of transaction parameters, including a transfer amount of:

`2,323,232`

### Remediation

- Enforce server-side authorization.
- Verify account ownership.
- Validate destination accounts.
- Implement transaction limits.
- Implement CSRF protection.
- Require additional verification for high-value transactions.

---

# 3. No Account Lockout / Brute Force Protection

### OWASP

**A07 — Identification & Authentication Failures**

### Severity

**High — CVSS 7.5**

Burp Intruder was used to perform authentication testing.

A total of **49 requests** were tested and response differences were observed.

The testing indicated insufficient protection against automated authentication attacks and potential username enumeration.

### Impact

Attackers may be able to:

- Perform repeated login attempts.
- Identify valid usernames.
- Attempt credential attacks.
- Continue automated authentication attempts without effective blocking.

### Remediation

- Implement rate limiting.
- Implement account lockout or progressive delays.
- Add CAPTCHA after repeated failures.
- Use uniform authentication responses.
- Implement MFA.

---

# 4. Cleartext Credentials over HTTP

### OWASP

**A02 — Cryptographic Failures**

### Severity

**High — CVSS 7.4**

Authentication traffic was observed over HTTP.

### Impact

Credentials and session-related information may be exposed to attackers capable of monitoring network traffic.

### Remediation

- Enforce HTTPS.
- Redirect HTTP to HTTPS.
- Enable HSTS.
- Use secure session cookies.
- Avoid transmitting sensitive information over plaintext HTTP.

---

# 5. Reflected Cross-Site Scripting

### OWASP

**A03 — Injection**

### Severity

**Medium — CVSS 6.1**

The search functionality reflected user-controlled input without sufficient output encoding.

### Impact

A malicious payload could potentially execute JavaScript within a victim's browser context.

### Remediation

- Apply context-aware output encoding.
- Validate user input.
- Implement a strong Content Security Policy.
- Avoid unsafe HTML rendering.

---

# 6. Verbose Server Error / Stack Trace Disclosure

### OWASP

**A05 — Security Misconfiguration**

### Severity

**Medium — CVSS 5.3**

Malformed input to the transaction functionality generated a verbose server-side error.

The response disclosed information including:

- Java class information
- Internal package information
- Apache Tomcat information
- Application implementation details

### Remediation

- Use centralized exception handling.
- Return generic errors to users.
- Disable detailed stack traces.
- Store detailed errors only in server-side logs.

---

# 7. Clickjacking

### OWASP

**A05 — Security Misconfiguration**

### Severity

**Medium — CVSS 4.3**

The application did not implement effective clickjacking protection through:

- `X-Frame-Options`
- CSP `frame-ancestors`

A custom HTML iframe Proof-of-Concept was used to validate the issue.

### Remediation

Implement appropriate security headers such as:

`X-Frame-Options: DENY`

and/or a CSP policy using:

`frame-ancestors 'none'`

---

# 8. Weak TLS Configuration

### OWASP

**A02 — Cryptographic Failures**

### Severity

**Medium — CVSS 5.9**

TLS testing identified legacy protocol and cryptographic configuration weaknesses.

### Identified Issues

- TLS 1.0 enabled
- TLS 1.1 enabled
- TLS 1.3 unavailable
- 1024-bit DHE parameters
- Missing fallback SCSV

### Remediation

- Disable TLS 1.0.
- Disable TLS 1.1.
- Enable TLS 1.3.
- Use strong key exchange parameters.
- Use modern cipher suites.

---

# 9. Vulnerable & Outdated Components

### OWASP

**A06 — Vulnerable & Outdated Components**

### Severity

**Low — CVSS 5.0**

The application environment disclosed an outdated Apache Tomcat version:

`Tomcat 7.0.92`

### Impact

Unsupported or outdated software may contain known vulnerabilities and increases the attack surface.

### Remediation

- Upgrade to a supported Tomcat version.
- Maintain regular patch management.
- Monitor vendor security advisories.
- Remove unsupported components.

---

# 10. Information Disclosure

### OWASP

**A05 — Security Misconfiguration**

### Severity

**Low — CVSS 3.1**

The application disclosed technical information through:

- Server banners
- Application/server information
- Open-source notices
- Subdomain information

### Remediation

- Minimize server banners.
- Remove unnecessary technical information.
- Review exposed subdomains.
- Disable unnecessary services.

---

# 11. Insecure Design — No Transaction Limits

### OWASP

**A04 — Insecure Design**

### Severity

**High — CVSS 7.1**

The transaction workflow lacked effective controls such as:

- Per-transaction limits
- Daily limits
- Transaction velocity controls
- Step-up authentication
- Anomaly detection

### Impact

An attacker with access to a valid session could potentially perform high-value transactions without additional verification.

### Remediation

- Implement transaction limits.
- Implement daily cumulative limits.
- Require MFA/OTP for high-value transactions.
- Implement transaction anomaly detection.
- Introduce fraud monitoring.

---

# 12. Missing Anti-CSRF Protection

### OWASP

**A08 — Software & Data Integrity Failures**

### Severity

**Medium — CVSS 6.5**

State-changing functionality did not include a dedicated anti-CSRF token.

### Impact

An attacker could potentially attempt to cause a victim's authenticated browser to perform unauthorized state-changing requests.

### Remediation

- Implement unpredictable CSRF tokens.
- Validate tokens server-side.
- Use appropriate `SameSite` cookie settings.
- Protect all state-changing operations.

---

# 13. Security Logging & Monitoring Failures

### OWASP

**A09 — Security Logging & Monitoring Failures**

### Severity

**Medium**

During testing, effective blocking mechanisms such as throttling, CAPTCHA, or account lockout were not observed.

### Impact

Automated attacks may continue without adequate detection and response.

### Remediation

- Implement centralized logging.
- Monitor authentication failures.
- Monitor transaction anomalies.
- Monitor parameter manipulation.
- Integrate security events with SIEM.
- Configure alerting for suspicious activity.

---

# 🔗 Attack Narrative

The assessment demonstrated how multiple weaknesses could be chained together.

## Attack Path 1 — SQL Injection to Transaction Manipulation

    Reconnaissance
          ↓
    Attack Surface Discovery
          ↓
    SQL Injection
          ↓
    Authentication Bypass
          ↓
    Banking Dashboard Access
          ↓
    Broken Access Control / IDOR
          ↓
    Transaction Parameter Manipulation
          ↓
    Unauthorized Fund Transfer

---

## Attack Path 2 — Authentication Attack

    Login Endpoint
          ↓
    Burp Intruder
          ↓
    Repeated Authentication Requests
          ↓
    Username Enumeration
          ↓
    Potential Credential Attack
          ↓
    Authenticated Access

---

## Attack Path 3 — XSS / CSRF

    Reflected XSS
          +
    Missing CSRF Protection
          ↓
    Malicious Request / Script Execution
          ↓
    Potential State-Changing Action
          ↓
    Potential Unauthorized Transaction

---

# 📊 OWASP Top 10:2021 Coverage

The assessment identified confirmed findings across **8 of the 10 OWASP Top 10:2021 categories**.

| OWASP Category | Status |
|---|---|
| A01 — Broken Access Control | ✅ Confirmed |
| A02 — Cryptographic Failures | ✅ Confirmed |
| A03 — Injection | ✅ Confirmed |
| A04 — Insecure Design | ✅ Confirmed |
| A05 — Security Misconfiguration | ✅ Confirmed |
| A06 — Vulnerable & Outdated Components | ✅ Confirmed |
| A07 — Identification & Authentication Failures | ✅ Confirmed |
| A08 — Software & Data Integrity Failures | ✅ Confirmed |
| A09 — Security Logging & Monitoring Failures | ✅ Confirmed |
| A10 — Server-Side Request Forgery | ⚪ Not Applicable |

A10 — SSRF was not applicable to the available application functionality from the black-box testing perspective.

---

# 📈 Overall Risk

## 🔴 Critical

**Overall Risk Rating: 9.8 / 10**

The overall risk rating was driven by the highest-severity confirmed vulnerability, SQL Injection authentication bypass.

The combination of multiple vulnerabilities created several possible attack paths.

The most significant risks were:

- Authentication bypass
- Unauthorized access
- Broken access control
- Transaction manipulation
- Weak authentication controls
- Cleartext credentials
- Missing CSRF protection
- Missing transaction limits
- Insufficient security monitoring

---

# 🛡️ Recommended Remediation Priorities

## Priority 1 — Immediate

- Fix SQL Injection vulnerabilities.
- Implement server-side authorization checks.
- Protect fund-transfer functionality.
- Implement transaction limits.
- Enforce HTTPS.
- Implement strong authentication and MFA.

## Priority 2 — High

- Implement rate limiting and account lockout.
- Implement CSRF protection.
- Fix reflected XSS.
- Upgrade outdated components.
- Disable legacy TLS protocols.

## Priority 3 — Medium

- Remove verbose stack traces.
- Implement secure HTTP headers.
- Reduce information disclosure.
- Improve security logging and monitoring.
- Implement SIEM-based alerting.

---

# 🏁 Conclusion

The assessment identified **13 security findings** across authentication, authorization, input validation, business logic, cryptography, configuration, application components, and monitoring.

The most significant attack chain demonstrated during the assessment was:

**SQL Injection → Authentication Bypass → Broken Access Control → Transaction Manipulation**

The assessment confirmed weaknesses across **8 OWASP Top 10:2021 categories**.

The project demonstrates practical experience in:

- Web application reconnaissance
- Application enumeration
- Manual web security testing
- Authentication testing
- SQL Injection testing
- Broken Access Control testing
- IDOR testing
- XSS testing
- CSRF testing
- Business-logic testing
- Clickjacking testing
- TLS security assessment
- Security-header analysis
- Vulnerability validation
- OWASP mapping
- Risk assessment
- Professional penetration-testing reporting

---

# 💻 Skills Demonstrated

## Web Application Security

- OWASP Top 10:2021
- Authentication Testing
- Authorization Testing
- SQL Injection
- Broken Access Control
- IDOR
- Reflected XSS
- CSRF
- Clickjacking
- Business Logic Testing
- Security Misconfiguration
- Information Disclosure

## Reconnaissance & Enumeration

- Nmap
- WHOIS
- DNS Enumeration
- Subdomain Enumeration
- Service Enumeration
- Web Technology Fingerprinting
- WAF Detection
- TLS/SSL Assessment

## Security Tools

- Burp Suite Community
- Burp Proxy
- Burp Repeater
- Burp Intruder
- SQLMap
- Nmap
- Subfinder
- WhatWeb
- WAFW00F
- sslscan
- WHOIS
- dig

## Reporting Skills

- Vulnerability Documentation
- Proof-of-Concept Development
- CVSS-Based Severity Assessment
- OWASP Mapping
- Risk Analysis
- Impact Analysis
- Remediation Planning
- Attack-Chain Documentation
- Professional Security Reporting

---

# 📂 Project Structure

    Altoro-Mutual-OWASP-Pentest/
    │
    ├── README.md
    │
    ├── Report/
    │   └── Altoro_Mutual_OWASP_Pentest_Report.pdf
    │
    ├── Screenshots/
    │   ├── Reconnaissance/
    │   ├── SQL-Injection/
    │   ├── IDOR/
    │   ├── Brute-Force/
    │   ├── XSS/
    │   ├── CSRF/
    │   ├── Clickjacking/
    │   └── TLS/
    │
    └── Evidence/

---

# ⚠️ Ethical & Legal Disclaimer

This project was performed against **testfire.net**, an intentionally vulnerable application intended for security training and educational purposes.

The techniques documented in this repository must only be used against systems for which explicit authorization has been obtained.

Unauthorized penetration testing, vulnerability exploitation, credential attacks, or data manipulation against real systems may be illegal.

---

## 📥 Detailed Analysis & Documentation
Click the link below to view or download the complete, comprehensive PDF security analysis report:

📁 [**Download Full Penetration Testing PDF Report**](./Web-Application-Penetration-Testing-Report.pdf)


# 👤 Author

## Mahesh Ade - Cybersecurity Student 


