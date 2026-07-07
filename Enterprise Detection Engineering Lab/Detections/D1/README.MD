Detection 01: Suspicious PowerShell Execution

Overview

PowerShell is a legitimate Windows scripting tool used by administrators and IT teams. However, attackers often abuse PowerShell to execute commands, perform reconnaissance, and run malicious scripts.

This detection focuses on monitoring PowerShell execution activity on a Windows endpoint.

⸻

Objective

Detect and analyze PowerShell activity by collecting Windows and Sysmon telemetry.

⸻

MITRE ATT&CK Mapping

Technique: Command and Scripting Interpreter: PowerShell MITRE ID: T1059.001

⸻

Lab Environment

Windows 11 Virtual Machine
VMware Fusion
Sysmon
Windows Event Logs
PowerShell Logging
⸻

Activity Performed

The following PowerShell commands were executed to generate telemetry:

whoami hostname Get-Process Get-Service Get-LocalUser

These commands simulate normal PowerShell activity that could also appear during attacker reconnaissance.

⸻

Telemetry Generated

Windows Security Event

Event ID 4688 - Process Creation

Shows when a new process is created.

Important information:

Process name
User account
Parent process
Command line
⸻

Sysmon Event

Sysmon Event ID 1 - Process Creation

Provides detailed process information.

Important fields:

Image
Command Line
Parent Image
User
⸻

PowerShell Logging

Event ID 4104 - PowerShell Script Block Logging

Shows PowerShell commands/scripts that were executed.

⸻

Screenshots

Screenshots included:

PowerShell commands executed
Sysmon Event ID 1
Windows Security Event ID 4688
PowerShell Event ID 4104
⸻

Detection Logic

Monitor PowerShell execution and collect:

User who executed PowerShell
Command executed
Parent process
Time of execution
PowerShell execution alone is not malicious, so additional context is required during investigation.

⸻

Investigation Steps

When investigating PowerShell activity:

Identify the user who executed PowerShell.
Review the command that was executed.
Check the parent process.
Determine if the activity is expected.
Review other endpoint activity if suspicious.
⸻

False Positives

Common legitimate PowerShell usage:

System administrators
IT automation scripts
Software deployment tools
⸻

Response Actions

If suspicious:

Investigate the user account.
Review PowerShell commands.
Check related processes.
Review additional security alerts.
⸻

Lessons Learned

This detection helped me understand:

How PowerShell creates security telemetry.
How Sysmon captures process activity.
How Windows Event Logs help SOC analysts investigate endpoint activity.
Why PowerShell monitoring is important in enterprise environments.
