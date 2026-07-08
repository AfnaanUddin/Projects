Detection 05: Scheduled Task Persistence

Overview

Scheduled Tasks are a legitimate Windows feature used for automation and system management. However, attackers can abuse scheduled tasks to maintain persistence on compromised systems.

This detection focuses on identifying the creation of new scheduled tasks that could be used for unauthorized execution.

⸻

Objective

Detect the creation of scheduled tasks and analyze whether they may be used for persistence.

⸻

MITRE ATT&CK Mapping

Technique: Scheduled Task/Job
MITRE ID: T1053

Sub-technique: Scheduled Task
MITRE ID: T1053.005

⸻

Lab Environment

* Windows 11 Virtual Machine
* VMware Fusion
* Sysmon
* Windows Security Event Logs

⸻

Activity Performed

A scheduled task was created using the Windows Task Scheduler command:

schtasks /create /tn "SecurityLabTask" /tr "powershell.exe -command Get-Date" /sc minute /mo 5

The task was created to simulate how an attacker could establish persistence using Windows built-in tools.

⸻

Telemetry Generated

Windows Security Event ID 4698 - Scheduled Task Created

Event ID 4698 records when a scheduled task is created.

Important information:

* Task name
* User who created the task
* Command/action being executed

Screenshot:

⸻

Sysmon Event ID 1 - Process Creation

Sysmon captured the execution of schtasks.exe used to create the scheduled task.

Important fields:

* Process name
* Command line
* Parent process
* User account

Screenshot:

⸻

Detection Logic

Monitor for:

* New scheduled tasks being created.
* Scheduled tasks executing suspicious commands.
* Tasks created by unusual users.
* Tasks running PowerShell, scripts, or unknown executables.

A scheduled task is not automatically malicious, but unexpected task creation should be investigated.

⸻

Investigation Steps

1. Identify who created the scheduled task.
2. Review the task name and scheduled action.
3. Check what program or command the task executes.
4. Determine if the task creation was authorized.
5. Investigate the user and system activity around the same time.

⸻

False Positives

Legitimate scheduled tasks may be created by:

* Windows updates
* Antivirus software
* Backup applications
* IT automation tools
* System administrators

⸻

Response Actions

If the scheduled task is suspicious:

* Disable or remove the task.
* Investigate the creating account.
* Analyze the executed command or file.
* Review additional persistence mechanisms.

⸻

Lessons Learned

This detection helped me understand:

* How attackers abuse legitimate Windows features for persistence.
* How scheduled tasks are created and monitored.
* How Windows Event ID 4698 provides visibility into task creation.
* How Sysmon helps identify the processes responsible for creating persistence mechanisms.
