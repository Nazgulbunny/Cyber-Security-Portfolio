# Web Server Compromise — Brute-Force Attack Investigation

## Overview

This project investigates the compromise of a web application following unauthorized access to an administrative account.

The incident involved a brute-force attack against a default administrator password, modification of website source code, delivery of a malicious executable, and redirection of users to a fraudulent website.

The investigation used network traffic evidence and incident information to reconstruct the attack and recommend security controls.

---

## Scenario

Users visiting:

`yummyrecipesforme.com`

reported being prompted to download a supposed browser update.

After executing the downloaded file:

- Their computers became slower.
- Their browsers redirected to another website.
- The fraudulent website imitated the legitimate service.

The website administrator was also unable to access the administration panel.

Investigation determined that an attacker had successfully compromised the administrative account.

---

# Attack Chain

The incident can be represented as:

```text
Default Admin Password
        ↓
Brute-Force Attack
        ↓
Administrative Access
        ↓
Website Source Code Modified
        ↓
Malicious JavaScript Added
        ↓
Visitor Opens Website
        ↓
Malicious File Download Prompt
        ↓
Executable Runs
        ↓
Browser Redirected
        ↓
Fraudulent Website
```

---

# Root Cause

The primary security weakness was the continued use of a **default administrator password**.

The environment also lacked adequate controls for preventing repeated authentication attempts.

This allowed the attacker to repeatedly attempt known/default credentials until gaining administrative access.

---

# Network Analysis

The captured traffic showed several important stages.

## 1. DNS Resolution

The client first requested DNS resolution for:

```text
yummyrecipesforme.com
```

The DNS server returned the legitimate site's IP address.

---

## 2. HTTP Connection

The browser established a TCP connection to the web server and generated an HTTP request.

```text
HTTP: GET / HTTP/1.1
```

The packet capture confirms web communication over HTTP.

It does **not**, by itself, establish that this specific GET request contained the malicious JavaScript. The malicious code was confirmed separately through analysis of the compromised website's source code.

---

## 3. Malicious Download

The compromised website prompted visitors to download and execute a malicious file disguised as a browser update.

---

## 4. Secondary DNS Resolution

After execution, another DNS request was generated for:

```text
greatrecipesforme.com
```

The DNS server resolved the fraudulent domain to another IP address.

---

## 5. Redirected Web Traffic

The browser subsequently established an HTTP connection to the fraudulent website.

This network sequence supported the finding that users were being redirected away from the legitimate service.

---

# Protocols Identified

| Protocol | Purpose |
|---|---|
| DNS | Resolve domain names into IP addresses |
| TCP | Establish reliable network connections |
| HTTP | Transfer web content |
| IP | Route packets between systems |

---

# Security Impact

The compromise affected several elements of the CIA security model.

### Confidentiality

The attacker obtained unauthorized administrative access.

### Integrity

The attacker modified the legitimate website's source code.

### Availability

The legitimate administrator lost access to the administration interface and normal website operations were disrupted.

---

# Immediate Response

Recommended immediate actions include:

1. Disable or reset the compromised administrator account.
2. Remove the malicious JavaScript from the website.
3. Remove malicious files from the hosting environment.
4. Reset administrative credentials.
5. Review authentication and web-server logs.
6. Identify potentially affected users.
7. Investigate the downloaded executable.
8. Preserve relevant logs and evidence for further investigation.

---

# Preventive Controls

## Multi-Factor Authentication

Administrative accounts should require MFA.

A compromised password alone would therefore not normally be sufficient to access the administration interface.

---

## Remove Default Credentials

Default passwords should be changed before systems are exposed to production environments.

---

## Brute-Force Protection

Authentication systems should implement controls such as:

- Rate limiting
- Progressive delays
- Account lockout policies where appropriate
- Suspicious-login detection
- Authentication monitoring

---

## Strong Authentication Policies

Administrative credentials should use long, unique passwords and should be managed securely.

---

## File Integrity Monitoring

Changes to sensitive web application files should generate security alerts.

Unexpected modification of production JavaScript or other application resources could then be detected more quickly.

---

## Security Logging

Authentication and administrative actions should be centrally logged and monitored for:

- Repeated failed login attempts
- Successful login after numerous failures
- Administrative changes
- Source-code modifications
- Unusual administrator locations or devices

---

## HTTPS

Internet-facing production websites should use HTTPS rather than transmitting web traffic over unencrypted HTTP.

---

# Skills Demonstrated

This project demonstrates knowledge of:

- Incident investigation
- Brute-force attacks
- Web security
- Authentication security
- Network traffic analysis
- DNS
- TCP/IP
- HTTP
- Malware delivery
- File integrity
- Multi-factor authentication
- Incident containment
- Root-cause analysis

---

## Key Takeaway

The incident demonstrates how a seemingly simple security weakness—a default administrative password—can lead to a much larger compromise.

Once privileged access was obtained, the attacker was able to alter trusted website content and use the legitimate service as part of the malware delivery chain.

The most effective defense is therefore not a single control, but layered security combining strong authentication, MFA, brute-force protection, monitoring, secure configuration, and file-integrity controls.
