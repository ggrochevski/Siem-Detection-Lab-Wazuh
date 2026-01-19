# Authentication Queries (Windows Security Logs)

Use these in OpenSearch Dashboards (Discover) with the `wazuh-alerts-*` index pattern.

## Failed logons (4625)
**Lucene:**

data.win.system.eventID:4625 AND agent.name:"WIN-ENDPOINT-01"

**DQL:**

data.win.system.eventID == 4625 AND agent.name == "WIN-ENDPOINT-01"

## Successful logons (4624)
**Lucene:**

data.win.system.eventID:4624 AND agent.name:"WIN-ENDPOINT-01"

**DQL:**

data.win.system.eventID == 4624 AND agent.name == "WIN-ENDPOINT-01"

## Correlation workflow (manual)
1. Run 4625 query (failures) and note the time range + username  
2. Run 4624 query (successes) and check if a success occurs shortly after failures for the same user/host
