# Siem-for-analyzing-windows-logs-

## Objective

The Windows Event Log SIEM Lab project aimed to design and implement a centralised log monitoring environment using Splunk. The objective was to ingest Windows Event Logs via Splunk Universal Forwarder, index the data into a custom index, and build operational dashboards to visualise system activity and security-relevant telemetry.

This project demonstrates practical experience in log ingestion, parsing, search processing language (SPL), and dashboard creation within a SIEM platform.

## Skills Learned

* Practical deployment of Splunk Enterprise and Universal Forwarder

* Configuration of log forwarding using inputs.conf and outputs.conf

* Creation and management of custom Splunk indexes

* Troubleshooting field extraction and parsing issues

* Writing SPL queries for aggregation and visualisation

* Building operational dashboards for log monitoring

* Basic detection engineering using Windows Event Codes

## Tools Used

Splunk Enterprise (Free License Mode)

Splunk Universal Forwarder (Windows)

Windows Event Viewer

Windows PowerShell (for test event generation)

SPL (Search Processing Language)

## Architecture Overview

Single-machine lab environment:

Windows Machine
→ Splunk Universal Forwarder
→ Splunk Enterprise (localhost:9997 receiving port)
→ Custom index: windows_logs
→ Dashboard visualisation

## Configuration Details

### Inputs.conf
``` bash
[WinEventLog://Application]
disabled = 0
index = windows_logs

[WinEventLog://System]
disabled = 0
index = windows_logs

[WinEventLog://Security]
disabled = 0
index = windows_logs
```

### Outputs.conf
```bash 
[tcpout]
defaultGroup = default-autolb-group

[tcpout:default-autolb-group]
server = localhost:9997

[tcpout-server://localhost:9997]
```
## Key SPL Queries Used
### Total Errors
``` bash
index=windows_logs EventCode=1000 | stats count
```

### Top Event Codes
``` bash
index=windows_logs | stats count by EventCode
```

### Events by Host
``` bash
index=windows_logs | stats count by ComputerName
```

### Top Accounts Observed
``` bash
index=windows_logs | stats count by Account_Name
```

### Event Volume Over Time
``` bash
index=windows_logs | timechart count
```

## Dashboard Panels
<img width="1919" height="921" alt="Screenshot 2026-02-11 222848" src="https://github.com/user-attachments/assets/59a3c6fb-8f6c-43c4-bc93-b9562cde8580" />


## Troubleshooting Highlights

* Identified missing field aggregation due to incorrect field names.

* Used ` fieldsummary ` to validate searchable fields.
  
* Resolved index visibility issues caused by incomplete configuration.
  
* Managed Splunk license transition from Enterprise Trial to Free Mode.

* Validated forwarder health using splunk.exe CLI.


## Outcome
Successfully built a functional Windows log ingestion pipeline using Splunk, created operational dashboards, and validated end-to-end SIEM functionality in a lab environment
