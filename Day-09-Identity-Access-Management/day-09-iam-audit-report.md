# Day 9: Identity and Access Management (IAM) Audit

## Lab Overview

This lab involved conducting a simulated Identity and Access Management (IAM) audit using a fictional employee account dataset containing 12 records. I analyzed account status, administrator privileges, multifactor authentication (MFA), employee termination status, and account inactivity to identify potential access control weaknesses.

Using macOS Terminal, I applied command-line filtering techniques to identify accounts requiring further investigation and developed preliminary risk-based remediation recommendations.

The objective was to practice foundational IAM security controls, access reviews, and audit procedures relevant to IT support, cybersecurity operations, and Governance, Risk, and Compliance (GRC).

## Lab Objectives

- Identify accounts with administrator privileges.
- Evaluate potential excessive permissions using the Principle of Least Privilege.
- Identify accounts without MFA.
- Detect terminated employees whose accounts remain enabled.
- Investigate dormant accounts and account status.
- Understand Role-Based Access Control (RBAC).
- Practice access recertification and remediation verification.
- Document access control findings and recommendations.

## Lab Environment

- **Operating System:** macOS
- **Tools:** Terminal (zsh), awk, Visual Studio Code
- **Dataset:** day-09-iam-audit.csv
- **Data Format:** CSV
- **Lab Directory:** Documents/Cybersecurity-Labs/Identity-Access-Management

## Audit Scope

The audit covered 12 fictional employee accounts across IT, Finance, Sales, HR, Operations, and Marketing. Accounts were reviewed for elevated permissions, missing MFA, employee offboarding concerns, and inactivity exceeding 30 days.

For this fictional dataset, account statuses of Active and Enabled were treated as usable, while Disabled indicated that account access was turned off.


## IAM Audit Commands and Results

All findings were obtained from the fictional `day-09-iam-audit.csv` dataset using macOS Terminal and `awk`.

### 1. Verify Dataset Records

```bash
awk 'END {print NR}' day-09-iam-audit.csv
```

**Result:** 13 rows, including 12 employee accounts and one CSV header.

### 2. Identify Administrator Accounts

```bash
awk -F, '$6=="Admin" {print $1, $2, $3, $4}' day-09-iam-audit.csv
```

**Result:** 5 administrator accounts.

### 3. Identify Administrator Accounts Outside IT

```bash
awk -F, '$6=="Admin" && $3!="IT" {print $1, $2, $3, $4}' day-09-iam-audit.csv
```

**Result:** 2 accounts: `bwilson` and `cgreen`.

### 4. Identify Accounts Without MFA

```bash
awk -F, '$7=="No" {print $1, $2, $4, $6}' day-09-iam-audit.csv
```

**Result:** 4 accounts without MFA.

### 5. Identify Administrator Accounts Without MFA

```bash
awk -F, '$6=="Admin" && $7=="No" {print $1, $2, $3, $4}' day-09-iam-audit.csv
```

**Result:** 2 accounts: `bwilson` and `cgreen`.

### 6. Identify Terminated Employee Accounts

```bash
awk -F, '$9=="Terminated" {print $1, $2, $5, $7, $8}' day-09-iam-audit.csv
```

**Result:** 2 terminated employees.

### 7. Identify Terminated Employees With Usable Accounts

```bash
awk -F, '$9=="Terminated" && ($5=="Enabled" || $5=="Active") {print $1, $2, $5, $8}' day-09-iam-audit.csv
```

**Result:** 1 account: `rthomas`.

### 8. Identify Dormant Accounts

```bash
awk -F, 'NR>1 && $8>30 {print $1, $2, $5, $8, $9}' day-09-iam-audit.csv
```

**Result:** 3 accounts with more than 30 days since last login.

### 9. Identify Dormant Accounts That Remain Usable

```bash
awk -F, 'NR>1 && $8>30 && ($5=="Active" || $5=="Enabled") {print $1, $2, $5, $8, $9}' day-09-iam-audit.csv
```

**Result:** 2 accounts: `kdavis` and `rthomas`.

### 10. Count Active or Enabled Accounts

```bash
awk -F, 'NR>1 && ($5=="Active" || $5=="Enabled") {count++} END {print count+0}' day-09-iam-audit.csv
```

**Result:** 11 accounts were usable; 1 was disabled.

## IAM Audit Findings Summary

| Audit Category | Count |
|---|---:|
| Total employee accounts | 12 |
| Active or enabled accounts | 11 |
| Disabled accounts | 1 |
| Administrator accounts | 5 |
| Administrator accounts outside IT | 2 |
| Accounts without MFA | 4 |
| Administrator accounts without MFA | 2 |
| Terminated employee accounts | 2 |
| Terminated employees with usable accounts | 1 |
| Dormant accounts (over 30 days) | 3 |
| Dormant accounts still usable | 2 |

**Analysis note:** Findings overlap. A single account can appear in multiple categories. Accounts with administrator access outside IT require review, but they do not automatically represent inappropriate access.


## IAM Risk Priorities and Remediation Recommendations

The following findings were prioritized based on employment status, account permissions, MFA protection, account inactivity, and potential business impact.

| Priority | Account | Security Finding | Recommended Remediation |
|---|---|---|---|
| High — Offboarding | rthomas | Terminated employee with an enabled account, no MFA, and 120 days since last login | Confirm termination with HR, coordinate account deactivation, revoke sessions, review associated access, and verify completion. |
| High — Privileged Access | bwilson | Sales Representative with Admin privileges and no MFA | Remove unnecessary Admin access with authorization, retain approved Sales access, enable MFA, and verify changes. |
| High — Privileged Access | cgreen | HR Manager with Admin privileges and no MFA | Review business justification, remove unneeded privileges, retain authorized HR access, enable MFA, and document recertification. |
| Medium — Dormant Account | kdavis | Active employee with no MFA and 45 days since last login | Confirm continued business need, enable appropriate MFA, and review account status. |

### Recommended IAM Security Improvements

1. **Strengthen employee offboarding:** Coordinate timely account deactivation with HR and IT.
2. **Enforce MFA:** Prioritize privileged accounts and extend appropriate MFA requirements to other users.
3. **Apply least privilege:** Remove permissions that aren't needed for authorized job duties.
4. **Perform periodic access reviews:** Have managers and system owners recertify access.
5. **Review dormant accounts:** Investigate accounts exceeding the organization's inactivity threshold.
6. **Verify remediation:** Confirm access changes and MFA enforcement before closing findings.
7. **Retain audit evidence:** Document findings, approvals, corrective actions, and verification.

### Remediation Verification

A finding should not be marked Resolved simply because a change was requested.

For example, resolving the `bwilson` finding requires confirming that unnecessary administrator privileges were removed, MFA is enabled and enforced, and approved Sales access remains functional.

**Lab limitation:** These recommendations are based on fictional account records. No actual accounts were disabled, permissions changed, or MFA settings modified during this exercise.


## Key Findings

During this simulated Identity and Access Management (IAM) audit, I analyzed 12 fictional employee accounts and identified several potential access control weaknesses.

The audit identified five administrator accounts, four accounts without MFA, and two administrator accounts with MFA disabled. I also identified one terminated employee whose account remained enabled and two dormant accounts that were still usable.

The highest-priority offboarding finding involved `rthomas`, a terminated employee with an enabled account and MFA disabled. Additional privileged-access concerns involved `bwilson` and `cgreen`, whose administrator permissions required business justification and stronger authentication controls.

These findings demonstrated the importance of reviewing employee access based on job responsibilities, employment status, authentication protection, and account activity.

## Skills Developed

- Identity and Access Management (IAM) fundamentals
- User account auditing and access reviews
- Principle of Least Privilege
- Role-Based Access Control (RBAC)
- Multifactor authentication (MFA) assessment
- Privileged account reviews
- Employee offboarding and account deprovisioning
- Dormant account identification
- Access recertification
- Risk-based remediation prioritization
- Remediation verification and audit evidence
- CSV analysis using macOS Terminal and awk
- Security reporting and documentation

## Lessons Learned

This lab demonstrated that effective IAM requires more than creating and disabling employee accounts. Organizations must regularly review permissions, verify employee access needs, enforce appropriate authentication protections, and remove access when it is no longer authorized.

I learned that administrator privileges should be justified by business requirements and that terminated employees with enabled accounts present potential security risks. I also learned that account inactivity alone does not prove inappropriate access, so investigation and coordination with account owners are important.

Another key lesson was the importance of remediation verification. Security findings should not be considered resolved until authorized changes have been confirmed and supporting evidence has been documented.

## Conclusion

I completed a simulated IAM audit using macOS Terminal, Visual Studio Code, and a fictional CSV dataset. I analyzed 12 employee accounts, identified access control concerns, evaluated risk priorities, and developed remediation recommendations using least privilege and access governance principles.

This project strengthened foundational skills relevant to IT Support, IAM Analyst, Cybersecurity Analyst, and Governance, Risk, and Compliance (GRC) roles.

**Lab Disclaimer:** All accounts, employees, and security findings were fictional. No real identity systems or account permissions were accessed or modified during this lab.