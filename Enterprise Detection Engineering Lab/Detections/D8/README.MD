# Detection 08: WMI Execution

## Overview

Windows Management Instrumentation (WMI) is a legitimate Windows feature used for system administration and management. However, attackers can abuse WMI to execute commands and perform malicious activity without using traditional malware.

This detection focuses on identifying suspicious process execution through WMI.

---

## Objective

Detect processes created through WMI that may indicate attacker activity or Living-off-the-Land techniques.

---

## MITRE ATT&CK Mapping

**Technique:** Windows Management Instrumentation  
**MITRE ID:** T1047

---

## Lab Environment

- Windows 11 Virtual Machine
- VMware Fusion
- Sysmon
- PowerShell CIM/WMI

---

## Activity Performed

A process was created using Windows Management Instrumentation through PowerShell.

Command used:

```powershell
Invoke-CimMethod -ClassName Win32_Process -MethodName Create -Arguments @{CommandLine="notepad.exe"}

Telemetry Generated

Sysmon Event ID 1 - Process Creation

Sysmon captured the process creation activity.

Important information:

* Process name
* Parent process
* Command line
* User account
* Timestamp

Detection Logic

Monitor for:

* Processes created through WMI.
* WMI launching scripting engines such as PowerShell or Command Prompt.
* Suspicious parent-child process relationships.

Examples:

Suspicious:
WmiPrvSE.exe
      ↓
powershell.exe
      ↓
Encoded command

Investigation Steps

1. Identify the process created through WMI.
2. Review the parent process.
3. Analyze the command line arguments.
4. Determine if the activity was expected.
5. Investigate additional activity from the same user or machine.

⸻

False Positives

Legitimate WMI usage may occur from:

* System administrators
* Monitoring tools
* Enterprise management software
* IT automation systems

⸻

Response Actions

If suspicious:

* Investigate the user and process involved.
* Review related PowerShell or command execution activity.
* Check for additional attacker activity on the endpoint.

⸻

Lessons Learned

This detection helped me understand:

* How attackers abuse legitimate Windows tools.
* How WMI can be used for remote and local execution.
* How Sysmon Event ID 1 provides visibility into process relationships.
* Why parent-child process analysis is important in detection engineering.
