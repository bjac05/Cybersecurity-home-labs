# Day 5: Suspicious Login Activity Investigation

## Lab Overview

This lab simulates a Security Operations Center (SOC) investigation involving repeated failed login attempts and potentially unauthorized access to a privileged account.

Using a fictional authentication log, I analyzed login failures, successful authentications, usernames, source IP addresses, and event timestamps to identify potentially suspicious activity.

The objective was to practice authentication log analysis, event correlation, alert prioritization, and foundational incident response decision-making.

## Lab Objectives

- Identify failed and successful authentication events.
- Filter login activity by username and source IP address.
- Recognize patterns associated with brute-force attacks and password spraying.
- Correlate failed login attempts with successful authentications.
- Prioritize suspicious activity based on potential security impact.
- Document investigation findings and recommended response actions.

## Lab Environment

- Operating System: macOS
- Terminal: macOS Terminal (zsh)
- Text Editor: Visual Studio Code
- Log Source: Fictional authentication events created for training
- Log File: simulated-login-events.log
- Investigation Directory: Documents/Cybersecurity-Labs/SOC/Day-05-Login-Investigation

## Investigation Scope

This investigation used 20 simulated authentication events dated October 20, 2026. All usernames and IP addresses are fictional, and the activity did not involve real login attempts or attacks. Findings describe potential security patterns within the simulated dataset rather than a confirmed real-world incident.


## Commands Executed and Results

| Command | Purpose | Observation |
|---|---|---|
| `grep "LOGIN_FAILED" simulated-login-events.log` | Find failed authentication attempts | Identified failed logins across multiple accounts and source IP addresses. |
| `grep -c "LOGIN_FAILED" simulated-login-events.log` | Count failed attempts | Found 12 failed login events. |
| `grep "LOGIN_SUCCESS" simulated-login-events.log` | Find successful authentications | Identified 8 successful login events. |
| `grep "203.0.113.45" simulated-login-events.log` | Investigate a specific source IP | Found six failures followed by one successful administrator login. |
| `grep "198.51.100.77" simulated-login-events.log` | Investigate another source IP | Found four failed logins targeting three accounts. |
| `grep "user=admin " simulated-login-events.log` | Isolate the administrator account | Identified seven authentication events, excluding the separate `administrator` account. |
| `grep "user=admin " simulated-login-events.log \| grep -c "LOGIN_FAILED"` | Count administrator login failures | Confirmed six failed attempts against `admin`. |

## Authentication Event Summary

- **Total simulated events:** 20
- **Failed logins:** 12
- **Successful logins:** 8
- **Primary source under investigation:** `203.0.113.45`
- **Secondary source under investigation:** `198.51.100.77`

All source IP addresses in this lab use ranges reserved for documentation and testing. They do not identify actual attacking systems.


## Investigation Findings

### Finding 1: Potential Successful Brute-Force Attack

**Source IP:** `203.0.113.45`  
**Target account:** `admin`  
**Alert severity:** High (simulated assessment)
 
The source IP generated six failed login attempts against the `admin` account between 08:10:05 and 08:10:25. Each failure occurred four seconds apart. At 08:10:29, the same IP successfully authenticated to the account.

This sequence lasted 24 seconds and is consistent with a potentially successful brute-force attack. Because the account may have elevated privileges, the activity was prioritized for investigation. The logs alone do not confirm unauthorized access.

### Finding 2: Multiple Accounts Targeted

**Source IP:** `198.51.100.77`  
**Alert severity:** Medium (simulated assessment)

Four failed login attempts targeted three accounts between 08:25:10 and 08:25:16:

- `service_account`: Two failures
- `backup_admin`: One failure
- `administrator`: One failure

The activity occurred over six seconds and could indicate password spraying or account enumeration. No successful login from this IP was present in the simulated dataset. The attempted passwords and account-validity responses were unavailable, so the technique cannot be confirmed.

### Finding 3: Other Authentication Activity

The remaining events included successful logins and isolated login failures involving `jsmith` and `mjones`.

These isolated failures followed by successful authentications may be consistent with ordinary password-entry mistakes. Additional context would be needed to determine whether they were authorized.

## Initial Security Assessment

**Priority:** Investigate the `admin` login sequence first, while retaining the multi-account failures for follow-up.

**Classification:** Suspicious authentication activity; potential account compromise not confirmed.

**Limitations:** This assessment relies entirely on a fictional 20-event dataset. It contains no MFA results, account-owner confirmation, endpoint activity, or post-login actions.


## Recommended Incident Response Actions

### 1. Validate the Alert

- Review the authentication timeline for the `admin` account.
- Confirm whether the successful login was authorized by the account owner.
- Review MFA results, device information, and login location if available.

### 2. Investigate Potential Account Compromise

- Examine activity performed after the successful administrator login.
- Check for unusual account changes, privilege escalation, or suspicious processes.
- Correlate authentication events with endpoint and network security logs.

### 3. Escalate and Contain if Necessary

- Escalate the high-priority authentication alert to the appropriate security team.
- If unauthorized access is confirmed or strongly suspected, follow approved procedures for session revocation, password resets, and temporary account restrictions.
- Preserve relevant evidence before making changes when feasible.

### 4. Investigate the Secondary Source

- Review the accounts targeted by `198.51.100.77`.
- Check for additional attempts involving the same source across a wider time window.
- Determine whether password spraying or account enumeration is supported by additional evidence.

### 5. Document and Monitor

- Record the timeline, affected accounts, source IP addresses, and investigation findings.
- Continue monitoring for suspicious authentication activity.
- Update the incident record as new information becomes available.

**Response limitation:** These actions are recommendations for a fictional SOC investigation. No real accounts, systems, or network connections were modified.


## Security Takeaways

- **Authentication analysis:** Used command-line tools to identify and count successful and failed login attempts.
- **Event correlation:** Connected login events using usernames, source IP addresses, and timestamps.
- **Threat identification:** Recognized patterns consistent with potential brute-force attacks and password spraying.
- **Alert prioritization:** Prioritized a privileged account with repeated failures followed by a successful login.
- **Incident response:** Developed recommendations for validating alerts, investigating possible compromise, and escalating suspicious activity.
- **Evidence-based analysis:** Distinguished suspicious behavior from confirmed unauthorized access.

## Conclusion

During this lab, I investigated 20 simulated authentication events using macOS Terminal. I identified 12 failed logins and eight successful logins, then analyzed suspicious activity associated with two source IP addresses.

The highest-priority finding involved six failed login attempts against the `admin` account followed by a successful login from the same source within a 24-second period. I also identified four failed attempts against three different accounts from a second IP address.

Based on the simulated evidence, I classified the administrator login sequence as a high-priority alert requiring further investigation. However, the available logs did not confirm that unauthorized access occurred.

This lab strengthened my foundational SOC analyst skills in authentication log analysis, event correlation, threat identification, alert prioritization, and incident response planning. No real systems were attacked or modified during this exercise.
