# Detections (Wazuh SIEM)

This page documents the detection use cases validated in the lab using Windows Security Event Logs collected by the Wazuh agent.

---

## Detection Use Case 1: Authentication Anomalies (Failures → Success)

### Goal
Identify possible credential guessing or brute-force behavior by correlating repeated failed logons with a subsequent successful logon.

### Data Source
- Windows Security Event Log
- Wazuh agent on WIN-ENDPOINT-01

### Key Event IDs
- **4625** = Failed logon
- **4624** = Successful logon

### Detection Logic (Conceptual)
Trigger investigation when:
- ≥ 5 failed logons (4625) occur within a short window (ex: 5 minutes), and
- a successful logon (4624) occurs shortly after on the same host/user.

### MITRE ATT&CK
- **T1110 – Brute Force** (Credential Access)

### Analyst Notes / Tuning
Potential false positives include user password mistakes. Tuning options:
- raise threshold to 8–10 failures
- require repeated failures across multiple usernames
- alert only outside normal hours

---

## Detection Use Case 2: Suspicious PowerShell Execution

### Goal
Detect PowerShell execution patterns commonly used in attacker tradecraft, especially following authentication anomalies.

### Data Source
- Windows Security Event Log (process creation)
- Wazuh agent on WIN-ENDPOINT-01

### Key Event IDs
- **4688** = Process creation

### Detection Indicators
- Process name: `powershell.exe`
- Parent process: `cmd.exe` (interactive execution path)
- Suspicious flags (if command-line logging is enabled):
  - `-NoProfile`
  - `-WindowStyle Hidden`
  - `-EncodedCommand`

### MITRE ATT&CK
- **T1059.001 – PowerShell** (Execution)

### Analyst Notes / Tuning
PowerShell is legitimate, so context matters. Consider:
- allowlisting known admin scripts/users
- focusing on encoded/hidden flags
- correlating with auth anomalies or unusual logon types
