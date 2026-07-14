Detection 06: Registry Run Key Persistence

Overview

Attackers can use Windows Registry Run Keys to automatically execute programs when a user logs into the system. This allows them to maintain persistence without manually starting the program.

⸻

Objective

Detect unauthorized programs added to Windows Registry Run Keys.

⸻

MITRE ATT&CK Mapping

Technique: Registry Run Keys / Startup Folder
MITRE ID: T1547.001

⸻

Lab Environment

* Windows 11 Virtual Machine
* VMware Fusion
* Sysmon
* Windows Registry

⸻

Activity Performed

A Registry Run Key was created to automatically launch Notepad when the user logs in.

Command used: reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v SecurityLabRun /t REG_SZ /d "notepad.exe" /f
This simulated how an attacker could create persistence using Windows Registry.

_____

Telemetry Generated

Sysmon Event ID 13 - Registry Value Set

Sysmon detected the registry modification.

Important information:

* Registry path modified
* Value created
* Process responsible for the change

_____

Detection Logic:
Monitor for changes to:
HKCU\Software\Microsoft\Windows\CurrentVersion\Run and HKLM\Software\Microsoft\Windows\CurrentVersion\Run

Investigation Steps

1. Identify the registry key that was modified.
2. Check what program was added.
3. Determine which user or process made the change.
4. Verify if the change was legitimate.
5. Look for other persistence activity.

⸻

False Positives

Common legitimate changes:

* Software installations
* System updates
* Enterprise applications
* User-installed programs

⸻

Response Actions

If suspicious:

* Remove the unauthorized Run Key.
* Investigate the associated program.
* Check the endpoint for additional persistence techniques.

⸻

Lessons Learned

This detection helped me understand:

* How attackers use Registry Run Keys for persistence.
* How Sysmon Event ID 13 provides visibility into registry changes.
* Why monitoring startup locations is important for detecting persistence techniques.
