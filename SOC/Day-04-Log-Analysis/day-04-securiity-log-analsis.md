# Day 4: SOC Security Log Analysis

## Lab Overview

This lab focuses on analyzing macOS system logs using
command-line tools to identify system events, investigate
errors, and evaluate potentially suspicious activity.

I used macOS Terminal to retrieve and filter logs, examine
loginwindow-related activity, and preserve selected evidence
for further investigation. The objective was to practice
foundational security monitoring and incident triage skills
relevant to a Security Operations Center (SOC).

## Lab Objectives

- Retrieve and examine system logs using Terminal.
- Filter events by severity, process name, and keywords.
- Practice using grep, head, tail, and wc to analyze log data.
- Compare results across different investigation time windows.
- Save and verify log evidence for analysis.
- Document observations and distinguish routine system
  activity from potential security concerns.

## Lab Environment

- Operating System: macOS
- Terminal: macOS Terminal (zsh)
- Text Editor: Visual Studio Code
- Log Source: macOS Unified Logging
- Investigation Directory: Documents/Cybersecurity-Labs/SOC/Day-04-Log-Analysis

## Investigation Scope

This investigation focused on a limited sample of local
macOS system events, particularly messages containing
loginwindow. It was a training exercise, not a comprehensive
security audit or confirmation that the system was free
of threats.


## Commands Executed and Results

| Command | Purpose | Observation |
|---|---|---|
| `log show --last 1m --style compact` | Retrieve recent system logs | Displayed timestamped events from macOS services and applications. |
| `log show --last 1m --style compact --predicate 'messageType == error'` | Filter error-level events | Identified errors involving Apple services, Norton/Symantec extensions, and other system components. |
| `log show --last 1m --style compact \| grep -i authentication` | Search for authentication-related messages | Returned no matching lines in the sampled time window. |
| `log show --last 5m --style compact \| grep -i failed` | Identify failed operations | Revealed recurring system and application errors. |
| `log show --last 2m --style compact \| grep -i loginwindow` | Search for loginwindow-related events | Identified screen saver, display, and session-related activity. |
| `log show --last 2m --style compact \| grep -i loginwindow \| wc -l` | Count matching events | Returned 0 during one two-minute search. |
| `log show --last 30m --style compact \| grep -i loginwindow \| wc -l` | Expand the investigation window | Returned 783 matching lines. |
| `log show --last 30m --style compact \| grep -i loginwindow > loginwindow-investigation.log` | Save selected evidence | Created a local investigation log file. |
| `ls -lh loginwindow-investigation.log` | Verify the evidence file | Confirmed the file was approximately 13 KB. |
| `wc -l loginwindow-investigation.log` | Count saved evidence | Confirmed 62 saved lines. |
| `head -n 5 loginwindow-investigation.log` | Inspect earliest saved entries | Identified laptop lid-state changes. |
| `tail -n 5 loginwindow-investigation.log` | Inspect latest saved entries | Identified screen saver and display sleep checks. |

**Evidence handling note:** The raw investigation log was retained
locally rather than uploaded to a public repository because
system logs can contain private information.


## Evidence Summary

- **Evidence source:** macOS Unified Logging
- **Collection method:** Terminal commands using `log show`, `grep`, and output redirection
- **Saved evidence:** `loginwindow-investigation.log`
- **Evidence size:** Approximately 13 KB
- **Saved log entries:** 62 lines
- **Investigation date:** October 19, 2026
- **Evidence storage:** Retained locally; raw logs excluded from public GitHub

The saved evidence was reviewed using `head`, `tail`, and `wc`. The findings represent a limited investigation of matching system log messages, not a comprehensive authentication audit.


## Investigation Findings

### Finding 1: Recurring System Errors

Filtering for error-level events and messages containing `failed` revealed errors associated with macOS services and applications.

Observed examples included:
- `searchpartyd`: Failed to determine beacon information.
- `loginwindow`: Failed to set up a clipboard-related reference (`CFPasteboardRef`).
- Norton/Symantec network extension: Application-information lookup errors.
- Apple News services: Configuration initialization failures.

These events may indicate routine application, connectivity, or system-service issues. The evidence reviewed did not establish malicious activity.

### Finding 2: Loginwindow Activity

A keyword search for `loginwindow` identified events associated with screen saver checks, display sleep, and laptop lid-state changes.

The saved log file contained 62 matching lines and was approximately 13 KB in size.

The first five saved entries included `clamshellStateChanged` messages. The last five included `ScreenSaverDaemon` checks and display sleep-related messages.

These observations were consistent with normal macOS session and display management. No clear evidence of unauthorized login activity was identified in the sampled entries.

### Finding 3: Investigation Time Window

A two-minute keyword search returned 0 matching lines, while a separate 30-minute search returned 783 matching lines.

This demonstrated how the selected time window affects investigation results. Since the searches were performed at different times, these figures should not be interpreted as a direct rate comparison.

### Initial Security Assessment

**Classification:** No confirmed security incident identified in the reviewed evidence.

**Assessment:** The sampled events appeared primarily related to routine system processes, application errors, and display management. Further investigation would be appropriate if the activity coincided with suspicious sign-in attempts, unexpected processes, security software failures, or user-reported issues.

**Limitation:** This was a limited local log review and does not establish that the entire system is free from threats.


## Security Takeaways

- **Log filtering:** Used command-line tools to narrow large volumes of system events into relevant results.
- **Event analysis:** Examined timestamps, process names, and messages to understand system activity.
- **Investigation scope:** Learned how changing time windows affects the number of matching events.
- **Evidence preservation:** Saved filtered log entries locally for repeatable analysis.
- **Incident triage:** Distinguished routine system errors from activity that may warrant further investigation.
- **Security awareness:** Learned that an error message or a large number of log entries does not automatically indicate an attack.

## Conclusion

During this lab, I gained hands-on experience collecting, filtering, and examining macOS system logs using Terminal. I investigated system errors, reviewed loginwindow-related activity, and preserved 62 matching log lines for further analysis.

Based on the sampled evidence, I did not identify a confirmed security incident. The events I examined appeared consistent with routine application, session, and display management activity.

This lab strengthened my foundational SOC investigation skills, including log analysis, command-line filtering, evidence handling, and documenting findings. Future exercises will build on these skills using simulated security alerts and authentication events.
