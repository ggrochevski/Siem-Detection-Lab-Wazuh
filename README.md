# SIEM Detection & SOC Monitoring Lab (Wazuh)

## Overview
This project demonstrates a Security Operations Center (SOC) detection lab built using **Wazuh SIEM** to monitor a Windows endpoint. The lab focuses on collecting, analyzing, and correlating Windows security events to detect authentication anomalies and suspicious process execution behavior commonly associated with real-world attacks.

The goal of this project is to showcase hands-on SOC skills, including endpoint onboarding, log analysis, event correlation, and detection engineering.

---

## Lab Architecture
- **SIEM Platform:** Wazuh (All-in-One deployment)
- **Endpoint:** Windows 11
- **Log Source:** Windows Security Event Log
- **Collection Method:** Wazuh Agent
- **Analysis Tool:** OpenSearch Dashboards (Discover)
- **Networking:** Host-only network for SIEM communication, NAT for internet access

---

## Data Sources & Telemetry
The following Windows Security Event IDs were collected and analyzed:

| Event ID | Description |
|--------|-------------|
| 4625 | Failed logon attempt |
| 4624 | Successful logon |
| 4688 | Process creation |

Advanced Windows Audit Policies were enabled to ensure high-fidelity security telemetry.

---

## Detection Use Case
### Suspicious Authentication Followed by PowerShell Execution

**Scenario:**  
Multiple failed login attempts were observed on a Windows endpoint, followed by a successful authentication and subsequent PowerShell execution. This behavior mirrors common attacker workflows involving credential guessing and post-authentication reconnaissance.

**Detection Logic (Conceptual):**
- Repeated failed logins (4625) within a short time window
- A successful login (4624) on the same host and user
- PowerShell process creation (4688) shortly after authentication

---

## Analysis & Investigation
Events were analyzed using OpenSearch Dashboards to correlate authentication activity with process execution. Process parent-child relationships, user context, and privilege level were reviewed to assess the nature of the activity.

The behavior was determined to be **benign lab activity**, but the detection logic reflects real-world SOC investigation workflows.

---

## MITRE ATT&CK Mapping
- **T1110 – Brute Force**
- **T1059.001 – PowerShell**

---

## Key Takeaways
- Built and configured a functional SIEM lab environment
- Onboarded and monitored a Windows endpoint using agent-based telemetry
- Correlated authentication and execution events to detect suspicious behavior
- Applied SOC-style investigation techniques and MITRE ATT&CK mapping

---

## Future Improvements
- Enable full command-line logging for enhanced execution visibility
- Create custom Wazuh detection rules based on observed behavior
- Add additional endpoint detection scenarios

---

## Disclaimer
This project was conducted in a controlled lab environment for educational purposes. No malicious activity was performed.
