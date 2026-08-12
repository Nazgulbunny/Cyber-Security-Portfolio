# Network Hardening — Security Risk Assessment

## Overview

This project evaluates the security posture of a fictional social media organization following a major data breach.

The objective was to identify weaknesses in the organization's network and authentication controls, assess the risks created by those weaknesses, and recommend security-hardening measures to reduce the likelihood of future compromise.

---

## Scenario

Following a breach involving customer personal information, a security review identified four significant weaknesses:

- Employees shared passwords.
- The database administrator account still used its default password.
- Firewall rules did not adequately filter inbound and outbound traffic.
- Multi-factor authentication (MFA) was not implemented.

These weaknesses increased the organization's exposure to unauthorized access, credential compromise, network attacks, and further data breaches.

---

# Security Findings

| Finding | Risk | Priority |
|---|---|---|
| Shared employee passwords | Unauthorized access and lack of accountability | High |
| Default database administrator password | Privileged account compromise | Critical |
| Inadequate firewall rules | Unauthorized or malicious network traffic | High |
| MFA not implemented | Account takeover following credential compromise | High |

---

# Risk Analysis

## 1. Default Administrative Credentials

The database administrator account used a default password.

Default credentials represent a critical security weakness because they may be publicly documented, reused across installations, or included in automated credential attacks.

Successful compromise could provide an attacker with privileged access to sensitive systems and customer information.

**Risk: Critical**

---

## 2. Shared Passwords

Password sharing prevents reliable attribution of actions to individual users and increases the likelihood of credential exposure.

It also makes credential revocation more difficult because changing a shared credential may affect multiple users.

**Risk: High**

---

## 3. Inadequate Firewall Configuration

The firewall did not contain sufficient rules for filtering inbound and outbound network traffic.

Without appropriate filtering, unnecessary services and network paths may remain exposed to attackers.

**Risk: High**

---

## 4. Lack of Multi-Factor Authentication

Authentication relied primarily on passwords.

If an attacker obtained a valid password through phishing, credential reuse, password guessing, or another technique, there was no additional authentication factor protecting the account.

**Risk: High**

---

# Recommended Hardening Measures

## 1. Secure Baseline Configurations

Establish hardened baseline configurations for systems and network devices.

Baselines should define approved security settings including:

- Authentication requirements
- Network configuration
- Enabled services
- Logging
- Access controls
- Patch requirements
- Firewall configuration

Systems can then be regularly compared against the approved baseline to detect configuration drift.

---

## 2. Strengthen Firewall Configuration

Implement explicit firewall policies based on business requirements and the principle of least privilege.

Firewall rules should:

- Permit only required inbound traffic.
- Restrict unnecessary outbound communication.
- Remove obsolete rules.
- Document business justification.
- Be reviewed periodically.
- Generate logs for relevant security events.

---

## 3. Reduce Exposed Services

Unused ports and unnecessary services should be disabled.

Reducing unnecessary services decreases the system's attack surface and limits opportunities for attackers to exploit vulnerable or incorrectly configured services.

---

## 4. Implement MFA

Multi-factor authentication should be required for sensitive systems, particularly:

- Administrative accounts
- Remote access
- Database administration
- Security systems
- Privileged operations

MFA significantly reduces the usefulness of stolen passwords.

---

## 5. Eliminate Default Credentials

All default passwords should be changed before a system enters production.

Administrative credentials should be:

- Unique
- Strong
- Securely stored
- Regularly reviewed
- Restricted to authorized personnel

---

## 6. Eliminate Password Sharing

Every user should have an individually identifiable account.

This improves:

- Accountability
- Auditability
- Access revocation
- Incident investigation
- Least-privilege enforcement

---

# Defense in Depth

The identified weaknesses should not be addressed independently.

A stronger security architecture combines multiple defensive layers:

```text
                    Users
                      │
                      ▼
             Strong Authentication
                 + MFA
                      │
                      ▼
                Access Control
                      │
                      ▼
              Firewall Policies
                      │
                      ▼
              Hardened Systems
                      │
                      ▼
           Monitoring + Logging
                      │
                      ▼
             Protected Data
```

If one defensive layer fails, additional controls can still limit the attacker's ability to compromise sensitive systems.

---

# Maintenance Strategy

Security hardening is not a one-time activity.

The organization should establish recurring processes for:

- Firewall rule reviews
- Vulnerability scanning
- Patch management
- Access reviews
- Configuration auditing
- Privileged account reviews
- Security monitoring

Significant infrastructure changes should also trigger security configuration reviews.

---

# Skills Demonstrated

This project demonstrates knowledge of:

- Network hardening
- Security risk assessment
- Firewall security
- Attack-surface reduction
- Secure configuration
- Multi-factor authentication
- Password security
- Privileged access
- Least privilege
- Defense in depth
- Security monitoring
- Configuration management

---

## Key Takeaway

Network hardening requires both technical and identity-related controls.

Firewall configuration and reducing unnecessary network exposure are important, but they cannot compensate for weak authentication or compromised privileged accounts.

Combining secure configuration, MFA, individual accountability, least privilege, firewall controls, and continuous monitoring provides a substantially stronger defensive posture.
