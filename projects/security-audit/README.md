# Security Audit — Botium Toys

## Overview

This project demonstrates the execution of an internal cybersecurity audit for **Botium Toys**, a fictional U.S.-based company with a growing international e-commerce presence.

The objective was to assess the organization's current security posture, identify gaps in existing controls, evaluate compliance risks, and recommend measures to reduce security and business risk.

The assessment was based on the **NIST Cybersecurity Framework (NIST CSF)** and considered administrative, technical, physical, and compliance controls.

---

## Scenario

Botium Toys operates from a single physical location that functions as its office, storefront, and warehouse.

As the company's online business expanded internationally, its IT environment became increasingly important to business operations. The organization therefore needed to evaluate whether its existing security controls were sufficient to protect critical assets and support regulatory compliance.

Particular attention was required for:

- Customer personally identifiable information (PII)
- Payment card information
- Access to sensitive systems
- Business continuity
- Security monitoring
- European customer data
- Online payment processing

---

## Objectives

The security audit focused on:

1. Reviewing the organization's current security controls.
2. Identifying vulnerabilities and control gaps.
3. Evaluating risks to critical systems and data.
4. Assessing relevant compliance requirements.
5. Recommending improvements to strengthen the organization's security posture.

---

## Framework

The assessment used the **NIST Cybersecurity Framework (NIST CSF)** as the primary framework for evaluating cybersecurity risk and security controls.

The audit considered three major categories of controls:

- Administrative / Managerial Controls
- Technical Controls
- Physical / Operational Controls

Compliance considerations included data protection requirements and payment-card security.

---

# Audit Findings

## Administrative / Managerial Controls

| Control | Status | Finding |
|---|---|---|
| Least Privilege | ❌ Gap | Employees had excessive access to sensitive information. |
| Separation of Duties | ❌ Gap | Appropriate separation of privileged responsibilities was not sufficiently established. |
| Disaster Recovery | ❌ Gap | No adequate disaster recovery plan was in place. |
| Password Policy | ❌ Gap | Password requirements did not meet appropriate complexity standards. |
| Account Management | ❌ Gap | Centralized account and password management controls were insufficient. |

---

## Technical Controls

| Control | Status | Finding |
|---|---|---|
| Firewall | ✅ Implemented | A firewall with defined security rules was present. |
| IDS/IPS | ❌ Gap | No intrusion detection system was deployed. |
| Data Encryption | ❌ Critical Gap | Sensitive customer and payment information was not adequately encrypted. |
| Backups | ❌ Critical Gap | Critical data did not have sufficient backup protection. |
| Password Management | ❌ Gap | No centralized password management solution was available. |
| Antivirus | ✅ Implemented | Antivirus protection was installed and monitored. |
| Legacy System Maintenance | ❌ Gap | Legacy systems lacked a regular maintenance and monitoring schedule. |

---

## Physical / Operational Controls

| Control | Status | Finding |
|---|---|---|
| Physical Access Controls | ✅ Implemented | Physical security measures were present. |
| CCTV | ✅ Implemented | Surveillance controls were available. |
| Fire Protection | ✅ Implemented | Fire detection and prevention measures were in place. |

---

# Compliance Assessment

## Data Protection

The assessment identified gaps in the protection of customer PII and other sensitive information.

Because the company serves customers internationally, including customers in the European Union, inadequate protection of personal information could create both cybersecurity and regulatory risk.

### Status

**❌ Requires remediation**

---

## Payment Security

Customer payment information was not sufficiently protected through encryption.

This creates a significant security risk and raises concerns regarding compliance with payment-card security requirements.

### Status

**❌ Requires remediation**

---

# Key Risks

The audit identified several significant risks.

### 1. Sensitive Data Exposure

Insufficient encryption could allow attackers to access customer or payment information if systems were compromised.

**Risk Level: High**

### 2. Excessive Access Privileges

Employees had broader access to sensitive information than necessary.

This increases the potential impact of compromised accounts, insider threats, or accidental data exposure.

**Risk Level: High**

### 3. Lack of Disaster Recovery

Without an established disaster recovery strategy, a ransomware attack, infrastructure failure, or destructive security incident could significantly disrupt business operations.

**Risk Level: High**

### 4. Limited Threat Detection

The absence of IDS/IPS capabilities reduces the organization's ability to detect suspicious or malicious network activity.

**Risk Level: Medium–High**

### 5. Legacy System Exposure

Systems without regular maintenance and monitoring may contain known vulnerabilities that attackers could exploit.

**Risk Level: Medium–High**

---

# Recommendations

Based on the audit findings, the following security improvements should be prioritized.

## Priority 1 — Protect Sensitive Data

Implement encryption for sensitive customer and payment information both **in transit and at rest**.

---

## Priority 2 — Implement Least Privilege

Review employee access rights and restrict access according to business responsibilities.

Introduce:

- Role-Based Access Control (RBAC)
- Periodic access reviews
- Privileged account monitoring
- Separation of duties

---

## Priority 3 — Establish Disaster Recovery

Develop and regularly test:

- Backup procedures
- Disaster recovery plans
- Recovery objectives
- Business continuity procedures

Critical backups should be protected from modification by compromised production systems.

---

## Priority 4 — Improve Authentication

Strengthen authentication controls through:

- Strong password requirements
- Centralized password management
- Multi-factor authentication (MFA)
- Account lifecycle management

---

## Priority 5 — Improve Threat Detection

Deploy and configure:

- Intrusion Detection / Prevention Systems (IDS/IPS)
- Centralized security logging
- Network monitoring
- Security alerts for suspicious activity

---

## Priority 6 — Establish Vulnerability Management

Introduce a recurring process for:

- Vulnerability scanning
- Patch management
- Legacy system reviews
- Security configuration reviews
- Remediation tracking

---

# Skills Demonstrated

This project demonstrates practical knowledge of:

- Security auditing
- Security controls assessment
- Risk identification
- NIST Cybersecurity Framework
- Access control
- Least privilege
- Data protection
- Network security
- IDS/IPS
- Disaster recovery
- Vulnerability management
- Security compliance
- Security recommendations
- Stakeholder communication

---

## Key Takeaway

The assessment demonstrated that cybersecurity audits should evaluate more than individual technical controls.

Security posture depends on the interaction between **people, processes, technology, governance, and business risk**.

The most significant weaknesses identified in this assessment were related to sensitive-data protection, excessive access privileges, disaster recovery, authentication, and threat detection.

Addressing these areas would substantially reduce the organization's attack surface and improve its ability to prevent, detect, respond to, and recover from cybersecurity incidents.
