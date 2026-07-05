# 🛡️ Enterprise Detection Engineering Lab

## Overview

This project is a hands-on detection engineering lab built in a Windows 11 virtual machine using Sysmon and Windows Security Event Logging.

The objective is to simulate real-world SOC (Security Operations Center) workflows by generating endpoint telemetry, analyzing system behavior, and building detection logic based on actual system activity.

This lab focuses on understanding how attackers generate telemetry and how defenders detect and investigate that behavior using industry-standard tools.

---

## 🎯 Objectives

- Build a Windows-based SOC detection environment
- Enable and analyze Sysmon telemetry
- Study Windows Security Event Logs
- Simulate real endpoint activity
- Analyze process execution and authentication events
- Build detection logic from raw telemetry
- Map behaviors to MITRE ATT&CK framework

---

## 🧪 Lab Environment

- Windows 11 Virtual Machine (VMware Fusion)
- Sysmon (Sysinternals)
- Windows Event Viewer
- PowerShell & Command Prompt
- Isolated virtual network environment

---

## 📊 Telemetry Sources

### Windows Security Logs
- 4624 → Successful logon
- 4625 → Failed logon
- 4720 → User creation
- 4732 → Group modification

### Sysmon Logs
- Event ID 1 → Process creation
- Event ID 3 → Network connections
- Event ID 7 → Image loads
- Event ID 10 → Process access
- Event ID 11 → File creation

---

# 🔍 DETECTIONS (1–10)

---

## 🔥 Detection #1 — Successful Logon (4624)

Detect successful authentication events.

**MITRE:** T1078 – Valid Accounts

📸 Evidence:
![4624 Logon](screenshots/detection-1-4624.png)

---

## 🔥 Detection #2 — Failed Logon Attempts (4625)

Detect brute-force or invalid login attempts.

**MITRE:** T1110 – Brute Force

📸 Evidence:
![4625 Failed Logon](screenshots/detection-2-4625.png)

---

## 🔥 Detection #3 — User Account Creation (4720)

Detect creation of new local users.

**MITRE:** T1136 – Create Account

📸 Evidence:
![User Creation](screenshots/detection-3-user.png)

---

## 🔥 Detection #4 — Privilege Escalation (4732)

Detect users added to administrator groups.

**MITRE:** T1068 – Privilege Escalation

📸 Evidence:
![Privilege Escalation](screenshots/detection-4-admin.png)

---

## 🔥 Detection #5 — Group Membership Changes

Monitor changes to local security groups.

📸 Evidence:
![Group Change](screenshots/detection-5-group.png)

---

## 🔥 Detection #6 — Logon Session Analysis

Analyze interactive vs remote logins.

📸 Evidence:
![Logon Sessions](screenshots/detection-6-logons.png)

---

## 🔥 Detection #7 — Authentication Correlation

Correlate failed logins followed by successful logins.

📸 Evidence:
![Auth Correlation](screenshots/detection-7-correlation.png)

---

## 🔥 Detection #8 — Process Execution Monitoring (Sysmon Event ID 1)

Monitor all process creation activity.

Key fields:
- Image
- CommandLine
- ParentImage
- User

**MITRE:** T1059 – Command and Scripting Interpreter

📸 Evidence:
![Sysmon Event 1](screenshots/detection-8-sysmon.png)

---

## 🔥 Detection #9 — Suspicious PowerShell Execution

Detect PowerShell with risky arguments:
- -NoProfile
- -ExecutionPolicy Bypass
- -WindowStyle Hidden

**MITRE:** T1059.001 – PowerShell

📸 Evidence:
![PowerShell](screenshots/detection-9-powershell.png)

---

## 🔥 Detection #10 — Parent-Child Process Analysis

Detect unusual process chains such as:
- cmd.exe → powershell.exe
- explorer.exe → powershell.exe

**MITRE:** T1059 / T1204

📸 Evidence:
![Process Tree](screenshots/detection-10-parentchild.png)

---

## 🧠 Skills Demonstrated

- Windows event log analysis
- Sysmon telemetry analysis
- Endpoint process monitoring
- Authentication analysis
- Privilege escalation detection
- PowerShell behavior analysis
- SOC investigation workflow
- MITRE ATT&CK mapping
- Detection engineering fundamentals

---

## 📌 Status

🟡 In Progress — Expanding toward 15 detections
(Currently completed: 10)
