# Incident Analysis: Suspicious Authentication and PowerShell Execution

## Incident Summary
Multiple failed authentication attempts were observed on a Windows endpoint, followed by a successful login and subsequent PowerShell execution. The behavior was detected through correlated Windows Security events collected by the Wazuh SIEM. While the activity was ultimately determined to be benign lab testing, the pattern closely resembles real-world attacker tradecraft involving credential guessing and post-authentication reconnaissance.

---

## Environment Overview
- **SIEM Platform:** Wazuh (All-in-One)
- **Endpoint:** Windows 11 (WIN-ENDPOINT-01)
- **Log Source:** Windows Security Event Log
- **Collection Method:** Wazuh Agent
- **Analysis Tool:** OpenSearch Dashboards (Discover)

This environment simulates a centralized SOC monitoring setup with agent-based endpoint visibility.

---

## Detection Timeline

### Authentication Failures
- **Event ID:** 4625 (Failed Logon)
- Multiple failed login attempts occurred on the same user account within a short time window.

### Successful Authentication
- **Event ID:** 4624 (Successful Logon)
- A successful login followed shortly after the failed attempts on the same host and user.

### Process Execution
- **Event ID:** 4688 (Process Creation)
- **Process:** powershell.exe
- **Parent Process:** cmd.exe
- **User Context:** Standard user (socuser)
- **Privilege Level:** Limited token (non-administrative)

This sequence represents authentication followed by execution activity.

---

## Analysis and Correlation
Individually, each event type may be benign. Failed logins can result from user error, successful logins are routine, and PowerShell is a legitimate administrative tool. However, when correlated, the pattern suggests potential credential compromise followed by post-authentication activity.

Correlation was performed by reviewing event timestamps, user context, and host information to determine whether execution activity occurred shortly after authentication anomalies.

---

## MITRE ATT&CK Mapping
The observed behavior aligns with the following MITRE ATT&CK techniques:

- **Credential Access**
  - **T1110 – Brute Force**
- **Execution**
  - **T1059.001 – PowerShell**

Mapping detections to MITRE ATT&CK provides standardized context for understanding attacker behavior.

---

## Severity Assessment and Response
- **Severity:** Medium
- **SOC Actions:**
  - Reviewed authentication and execution events
  - Validated user and privilege context
  - Assessed command execution timing
  - Checked for additional suspicious activity

---

## Final Classification
The activity was classified as **benign**, as it was confirmed to be user-initiated testing within a controlled lab environment. No remediation actions were required.

---

## Key Takeaways
- Demonstrated effective event correlation across authentication and execution telemetry
- Validated endpoint visibility using process creation events
- Applied SOC-style investigation methodology
- Reinforced the importance of behavioral detection over single-event alerts
