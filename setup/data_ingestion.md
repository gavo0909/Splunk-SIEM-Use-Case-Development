# Data-ingestion — Log Verification Checks

## 1. Basic Event Count Check

Run this query:
```spl
index=main | stats count by EventCode
```

- Checks whether any events exist in the "main" index.
- Results show counts grouped by EventCode.
- If output is non-zero, Splunk is receiving logs.

![image alt](https://github.com/gavo0909/Splunk-SIEM-Use-Case-Development/blob/eb858c1347f3f54bf03b61e3e16c216f870950bf/setup/1.png)

## 2. Verify Security Logs

Run this query:
```spl
index=main source="WinEventLog:Security"
```

- Checks that Windows Security logs are being ingested.
- Typical events:
  - 4624 — Successful logon
  - 4625 — Failed logon
  - 4688 — Process creation

![image alt](https://github.com/gavo0909/Splunk-SIEM-Use-Case-Development/blob/d350dcd814e068831bc8dd640d078f834b31f9f5/setup/2.png)
## 3. Verify Sysmon Logs

Run this query:
```spl
index=main source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
```

- Checks that Sysmon events are flowing in.
- Typical Sysmon event IDs:
  - 1 — Process creation
  - 3 — Network connection
  - 11 — File creation

<img src="./media/image3.png" alt="Sysmon logs screenshot" width="800" />
