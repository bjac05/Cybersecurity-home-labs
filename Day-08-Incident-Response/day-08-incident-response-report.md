# Day 8: Security Incident Response Investigation

## Incident Overview

This lab involved investigating a simulated security incident using a fictional CSV log containing 15 security events. The purpose was to identify suspicious authentication activity, correlate related events, assess potential security risks, and develop incident response recommendations.

The investigation identified five failed administrator login attempts originating from 198.51.100.23, followed by a successful login to the admin account on SRV-001. Subsequent events included administrator privilege modifications, sensitive directory access, an unusual outbound data transfer, and creation of a new privileged account.

Based on this sequence, the incident was classified as a suspected administrator account compromise with possible unauthorized access, persistence, and data exfiltration. Urgent escalation was recommended.

## Incident Details

- **Incident Type:** Suspected Administrator Account Compromise
- **Incident Date:** October 15, 2026 (simulated)
- **Affected System:** SRV-001
- **Affected Account:** admin
- **Suspicious Source IP:** 198.51.100.23
- **Assessed Priority:** High/Critical
- **Investigation Status:** Simulated investigation completed; no live containment or remediation performed
- **Evidence Source:** day-08-incident-log.csv

## Lab Environment

- **Operating System:** macOS
- **Tools:** Terminal, grep, awk, Visual Studio Code
- **Data Format:** CSV
- **Lab Directory:** Documents/Cybersecurity-Labs/Incident-Response

**Disclaimer:** All security events, accounts, systems, and IP addresses in this exercise are fictional training data. The investigation did not involve real systems or confirmed malicious activity.


## Incident Timeline

The following timeline documents suspicious activity associated with source IP address `198.51.100.23` on October 15, 2026. All events are simulated.

| Time | Event ID | Event | Investigation Finding |
|---|---|---|---|
| 08:05:18–08:05:47 | EVT-002–EVT-006 | Failed Logins | Five failed attempts targeting the `admin` account on `SRV-001`. |
| 08:06:02 | EVT-007 | Successful Login | The same source IP successfully logged in as `admin`. |
| 08:07:15 | EVT-008 | Privilege Change | Administrator privileges were modified. |
| 08:09:42 | EVT-009 | File Access | A sensitive directory was accessed. |
| 08:12:07 | EVT-010 | Data Transfer | An unusual outbound data transfer was recorded. |
| 08:25:32 | EVT-014 | Account Change | A new privileged user account was created. |

### Timeline Analysis

The sequence of failed logins followed by successful administrator access and subsequent sensitive operations suggests a possible account compromise.

The unusual outbound data transfer raises concern about potential data exfiltration, while the creation of a privileged account could indicate an attempt to establish persistent access.

These are preliminary interpretations of the simulated log entries. Additional evidence would be required to confirm unauthorized access, determine what data was transferred, and establish whether an attacker was responsible.


## Investigation Commands and Evidence

### Commands Executed

**1. Verify the number of log records**

```bash
awk 'END {print NR}' day-08-incident-log.csv
```

Result: 16 total records, consisting of 15 simulated security events and one CSV header.

**2. Identify failed login attempts**

```bash
grep ",Login,Failed," day-08-incident-log.csv
```

Result: Six failed login events were identified.

**3. Identify source IP addresses for failed logins**

```bash
awk -F, '$6=="Login" && $7=="Failed" {print $3}' day-08-incident-log.csv
```

Result: Two distinct source IP addresses were associated with failed login events.

**4. Investigate the suspicious source IP**

```bash
grep "198.51.100.23" day-08-incident-log.csv
```

Result: Identified repeated failed administrator logins, a successful login, privilege modification, sensitive file access, unusual data transfer, and creation of a privileged account.

**5. Examine successful events from the suspicious IP**

```bash
awk -F, '$3=="198.51.100.23" && $7=="Success" {print $2, $6, $8}' day-08-incident-log.csv
```

Result: Five successful events were identified.

**6. Identify Critical-severity events**

```bash
awk -F, '$8=="Critical" {print $2, $3, $6, $8}' day-08-incident-log.csv
```

Result: One Critical event was identified: EVT-010, an unusual outbound data transfer.

### Key Evidence

- **Suspicious source IP:** 198.51.100.23
- **Affected account:** admin
- **Affected system:** SRV-001
- **Failed administrator logins:** 5
- **Successful events associated with the suspicious IP:** 5
- **Critical-severity events:** 1
- **Primary concern:** Possible administrator account compromise with suspicious privileged activity and potential data exfiltration.

These findings are based entirely on fictional training logs. The events warrant investigation but do not independently establish that an attacker gained access or stole information.


## Incident Response Recommendations

Based on the simulated evidence, I recommend urgently escalating this incident to the incident response team for further investigation and authorized containment.

### 1. Escalation and Evidence Preservation

- Notify the incident response team and relevant system owners.
- Preserve authentication logs, account modification events, and network transfer records.
- Record the incident timeline and maintain the integrity of collected evidence.
- Investigate whether the administrator activity was authorized.

### 2. Containment

- Revoke suspicious sessions associated with the potentially compromised administrator account.
- Temporarily restrict the affected account when authorized.
- Evaluate whether SRV-001 should be isolated to prevent continued malicious activity.
- Review the newly created privileged account for unauthorized access.
- Coordinate containment actions with system owners to minimize unnecessary business disruption.

### 3. Eradication

- Investigate and remove confirmed unauthorized accounts or malicious persistence mechanisms after preserving evidence.
- Secure potentially compromised credentials and address the underlying cause of unauthorized access.
- Examine affected systems for additional suspicious changes.

### 4. Recovery

- Verify that affected systems are free of confirmed threats.
- Validate security configurations and access controls.
- Restore approved access and test essential business services.
- Monitor for renewed suspicious logins or unauthorized activity.

### 5. Preventive Security Improvements

- Implement phishing-resistant multifactor authentication for privileged accounts where supported.
- Configure alerts for repeated failed logins followed by successful authentication.
- Review administrator privileges and newly created accounts regularly.
- Improve monitoring of sensitive file access and unusual outbound transfers.
- Conduct a post-incident review to identify response improvements.

### Investigation Limitations

The dataset does not establish whether the administrator login was unauthorized or whether sensitive data was actually exfiltrated. Additional authentication, endpoint, network, and system evidence would be required to confirm the cause and scope of the incident.

All actions above are recommendations for a fictional scenario. No live containment, eradication, or recovery actions were performed during this lab.


## Key Findings

During this simulated incident response investigation, I analyzed 15 security events and identified a suspicious sequence involving an administrator account on SRV-001.

The investigation identified six failed login attempts across two source IP addresses. Five of those attempts targeted the admin account from 198.51.100.23 and were followed by a successful login from the same IP.

Additional events included privilege modification, sensitive directory access, an unusual outbound data transfer, and creation of a privileged account. This sequence justified classifying the scenario as a suspected High/Critical-priority security incident requiring urgent escalation.

The available evidence raised concern about account compromise and possible data exfiltration but did not confirm malicious activity or establish that information was stolen.

## Skills Developed

- Security event and authentication log analysis
- Identifying suspicious login patterns
- Investigating source IP addresses
- Correlating events and constructing incident timelines
- Interpreting event severity and prioritizing incidents
- Using grep and awk to filter CSV evidence
- Understanding containment, eradication, and recovery
- Developing incident response recommendations
- Preserving evidence and documenting investigation findings
- Identifying preventive security improvements

## Lessons Learned

This lab demonstrated the importance of analyzing multiple security events together rather than treating each alert independently. Repeated failed logins followed by a successful administrator login, privilege changes, and unusual data transfer activity warrant further investigation.

I also learned that incident response involves more than identifying suspicious activity. Security teams must preserve evidence, escalate appropriately, coordinate authorized containment, eliminate confirmed threats, safely restore services, and identify opportunities to strengthen security controls.

## Conclusion

I completed a simulated incident response investigation using macOS Terminal, Visual Studio Code, and a fictional CSV dataset. I analyzed authentication and security events, reconstructed a suspicious timeline, assessed potential incident severity, and documented recommended response actions.

This project strengthened foundational skills relevant to SOC analysis, IT security operations, and Governance, Risk, and Compliance (GRC).

**Lab Disclaimer:** All events and systems were fictional. No real accounts, servers, or networks were investigated, contained, or modified.
