# DDoS Incident Response Using the NIST Cybersecurity Framework

## Overview

This project demonstrates how the **NIST Cybersecurity Framework (NIST CSF)** can be applied to analyze and improve an organization's response to a cybersecurity incident.

The scenario involves a Distributed Denial-of-Service (DDoS) attack in which a flood of ICMP packets overwhelmed an organization's internal network.

The incident is analyzed through five NIST CSF functions:

**Identify → Protect → Detect → Respond → Recover**

---

## Scenario

A multimedia company experienced a two-hour network outage caused by an unusually large volume of incoming ICMP traffic.

During the attack:

- Internal network services stopped responding.
- Legitimate users could not access network resources.
- Critical business services were disrupted.
- The incident-response team temporarily disabled non-critical services.
- Incoming ICMP traffic was blocked while critical services were restored.

The subsequent investigation determined that an attacker had exploited an inadequately configured firewall and generated a large volume of ICMP traffic against the organization's network.

---

# Attack Overview

```text
      Distributed Attack Sources
                 │
                 ▼
         ICMP Packet Flood
                 │
                 ▼
      Misconfigured Firewall
                 │
                 ▼
        Internal Network
                 │
                 ▼
        Resource Exhaustion
                 │
                 ▼
      Legitimate Traffic Fails
                 │
                 ▼
         Service Outage
```

---

# Security Impact

The primary security property affected was:

## Availability

The volume of malicious traffic prevented legitimate users from accessing network resources.

Potential business consequences included:

- Service interruption
- Reduced employee productivity
- Customer impact
- Operational costs
- Incident-response costs
- Potential reputational damage

---

# NIST CSF Analysis

## 1. Identify

The organization should maintain a clear understanding of its assets, network architecture, business dependencies, and cybersecurity risks.

Recommended activities include:

- Maintain an inventory of network devices and systems.
- Document critical business services.
- Map network architecture and dependencies.
- Review firewall configurations.
- Identify internet-facing infrastructure.
- Perform regular vulnerability assessments.
- Review access privileges.
- Conduct periodic security audits.

### Objective

Understand **what must be protected and where vulnerabilities exist** before an incident occurs.

---

## 2. Protect

Preventive controls should reduce the probability and potential impact of similar attacks.

Recommended controls include:

- Harden firewall configurations.
- Apply ICMP rate limiting.
- Implement source-address validation where appropriate.
- Maintain secure configuration baselines.
- Patch network infrastructure.
- Apply least privilege.
- Protect administrative interfaces.
- Implement appropriate network segmentation.
- Maintain security policies and procedures.

### Objective

Reduce the organization's **attack surface and exposure to known threats**.

---

## 3. Detect

The organization should identify abnormal network activity as early as possible.

Detection capabilities should include:

- Network traffic monitoring
- Firewall logging
- IDS/IPS
- Traffic baselining
- Automated alerting
- Detection of unusual ICMP volumes
- Detection of abnormal source patterns

For example:

```text
Normal ICMP Traffic
       │
       ▼
Network Monitoring
       │
       ├── Normal → Continue monitoring
       │
       └── Abnormal spike
                 │
                 ▼
             Security Alert
```

### Objective

Reduce the time between **attack initiation and detection**.

---

## 4. Respond

Once malicious activity is detected, the organization should contain the incident and restore critical capabilities as quickly as possible.

Actions during this incident included:

- Blocking malicious ICMP traffic
- Temporarily disabling non-critical services
- Prioritizing critical services
- Investigating network traffic
- Correcting firewall configuration

A structured response process should also include:

- Incident classification
- Escalation procedures
- Evidence preservation
- Technical investigation
- Internal communication
- Stakeholder communication
- Documentation of response actions

### Objective

**Contain, analyze, and neutralize the incident while minimizing business impact.**

---

## 5. Recover

Recovery focuses on returning affected systems and services to normal operation.

Activities should include:

- Restore network services.
- Validate system functionality.
- Confirm firewall changes are operating correctly.
- Monitor for recurring attack traffic.
- Review affected systems.
- Document lessons learned.
- Update incident-response procedures.
- Improve security controls based on the investigation.

### Objective

Restore normal operations while reducing the probability and impact of recurrence.

---

# Security Improvements Implemented

Following the incident, the network security team introduced several controls.

## ICMP Rate Limiting

Firewall rules were configured to restrict excessive incoming ICMP traffic.

This helps prevent large volumes of ICMP packets from consuming network resources.

---

## Source IP Verification

Source-address verification was implemented to help identify and reject traffic using invalid or spoofed source addresses.

---

## Network Monitoring

Monitoring capabilities were introduced to identify abnormal traffic patterns.

Establishing a baseline for normal traffic makes unusual spikes easier to detect.

---

## IDS/IPS

An Intrusion Detection/Prevention System was introduced to identify and filter suspicious traffic based on configured detection logic.

---

# Defense-in-Depth Strategy

The incident demonstrates why multiple controls should operate together.

```text
        Internet
           │
           ▼
   DDoS / Traffic Filtering
           │
           ▼
        Firewall
     + Rate Limiting
           │
           ▼
        IDS / IPS
           │
           ▼
   Network Segmentation
           │
           ▼
   Critical Infrastructure
           │
           ▼
   Monitoring + Alerting
```

No individual control completely eliminates DDoS risk.

Layered controls increase resilience and provide multiple opportunities to detect or limit malicious traffic.

---

# Lessons Learned

The attack succeeded because a network-security control was not adequately configured.

This demonstrates that deploying security technology is not sufficient by itself.

Security controls must also be:

- Correctly configured
- Regularly reviewed
- Continuously monitored
- Tested
- Updated as infrastructure and threats evolve

---

# Skills Demonstrated

This project demonstrates knowledge of:

- NIST Cybersecurity Framework
- Incident response
- DDoS attacks
- ICMP
- Firewall security
- IDS/IPS
- Network monitoring
- Traffic baselining
- Security controls
- Defense in depth
- Incident containment
- Recovery planning
- Security risk management

---

## Key Takeaway

The NIST Cybersecurity Framework provides a structured way to think about cybersecurity beyond simply responding to individual attacks.

Using:

**Identify → Protect → Detect → Respond → Recover**

allows an organization to connect technical incident response with broader risk management, prevention, monitoring, operational resilience, and continuous security improvement.
