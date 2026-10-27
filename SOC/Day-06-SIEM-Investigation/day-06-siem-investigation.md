# Day 6: SIEM Security Alert Investigation

## Lab Overview

This lab introduces Security Information and Event Management (SIEM) concepts through a simulated security investigation. I analyzed structured security events from authentication, endpoint, and identity sources to identify potentially malicious activity and prioritize alerts.

Using macOS Terminal, I filtered a CSV dataset by severity, correlated events associated with a specific source IP address, and investigated a Critical privilege-change alert.

The objective was to develop foundational skills in security event monitoring, alert triage, event correlation, and incident investigation.

## Lab Objectives

- Understand the purpose of SIEM platforms in security operations.
- Analyze structured security events from multiple sources.
- Filter events by severity and source IP address.
- Correlate authentication, endpoint, and identity alerts.
- Identify suspicious sequences involving successful logins and privilege changes.
- Prioritize alerts based on potential security impact.
- Document investigation findings and recommended response actions.

## Lab Environment

- Operating System: macOS
- Terminal: macOS Terminal (zsh)
- Text Editor: Visual Studio Code
- Dataset: simulated-siem-events.csv
- Data Format: CSV (Comma-Separated Values)
- Event Sources: Authentication, Endpoint, Identity
- Investigation Directory: Documents/Cybersecurity-Labs/SOC/Day-06-SIEM-Investigation

## Investigation Scope

This training exercise used a fictional dataset containing 17 security events dated October 22, 2026. All usernames, IP addresses, and security events were simulated. The investigation practiced SIEM-style searches and event correlation using Terminal commands rather than an installed SIEM platform.

Findings describe potentially suspicious patterns within the dataset and do not establish that a real security incident occurred.


## Commands Executed and Results

| Command | Purpose | Observation |
|---|---|---|
| `wc -l simulated-siem-events.csv` | Count newline characters in the dataset | Returned 17. The final event was present; the file may lack a trailing newline. |
| `tail -n 3 simulated-siem-events.csv` | Inspect the final events | Confirmed the final successful login at 09:31:02. |
| `grep -E ',(High\|Critical),' simulated-siem-events.csv` | Find High and Critical events | Identified two High-severity events and one Critical event. |
| `grep '203.0.113.45' simulated-siem-events.csv` | Correlate events by source IP | Identified seven events across three security sources. |
| `grep -c ',Critical,' simulated-siem-events.csv` | Count Critical events | Returned one Critical-severity event. |
| `grep Critical simulated-siem-events.csv` | Display Critical event details | Identified a privilege-change event involving the `admin` account. |

## Security Event Summary

- **Total simulated security events:** 17
- **Event sources:** Authentication, Endpoint, and Identity
- **High-severity events:** 2
- **Critical-severity events:** 1
- **Correlated events involving `203.0.113.45`:** 7
- **Primary account investigated:** `admin`
- **Critical event:** `PRIVILEGE_CHANGE` at 09:07:15

**Environment note:** These searches were performed with macOS Terminal against a fictional CSV dataset. No SIEM software was installed or used during this exercise.


## Investigation Findings

### Finding 1: Suspicious Administrator Authentication

**Source IP:** `203.0.113.45`  
**Account:** `admin`  
**Log source:** Authentication

Between 09:05:10 and 09:05:22, the dataset recorded four failed login attempts against the `admin` account. At 09:05:26, a successful login occurred from the same IP address.

The failures occurred at four-second intervals, followed by a successful authentication. This pattern is consistent with possible automated password guessing, but the dataset does not confirm unauthorized access.

### Finding 2: Suspicious Endpoint Activity

**Timestamp:** 09:06:03  
**Log source:** Endpoint  
**Event type:** `ANTIVIRUS_ALERT`  
**Severity:** High

An endpoint security event reported a suspicious executable associated with the `admin` account and the same source IP address.

Because this alert followed the successful login, it increased concern about possible malicious activity. However, the dataset does not identify the executable, confirm that it ran, or prove the events were causally related.

### Finding 3: Privileged Group Membership Change

**Timestamp:** 09:07:15  
**Log source:** Identity  
**Event type:** `PRIVILEGE_CHANGE`  
**Severity:** Critical

An identity-management event recorded an account being added to an administrators group. The event was associated with the `admin` account and source IP `203.0.113.45`.

This change raises concern about potential privilege escalation. The dataset does not identify which account was added to the group or establish whether the change was authorized.

### Finding 4: Cross-Source Event Correlation

Seven events were associated with `203.0.113.45` across Authentication, Endpoint, and Identity sources:

- Four failed administrator logins
- One successful administrator login
- One suspicious executable alert
- One privileged group membership change

The sequence occurred between 09:05:10 and 09:07:15, a period of two minutes and five seconds.

The combination of events warrants urgent investigation because it suggests possible account compromise and subsequent unauthorized activity.

## Initial Security Assessment

**Simulated incident priority:** Critical  
**Classification:** Suspected account compromise with possible privilege escalation; not confirmed.

**Reason for prioritization:** Repeated authentication failures followed by a successful login, an endpoint security alert, and a privileged group change involving the same account and source IP.

**Limitations:** This analysis is based on fictional events. Additional authentication details, device identifiers, endpoint telemetry, approval records, and account-owner confirmation would be needed to determine whether an actual compromise occurred.


## Recommended Incident Response Actions

### 1. Escalate the Security Alert

- Escalate the correlated events to the appropriate incident response team as a Critical-priority investigation.
- Provide the event timeline, affected account, source IP address, and associated security alerts.
- Preserve relevant logs and evidence according to organizational procedures.

### 2. Validate Authentication Activity

- Confirm whether the successful administrator login was authorized.
- Review MFA results, device identifiers, session details, and login history.
- Determine whether the account owner recognizes the activity.

### 3. Investigate the Endpoint Alert

- Identify the suspicious executable and its file hash, path, and detection details.
- Determine whether the executable was blocked, quarantined, or executed.
- Review endpoint activity for additional suspicious processes or connections.

### 4. Investigate the Privilege Change

- Identify which account was added to the administrators group.
- Verify whether the change was approved.
- Review related identity-management and administrative activity.

### 5. Contain and Monitor

- If compromise is confirmed or strongly suspected, follow approved procedures for account restrictions, session revocation, credential resets, and endpoint isolation as appropriate.
- Continue monitoring for additional suspicious authentication, endpoint, and privilege-change events.
- Document new findings and update the incident's priority as evidence develops.

**Response limitation:** These are recommended actions for a simulated investigation. No real accounts, endpoints, or networks were modified.


## Security Takeaways

- **SIEM fundamentals:** Learned how security events from multiple sources can be centralized and investigated.
- **Event correlation:** Connected authentication, endpoint, and identity events using a shared username, IP address, and timeline.
- **Alert filtering:** Used command-line searches to identify High and Critical severity events.
- **Threat identification:** Recognized activity consistent with possible password guessing, account compromise, and privilege escalation.
- **Alert prioritization:** Classified the combined activity as a Critical-priority simulated investigation based on potential impact.
- **Incident response:** Developed recommendations for validating alerts, preserving evidence, escalating incidents, and considering appropriate containment actions.
- **Evidence-based analysis:** Distinguished potentially malicious behavior from confirmed unauthorized activity.

## Conclusion

During this lab, I investigated 17 simulated security events representing authentication, endpoint, and identity-management activity. Using macOS Terminal, I filtered events by severity, identified one Critical and two High-severity alerts, and correlated seven events associated with a single source IP address.

The most significant finding involved four failed administrator login attempts followed by a successful authentication, a suspicious executable alert, and an administrators-group membership change. Together, these events suggested potential account compromise and privilege escalation, warranting urgent investigation.

This exercise strengthened my foundational understanding of SIEM workflows, security event correlation, alert triage, and incident response planning. Although I used a fictional CSV dataset rather than a deployed SIEM platform, the investigation demonstrated concepts relevant to entry-level SOC analyst responsibilities.

No real systems were attacked or modified during this exercise, and the simulated evidence did not establish a confirmed compromise.
