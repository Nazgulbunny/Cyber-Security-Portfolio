# SQL for Security Analysis — Login and Employee Investigation

## Overview

This project demonstrates how SQL can be used during cybersecurity investigations to analyze authentication activity and identify systems requiring security updates.

The investigation uses two datasets:

- `log_in_attempts`
- `employees`

SQL filtering was used to identify suspicious login activity based on time, date, and geographic location, as well as employee groups requiring security remediation.

---

## Scenario

Potential security issues were identified involving employee login activity and endpoint security.

The investigation required answering several questions:

1. Which failed login attempts occurred after business hours?
2. Which login attempts occurred on specific dates?
3. Which login attempts originated outside Mexico?
4. Which Marketing employees were located in the East building?
5. Which employees belonged to Finance or Sales?
6. Which employees were outside the Information Technology department?

---

# 1. Investigating Failed After-Hours Logins

The first objective was to identify unsuccessful login attempts occurring after 18:00.

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00:00'
  AND success = FALSE;
```

## Analysis

Two conditions are combined using `AND`:

```text
login_time > '18:00:00'
            +
success = FALSE
```

Therefore, a record is returned only when the authentication attempt:

- Occurred after 18:00
- Failed

This type of query can help security analysts identify unusual authentication activity outside expected working hours.

---

# 2. Investigating Specific Dates

Login activity associated with two dates was retrieved using:

```sql
SELECT *
FROM log_in_attempts
WHERE login_date IN ('2022-05-08', '2022-05-09');
```

Using `IN` makes the intent concise when checking a column against multiple specific values.

The equivalent query could also be written as:

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-08'
   OR login_date = '2022-05-09';
```

---

# 3. Investigating Logins Outside Mexico

To identify login attempts originating outside Mexico:

```sql
SELECT *
FROM log_in_attempts
WHERE country NOT LIKE 'MEX%';
```

The `%` wildcard represents any sequence of characters following `MEX`.

This allows the query to exclude country values beginning with that pattern.

---

# 4. Identifying Marketing Employees

The next investigation identified Marketing employees located in East-building offices.

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East-%';
```

This combines:

```text
Department = Marketing
        AND
Office begins with East-
```

Both conditions must be satisfied.

---

# 5. Identifying Finance and Sales Employees

Employees belonging to either department can be retrieved using:

```sql
SELECT *
FROM employees
WHERE department IN ('Sales', 'Finance');
```

The equivalent `OR` query would be:

```sql
SELECT *
FROM employees
WHERE department = 'Sales'
   OR department = 'Finance';
```

---

# 6. Identifying Employees Outside IT

To retrieve employees who are not members of the Information Technology department:

```sql
SELECT *
FROM employees
WHERE department <> 'Information Technology';
```

Another valid form is:

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

This query can be useful when a security action needs to target every department except a specific group.

---

# Security Applications

These SQL techniques can support cybersecurity investigations involving:

### Authentication Monitoring

```sql
WHERE success = FALSE
```

can help isolate failed authentication attempts.

### Temporal Analysis

```sql
WHERE login_time > '18:00:00'
```

can help identify activity occurring outside expected periods.

### Geographic Analysis

Location fields can be filtered to investigate authentication activity originating from unexpected countries or regions.

### Endpoint Remediation

Employee and asset datasets can be queried to identify groups requiring patches, configuration changes, or other security updates.

---

# SQL Concepts Demonstrated

This project uses:

```text
SELECT
FROM
WHERE
AND
OR
NOT
IN
LIKE
<>
=
>
```

It also demonstrates wildcard matching with:

```text
%
```

---

# Security Investigation Workflow

A simplified workflow for this type of analysis is:

```text
Security Alert
      │
      ▼
Identify Investigation Criteria
      │
      ▼
Query Relevant Dataset
      │
      ▼
Filter Suspicious Records
      │
      ▼
Analyze Results
      │
      ▼
Validate Findings
      │
      ▼
Investigate / Remediate
```

SQL provides the filtering and retrieval layer that allows analysts to reduce large datasets to the records relevant to an investigation.

---

# Skills Demonstrated

This project demonstrates practical knowledge of:

- SQL
- Security data analysis
- Authentication analysis
- Login investigation
- Security event filtering
- Pattern matching
- Boolean operators
- Dataset investigation
- Security remediation targeting
- Analytical problem solving

---

## Key Takeaway

Cybersecurity investigations often involve finding a small number of relevant events inside much larger datasets.

SQL provides security analysts with a powerful way to filter authentication, employee, asset, and security-event data according to specific investigative criteria.

Combining conditions such as:

```sql
WHERE login_time > '18:00:00'
  AND success = FALSE
```

turns a broad dataset into focused evidence that can support further investigation.
