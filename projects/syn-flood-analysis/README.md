# SYN Flood Attack Analysis

## Overview

This project investigates a network service disruption caused by an abnormal volume of TCP SYN requests targeting a web server.

The objective was to analyze the observed network behavior, identify the likely attack technique, explain how it affected service availability, and recommend defensive measures.

---

## Scenario

A travel company's monitoring system generated an alert indicating problems with its web server.

Users attempting to access the company website experienced connection timeouts.

Packet analysis revealed a large number of TCP SYN requests originating from an unfamiliar IP address. The server became overwhelmed and was increasingly unable to respond to legitimate connection requests.

As an immediate containment measure, the affected server was temporarily taken offline and the suspicious source IP address was blocked.

---

## Tools and Concepts

- TCP/IP
- TCP three-way handshake
- SYN packets
- Packet analysis
- Firewalls
- IDS/IPS
- Denial-of-Service (DoS)
- Network monitoring

---

# Investigation

Normal TCP connections are established through a three-way handshake:

```text
Client                    Server

   SYN  -------------------->
        <---------------- SYN-ACK
   ACK  -------------------->

        Connection established
```

During the incident, the server received an abnormally large number of SYN packets.

Instead of completing the handshake, the incoming requests left connections incomplete.

---

# Attack Identification

The observed behavior was consistent with a:

## TCP SYN Flood

A SYN flood is a form of Denial-of-Service attack that abuses the TCP connection-establishment process.

The attacker generates large numbers of SYN requests without successfully completing the TCP handshake.

The server must temporarily maintain state for these incomplete connections while waiting for the final ACK.

If enough half-open connections accumulate, resources available for legitimate clients can become exhausted.

---

# Impact

The attack affected the **availability** of the web service.

Potential consequences included:

- Website connection timeouts
- Degraded server performance
- Legitimate connections being rejected or delayed
- Business disruption
- Lost customer activity
- Potential revenue loss
- Reputational damage
- Increased incident-response costs

From the CIA security model, the primary property affected was:

**Availability**

---

# DoS vs. DDoS

A traditional **Denial-of-Service (DoS)** attack can originate from a single attacking system.

A **Distributed Denial-of-Service (DDoS)** attack uses multiple systems to generate malicious traffic against the target.

Based solely on the scenario's observation of traffic from an unfamiliar IP address, the available evidence supports identifying the activity as a SYN-flood DoS attack. Additional evidence would be required to determine whether the attack was distributed.

---

# Immediate Response

During the incident, two containment actions were taken:

1. Temporarily remove the affected server from service so it could recover.
2. Block the identified source IP address at the firewall.

Blocking the source IP provides short-term containment but should not be considered sufficient long-term protection because attackers may change or spoof source addresses.

---

# Recommended Mitigations

## 1. SYN Cookies

Enable SYN cookies where appropriate to reduce resource allocation for incomplete TCP handshakes.

---

## 2. Connection Rate Limiting

Limit abnormal connection rates to prevent individual sources from creating excessive numbers of connection requests.

---

## 3. Firewall Protection

Configure firewall policies capable of detecting and limiting abnormal SYN traffic.

---

## 4. IDS/IPS Monitoring

Deploy detection rules for unusual TCP connection patterns, including:

- Large SYN spikes
- Excessive half-open connections
- Abnormal connection rates

---

## 5. Network Monitoring

Establish baselines for normal network traffic and alert when SYN traffic or connection attempts significantly exceed expected levels.

---

## 6. DDoS Mitigation

For internet-facing critical services, consider upstream or managed DDoS protection capable of absorbing or filtering high-volume attacks before they reach the application infrastructure.

---

# Skills Demonstrated

This project demonstrates knowledge of:

- TCP/IP
- TCP three-way handshake
- SYN flood attacks
- Denial-of-Service attacks
- Packet analysis
- Network incident investigation
- Firewall controls
- IDS/IPS
- Network monitoring
- Incident containment
- Availability risk
- Security mitigation strategies

---

## Key Takeaway

Understanding normal protocol behavior is fundamental to identifying malicious network activity.

The TCP three-way handshake normally establishes reliable connections between clients and servers. A SYN flood weaponizes this legitimate mechanism by creating excessive incomplete connections.

Recognizing the difference between expected and abnormal protocol behavior allows security analysts to identify the attack and select appropriate defensive controls.
