# Execution Queries (Process Creation)

Use these in OpenSearch Dashboards (Discover) with the `wazuh-alerts-*` index pattern.

## Process creation (4688)
**Lucene:**
data.win.system.eventID:4688 AND agent.name:"WIN-ENDPOINT-01"

makefile
Copy code

**DQL:**
data.win.system.eventID == 4688 AND agent.name == "WIN-ENDPOINT-01"

makefile
Copy code

## PowerShell executions
**Lucene:**
data.win.system.eventID:4688 AND agent.name:"WIN-ENDPOINT-01" AND data.win.eventdata.newProcessName:*powershell.exe

makefile
Copy code

**DQL:**
data.win.system.eventID == 4688 AND agent.name == "WIN-ENDPOINT-01" AND data.win.eventdata.newProcessName LIKE "*powershell.exe"

makefile
Copy code

## Parent-child check (cmd → powershell)
**Lucene:**
data.win.system.eventID:4688 AND agent.name:"WIN-ENDPOINT-01" AND data.win.eventdata.parentProcessName:*cmd.exe AND data.win.eventdata.newProcessName:*powershell.exe

makefile
Copy code

**DQL:**
data.win.system.eventID == 4688 AND agent.name == "WIN-ENDPOINT-01" AND data.win.eventdata.parentProcessName LIKE "*cmd.exe" AND data.win.eventdata.newProcessName LIKE "*powershell.exe"

Copy code
