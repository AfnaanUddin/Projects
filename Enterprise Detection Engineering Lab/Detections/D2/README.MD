Detection 02: PowerShell Encoded Command

Overview

Attackers often use PowerShell because it is already available on Windows systems. One common technique is using encoded commands to hide the actual PowerShell instructions being executed.

This detection focuses on identifying PowerShell executions that use encoded commands.

⸻

Objective

Detect suspicious PowerShell activity where commands are hidden using encoding.

⸻

MITRE ATT&CK Mapping

Technique: Obfuscated Files or Information
MITRE ID: T1027

Related Technique: Command and Scripting Interpreter: PowerShell
MITRE ID: T1059.001

⸻

Lab Environment

* Windows 11 Virtual Machine
* VMware Fusion
* Sysmon
* Windows Security Logs
* PowerShell Script Block Logging

⸻

Activity Performed

A PowerShell command was encoded using Base64 and executed using:

powershell.exe -EncodedCommand <encoded_command>

The purpose was to simulate how attackers may attempt to hide PowerShell activity.

⸻

Telemetry Generated

Sysmon Event ID 1 - Process Creation

Sysmon captured the PowerShell execution.

Important fields:

* Process name
* Command line
* Parent process
* User account

The command line showed:

powershell.exe -EncodedCommand

⸻

Windows Security Event ID 4688 - Process Creation

Windows recorded the creation of the PowerShell process.

Important information:

* New process name
* User account
* Command line


⸻

PowerShell Event ID 4104 - Script Block Logging

PowerShell logging captured the script content that was executed.

This helps analysts understand what the encoded command actually performed.

⸻

Detection Logic

Monitor PowerShell execution where the command line contains:

-EncodedCommand

or:

-enc

Encoded PowerShell activity is not always malicious, but it should be reviewed because attackers commonly use it to hide commands.

⸻

Investigation Steps

When investigating an encoded PowerShell alert:

1. Identify the user who executed PowerShell.
2. Review the command line for encoded parameters.
3. Check PowerShell Event ID 4104 for the actual script content.
4. Review the parent process that launched PowerShell.
5. Determine whether the activity is expected.

⸻

False Positives

Possible legitimate uses include:

* Administrative scripts
* Software deployment tools
* Automation systems

⸻

Response Actions

If the activity is suspicious:

* Investigate the user account.
* Decode and review the PowerShell command.
* Check related processes and network activity.
* Look for additional suspicious activity on the endpoint.

⸻

Lessons Learned

This detection helped me understand:

* How attackers use PowerShell encoding to hide commands.
* How Sysmon provides process visibility.
* How Windows Event ID 4688 records process creation.
* How PowerShell Event ID 4104 helps reveal executed scripts.
* Why multiple telemetry sources are important for detection.
