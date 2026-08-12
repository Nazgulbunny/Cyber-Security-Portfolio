# SOC Incident Investigation — Incident Handler's Journal

## Overview

This project documents several security investigation activities from the perspective of a Security Operations Center (SOC) analyst.

The exercises cover multiple stages of security operations, including:

- Incident documentation
- Phishing investigation
- Ransomware analysis
- Network traffic analysis
- Packet capture
- Indicator-of-compromise investigation
- Malware reputation analysis

Tools used across the investigations included **Wireshark, tcpdump, VirusTotal, and Splunk**.

---

# Investigation 1 — Ransomware Incident

## Incident Summary

A healthcare organization experienced a ransomware incident that prevented employees from accessing critical files and medical records.

The attack began with targeted phishing emails containing malicious attachments.

After an employee executed the attachment, malware was installed and the attackers gained access to the environment.

Ransomware was subsequently deployed and critical files were encrypted.

A ransom note demanded payment in exchange for a decryption key.

---

## Incident Timeline

```text
Phishing Email
      │
      ▼
Malicious Attachment
      │
      ▼
Employee Executes File
      │
      ▼
Malware Infection
      │
      ▼
Attacker Access
      │
      ▼
Ransomware Deployment
      │
      ▼
Critical Files Encrypted
      │
      ▼
Business Operations Disrupted
```

---

# The 5 W's

## Who?

An organized malicious group targeting organizations in sectors including healthcare and transportation.

## What?

Attackers used phishing emails containing malicious attachments to gain access to the environment and deploy ransomware.

Critical files were encrypted and a ransom was demanded for the decryption key.

## When?

The incident became apparent on a Tuesday morning at approximately **09:00**.

## Where?

The incident affected systems within a small U.S. healthcare clinic.

Employee workstations and access to critical patient information were disrupted.

## Why?

The initial access vector was a malicious email attachment executed by an employee.

The provided scenario does not establish whether additional security-control failures contributed to the compromise.

---

# Security Impact

The incident primarily affected:

### Availability

Employees could not access critical medical records or systems required for business operations.

### Integrity

The ransomware modified the state of organizational files by encrypting them without authorization.

### Confidentiality

The scenario does not establish whether patient information was exfiltrated.

Further investigation would therefore be required before concluding that confidentiality was compromised.

---

# Investigation Priorities

Following containment, several questions would need to be answered:

- Which endpoints were compromised?
- Which user executed the malicious attachment?
- What malware was delivered?
- Did the attacker establish persistence?
- Did the attacker move laterally?
- Were credentials compromised?
- Was sensitive information exfiltrated?
- Which files were encrypted?
- Are clean backups available?
- What indicators of compromise can be identified?

---

# Investigation 2 — Packet Analysis with Wireshark

## Objective

Use Wireshark to inspect captured network traffic and understand communication between systems.

Wireshark allows analysts to examine individual packets and inspect information such as:

- Source IP address
- Destination IP address
- Protocol
- Ports
- TCP flags
- Packet payloads where available
- Communication sequences

---

## Security Applications

Packet analysis can help investigate:

- Suspicious outbound connections
- Unexpected protocols
- Malware communication
- Network scanning
- Authentication activity
- DNS requests
- Command-and-control indicators

---

# Investigation 3 — Packet Capture with tcpdump

## Objective

Use `tcpdump` from the Linux command line to capture and inspect network traffic.

Unlike Wireshark's graphical interface, tcpdump provides command-line packet capture and filtering capabilities.

Example:

```bash
sudo tcpdump -i eth0
```

Traffic can also be filtered.

For example:

```bash
sudo tcpdump -i eth0 port 53
```

focuses on traffic using port 53.

---

## Security Applications

tcpdump can support:

- Incident investigation
- Network troubleshooting
- Protocol analysis
- DNS investigation
- Suspicious connection analysis
- Packet collection for later analysis

Captured traffic can also be saved for further investigation:

```bash
sudo tcpdump -i eth0 -w capture.pcap
```

The resulting `.pcap` file can subsequently be analyzed using tools such as Wireshark.

---

# Investigation 4 — Malicious File Hash Analysis

## Scenario

A security alert identified a suspicious file associated with an email attachment at a financial services organization.

The file was represented by the following SHA-256 hash:

```text
54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b
```

The objective was to determine whether the file represented a known security threat.

---

## Tool

**VirusTotal**

VirusTotal can aggregate detections and analysis from multiple security vendors and data sources.

Rather than executing a suspicious file, analysts can investigate known indicators such as cryptographic hashes.

---

## Investigation Workflow

```text
Security Alert
      │
      ▼
Suspicious File
      │
      ▼
Calculate / Obtain SHA-256
      │
      ▼
Search Reputation Sources
      │
      ▼
VirusTotal Analysis
      │
      ▼
Evaluate Detection Results
      │
      ▼
Correlate With Other Evidence
      │
      ▼
Determine Response
```

---

## Finding

The supplied file hash was identified as malicious during the exercise.

This finding provided additional evidence supporting escalation of the security alert.

A reputation result should still be considered alongside other evidence such as:

- Endpoint telemetry
- Email metadata
- Network connections
- Process execution
- File behavior
- Authentication logs

---

# Investigation 5 — Log Analysis with Splunk

Splunk was used to explore security-event data and search logs for information relevant to an investigation.

A SIEM platform can help analysts correlate information from multiple sources such as:

```text
Firewall Logs ───────┐
Authentication Logs ─┤
Endpoint Logs ───────┤
DNS Logs ────────────┼──► SIEM ──► Investigation
Application Logs ────┤
IDS/IPS Alerts ──────┤
Cloud Logs ──────────┘
```

Centralizing these events allows analysts to search across systems and identify relationships that may not be obvious when individual logs are reviewed separately.

---

# Incident Investigation Lifecycle

The activities demonstrate a simplified SOC investigation process:

```text
          Alert
            │
            ▼
         Triage
            │
            ▼
     Evidence Collection
            │
            ▼
         Analysis
            │
            ▼
       Correlation
            │
            ▼
    Incident Confirmation
            │
            ▼
       Containment
            │
            ▼
      Remediation
            │
            ▼
        Recovery
            │
            ▼
     Lessons Learned
```

---

# Lessons Learned

## Evidence Before Conclusions

Security analysts should distinguish between what the available evidence proves and what remains a hypothesis.

For example, a ransomware incident does not automatically prove that sensitive information was stolen.

Additional evidence is required to establish data exfiltration.

---

## Multiple Data Sources Matter

Effective investigations often require correlating information from:

- Network packets
- Endpoint activity
- File hashes
- Authentication events
- Security alerts
- Email records
- System logs

No individual data source necessarily provides the complete attack story.

---

## Documentation Matters

Maintaining an incident journal creates a chronological record of:

- Findings
- Evidence
- Actions
- Decisions
- Open questions

This improves communication between analysts and supports later incident review.

---

# Skills Demonstrated

This project demonstrates knowledge of:

- Security Operations Center workflows
- Incident response
- Incident documentation
- Ransomware
- Phishing
- Network traffic analysis
- Wireshark
- tcpdump
- VirusTotal
- Splunk
- SHA-256 hashes
- Indicators of compromise
- SIEM concepts
- Evidence correlation
- Incident triage
- Root-cause investigation

---

## Key Takeaway

Security investigations are rarely solved using a single tool.

Network traffic, endpoint evidence, file reputation, authentication events, and centralized logs each provide different pieces of information.

The analyst's role is to correlate those pieces, distinguish evidence from assumptions, document findings clearly, and use the resulting information to support containment and remediation.
