# Python Security Automation — Access Control Allow-List Management

## Overview

This project demonstrates how Python can automate a simple cybersecurity access-control task.

The objective was to maintain an allow list containing IP addresses authorized to access a restricted network. A separate removal list identifies addresses that should no longer have access.

The Python algorithm reads the existing allow list, removes unauthorized addresses, and updates the file automatically.

---

## Scenario

A healthcare organization restricts access to systems containing sensitive patient information.

Authorized employees are represented by IP addresses stored in:

```text
allow_list.txt
```

When access must be revoked, the corresponding IP addresses are added to a removal list.

The objective is to automatically ensure that addresses marked for removal no longer appear in the allow list.

---

# Security Objective

The workflow implements a basic access-control maintenance process:

```text
Current Allow List
        │
        ▼
Read Authorized IPs
        │
        ▼
Compare Against Removal List
        │
        ▼
Remove Revoked Addresses
        │
        ▼
Write Updated Allow List
        │
        ▼
Access List Updated
```

Automating this process reduces the likelihood of outdated authorization remaining in the access-control file.

---

# Python Implementation

A concise implementation of the complete algorithm is:

```python
import_file = "allow_list.txt"

remove_list = [
    "192.168.97.225",
    "192.168.158.170",
    "192.168.201.40",
    "192.168.58.57"
]

# Read the current allow list
with open(import_file, "r") as file:
    ip_addresses = file.read().split()

# Remove addresses whose access has been revoked
ip_addresses = [
    ip
    for ip in ip_addresses
    if ip not in remove_list
]

# Write the updated allow list
with open(import_file, "w") as file:
    file.write("\n".join(ip_addresses))
```

---

# Step 1 — Define the Input

The filename containing authorized addresses is stored in:

```python
import_file = "allow_list.txt"
```

Addresses requiring removal are stored in a Python list:

```python
remove_list = [
    "192.168.97.225",
    "192.168.158.170",
    "192.168.201.40",
    "192.168.58.57"
]
```

---

# Step 2 — Read the Allow List

The file is opened in read mode:

```python
with open(import_file, "r") as file:
    ip_addresses = file.read()
```

Using a `with` statement ensures that Python manages the file resource and closes it after the operation completes.

---

# Step 3 — Parse the Data

The file contents initially exist as a string.

Using:

```python
ip_addresses = ip_addresses.split()
```

converts the contents into a list of individual IP addresses.

For example:

```text
192.168.1.10
192.168.1.20
192.168.1.30
```

becomes conceptually:

```python
[
    "192.168.1.10",
    "192.168.1.20",
    "192.168.1.30"
]
```

This makes the entries easier to compare and manipulate programmatically.

---

# Step 4 — Remove Revoked Addresses

One approach is to iterate through the addresses and remove entries appearing in the removal list.

A cleaner implementation uses a list comprehension:

```python
ip_addresses = [
    ip
    for ip in ip_addresses
    if ip not in remove_list
]
```

This creates a new list containing only addresses that remain authorized.

---

# Step 5 — Write the Updated File

The list must be converted back into text before being written to the file.

```python
updated_addresses = "\n".join(ip_addresses)
```

The file is then opened in write mode:

```python
with open(import_file, "w") as file:
    file.write(updated_addresses)
```

The existing contents are replaced with the revised allow list.

---

# Example

Assume the original file contains:

```text
192.168.10.15
192.168.97.225
192.168.20.40
192.168.58.57
192.168.30.60
```

and the removal list contains:

```python
[
    "192.168.97.225",
    "192.168.58.57"
]
```

After execution, the file becomes:

```text
192.168.10.15
192.168.20.40
192.168.30.60
```

The revoked addresses are no longer authorized by the file.

---

# Security Principles

## Access Revocation

Access should be removed when it is no longer required.

Examples include:

- Employee departure
- Role changes
- Temporary access expiration
- Compromised accounts or systems
- Changes in authorization

---

## Least Privilege

Maintaining accurate authorization lists supports the principle of least privilege.

Only systems or users with a current business requirement should retain access to restricted resources.

---

## Automation

Manual access-control maintenance can introduce errors.

Automation can improve:

- Consistency
- Repeatability
- Speed
- Scalability

For production systems, additional validation, logging, error handling, identity-based controls, and change management would normally be required.

---

# Potential Improvements

A production-oriented implementation could include:

### Input Validation

Validate that entries are legitimate IP addresses before processing them.

### Logging

Record which entries were removed and when the change occurred.

### Error Handling

Handle situations such as:

- Missing files
- Permission errors
- Invalid data
- Failed write operations

### Backup Before Modification

Create a backup before replacing the authorization file.

### Audit Trail

Record authorization changes for later security review.

### Identity-Based Access Control

IP allow lists alone are generally insufficient for strong identity verification.

A production security architecture should combine network restrictions with appropriate authentication and authorization controls.

---

# Skills Demonstrated

This project demonstrates practical knowledge of:

- Python
- Security automation
- File handling
- Access-control maintenance
- Lists
- List comprehensions
- Conditional logic
- Data parsing
- File modification
- Least privilege
- Access revocation
- Security process automation

---

## Key Takeaway

Simple automation can improve security operations by making repetitive access-control tasks more consistent and less error-prone.

The core workflow is:

```text
Read → Parse → Compare → Remove → Update
```

While this example is intentionally simple, the same principle can be extended to larger security-automation workflows involving IAM systems, APIs, asset inventories, security policies, and automated remediation.
