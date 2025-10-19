# Install Sysmon & Configure Log Forwarding

## Objective
Collect detailed Windows process and security events with Sysmon and forward them to Splunk for analysis.

## Prerequisites
- Windows host with Administrator access  
- Internet access to download Sysmon and optional configs  
- Splunk instance (or Splunk Universal Forwarder) available to receive logs

## Table of Contents
1. Download Sysmon  
2. Install Sysmon (default & recommended config)  
3. Configure Splunk to collect Sysmon logs  
4. Verify ingestion in Splunk  
5. Evidence & deliverables  
6. References

---

## 1. Download Sysmon
1. Go to the official Sysinternals page:  
   https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon  
2. Save and extract the ZIP to a folder, e.g. `C:\Tools\Sysmon`.

---

## 2. Install Sysmon

### Basic install (default config)
Run Command Prompt as Administrator and execute:
```bash
sysmon -accepteula -i
```

### Recommended: install with SwiftOnSecurity config
1. Clone the community config:
```bash
git clone https://github.com/SwiftOnSecurity/sysmon-config.git
cd sysmon-config
```
2. Install Sysmon with the exported config:
```bash
sysmon -accepteula -i sysmonconfig-export.xml
```

Notes:
- To update config later: `sysmon -c sysmonconfig-export.xml`
- To uninstall: `sysmon -u`

---

## 3. Configure Splunk to Collect Sysmon Logs

Option A — Splunk Enterprise (Web UI)
1. In Splunk Web: Settings → Data Inputs → Local Event Logs → Add new  
2. Add these channels:
   - Microsoft-Windows-Sysmon/Operational  
   - Security  
3. Set target index (e.g., `main` or custom index)

Option B — Splunk Universal Forwarder (Windows)
1. Install Universal Forwarder on the Windows host.  
2. Configure inputs.conf to collect the Sysmon channel:
```ini
[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = 0
index = main
```
3. Restart the forwarder service.

---

## 4. Verify Logs in Splunk

Search examples:
```spl
index=main sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" | stats count by EventID, Image
```
Or show recent Sysmon events:
```spl
index=main source="WinEventLog:Microsoft-Windows-Sysmon/Operational" | head 50
```

Common Sysmon Event IDs:
- 1 — Process Create  
- 3 — Network Connection  
- 11 — FileCreate (or FileCreateStreamHash)  
- 7 — Image Loaded

If you see these events, forwarding is working.


