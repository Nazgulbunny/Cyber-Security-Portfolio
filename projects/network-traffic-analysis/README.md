# Network Traffic Analysis — DNS and ICMP Incident

## Overview

This project demonstrates the analysis of network traffic during a website connectivity incident.

Using `tcpdump` output, I investigated DNS requests, UDP traffic, and ICMP error messages to determine why users were unable to access a website.

The goal was to identify the affected protocol and service, interpret the packet data, determine the likely cause of the issue, and recommend remediation steps.

---

## Scenario

Users attempting to access:

`www.yummyrecipesforme.com`

received a:

`destination port unreachable`

error.

To investigate the issue, network traffic was captured while attempting to load the website.

The browser attempted to resolve the domain name through DNS before establishing a connection to the web server.

---

## Tools and Protocols

This investigation involved:

- tcpdump
- DNS
- UDP
- ICMP
- TCP/IP
- Port analysis
- Packet inspection

---

# Traffic Analysis

The captured traffic showed DNS queries being sent from the client machine to a DNS server using UDP.

DNS normally uses:

**UDP port 53**

The client sent DNS requests to the configured DNS server, but instead of receiving a DNS response, the system received ICMP error messages.

The key message in the packet capture was:

```text
udp port 53 unreachable
```

This indicated that the DNS request could not be delivered successfully to the expected DNS service.

---

## Packet Flow

The sequence of events was:

1. The browser attempted to access the website.
2. The system generated a DNS query.
3. The DNS query was sent using UDP to port 53.
4. The DNS server did not process the request successfully.
5. An ICMP error message was returned.
6. DNS resolution failed.
7. Because the domain could not be resolved, the browser could not continue to the web server.

---

# Findings

## Affected Service

**DNS**

## Transport Protocol

**UDP**

## Destination Port

**53**

## Diagnostic Protocol

**ICMP**

## Error

```text
udp port 53 unreachable
```

---

# Interpretation

The ICMP response indicates that the UDP packet reached a system that could not accept traffic on the requested destination port.

This suggests that the DNS service was unavailable or that network controls prevented the DNS query from reaching a functioning DNS service.

Potential causes include:

- DNS service failure
- DNS server misconfiguration
- Firewall rules blocking UDP port 53
- Incorrect network configuration
- DNS service not listening on the expected interface or port

---

# Impact

Because DNS resolution failed, users could not resolve the website's domain name to an IP address.

This prevented access to the website even if the web server itself was still operational.

The incident therefore caused a service availability issue at the name-resolution layer.

---

# Recommended Actions

## 1. Verify DNS Service Availability

Confirm that the DNS service is running and listening on UDP port 53.

---

## 2. Review Firewall Rules

Check whether UDP traffic on port 53 is being blocked by:

- Host firewalls
- Network firewalls
- Security appliances
- Cloud security rules

---

## 3. Review DNS Server Logs

Inspect DNS logs for:

- Service failures
- Configuration errors
- Restart events
- Blocked requests
- Resource exhaustion

---

## 4. Test an Alternative DNS Resolver

Temporarily query another DNS server to determine whether the issue is isolated to the original resolver.

---

## 5. Implement Monitoring

Add monitoring for:

- DNS service availability
- DNS query failures
- Increased ICMP unreachable responses
- Port 53 connectivity

---

# Root Cause Assessment

Based on the available packet data, the strongest conclusion is that DNS requests sent over UDP port 53 were not being accepted by the destination system.

The packet capture alone does not prove whether the underlying cause was:

- a failed DNS service,
- a firewall rule,
- or another configuration problem.

Further server-side and firewall investigation would therefore be required to confirm the exact root cause.

---

# Skills Demonstrated

This project demonstrates knowledge of:

- Network traffic analysis
- tcpdump
- DNS
- UDP
- ICMP
- TCP/IP
- Port identification
- Incident investigation
- Network troubleshooting
- Root cause analysis
- Security monitoring
- Technical reporting

---

## Key Takeaway

Packet captures can reveal where communication is failing even when the application-level symptom is simply that a website does not load.

In this case, the key evidence was not the browser error itself, but the ICMP response indicating that UDP port 53 was unreachable.

This allowed the investigation to identify DNS resolution as the affected service and narrow the troubleshooting scope significantly.
