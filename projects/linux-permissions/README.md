# Linux Security — File and Directory Permissions

## Overview

This project demonstrates the use of Linux file permissions to enforce appropriate access controls within a research environment.

The objective was to inspect existing file and directory permissions, identify access that violated organizational security requirements, and modify those permissions using Linux commands.

The exercise demonstrates practical application of:

- Linux permissions
- `ls`
- `chmod`
- Least privilege
- User and group access control

---

## Scenario

A research team stores project files under:

```text
/home/researcher2/projects
```

As part of a security review, file and directory permissions needed to be examined to ensure that users had only the access required for their roles.

The goal was to identify excessive permissions and remove unauthorized access.

---

# Inspecting Permissions

The first step was to inspect the directory:

```bash
ls -la /home/researcher2/projects
```

The `-l` option displays detailed file information, including permissions, ownership, group membership, file size, and modification information.

The `-a` option also displays hidden files.

Example permission strings included:

```text
-rw-rw-rw-  project_k.txt
-rw-r-----  project_m.txt
-rw-rw-r--  project_r.txt
-rw-rw-r--  project_t.txt
-rw-w-----  .project_x.txt
drwx--x---  drafts
```

---

# Understanding Linux Permissions

Consider:

```text
-rw-rw-rw-
```

Linux permissions can be divided into four sections:

```text
- | rw- | rw- | rw-
    │      │      │
    │      │      └── Others
    │      └───────── Group
    └──────────────── User / Owner
```

The first character describes the object type:

```text
- = regular file
d = directory
l = symbolic link
```

The remaining characters represent:

```text
r = read
w = write
x = execute
- = permission not granted
```

Therefore:

```text
-rw-rw-rw-
```

means:

| Identity | Read | Write | Execute |
|---|---|---|---|
| Owner | Yes | Yes | No |
| Group | Yes | Yes | No |
| Others | Yes | Yes | No |

---

# Remediation

## Remove Write Access for Others

The organization's policy did not allow users outside the owner/group to modify `project_k.txt`.

Existing permissions:

```text
-rw-rw-rw-
```

The following command removes write permission from **others**:

```bash
chmod o-w /home/researcher2/projects/project_k.txt
```

Result:

```text
-rw-rw-r--
```

---

# Hidden File Permissions

The hidden file:

```text
.project_x.txt
```

required restricted permissions.

If the requirement is for the owner and group to have **read-only** access, with no permissions for others, the desired permissions are:

```text
-r--r-----
```

This can be configured symbolically:

```bash
chmod u=r,g=r,o= /home/researcher2/projects/.project_x.txt
```

or numerically:

```bash
chmod 440 /home/researcher2/projects/.project_x.txt
```

---

# Directory Permissions

The `drafts` directory needed to be accessible only by its owner.

The desired permissions are:

```text
drwx------
```

This can be configured using:

```bash
chmod 700 /home/researcher2/projects/drafts
```

or:

```bash
chmod u=rwx,g=,o= /home/researcher2/projects/drafts
```

This gives the owner:

- Read
- Write
- Execute

while removing all permissions from the group and others.

---

# Verification

After modifying permissions, the configuration should be verified:

```bash
ls -la /home/researcher2/projects
```

The relevant entries should now reflect the intended authorization.

For example:

```text
-rw-rw-r--  project_k.txt
-r--r-----  .project_x.txt
drwx------  drafts
```

Verification is an important part of security administration because executing a command does not automatically guarantee that the resulting configuration matches the intended security policy.

---

# Security Principles Applied

## Least Privilege

Users should receive only the permissions required to perform their responsibilities.

Removing unnecessary write or directory access reduces the possibility of unauthorized modification or disclosure.

---

## Access Control

Linux filesystem permissions provide discretionary access control through three primary identities:

```text
User
Group
Others
```

Permissions can then control:

```text
Read
Write
Execute
```

---

## Attack-Surface Reduction

Excessive filesystem permissions can enable unauthorized users to:

- Read sensitive information
- Modify files
- Delete information
- Execute files
- Access restricted directories

Restricting permissions reduces these opportunities.

---

# Skills Demonstrated

This project demonstrates practical knowledge of:

- Linux
- Linux filesystem permissions
- `ls`
- `chmod`
- Symbolic permissions
- Numeric/octal permissions
- Hidden files
- Directory permissions
- Access control
- Least privilege
- Security configuration
- Verification of security changes

---

## Key Takeaway

Linux file permissions provide a simple but important security boundary.

Effective permission management requires three steps:

```text
Inspect → Remediate → Verify
```

Understanding how user, group, and other permissions interact makes it possible to enforce least privilege and reduce unauthorized access to sensitive files and directories.
