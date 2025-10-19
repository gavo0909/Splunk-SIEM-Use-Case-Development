# Data-ingestion — Log Verification Checks

## 1. Basic Event Count Check

Run this query:
```spl
index=main | stats count by EventCode
```

- Checks whether any events exist in the "main" index.
- Results show counts grouped by EventCode.
- If output is non-zero, Splunk is receiving logs.

<img src="./media/image1.png" alt="Event count screenshot" width="800" />

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

<img src="./media/image2.png" alt="Security logs screenshot" width="800" />

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
