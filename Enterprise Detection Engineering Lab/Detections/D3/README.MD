Detection 03: New Local Administrator Account

Overview

Attackers who gain access to a Windows system may create a new local administrator account to maintain persistent access. Monitoring new account creation and administrator group membership helps detect this type of activity.

⸻

Objective

Detect the creation of a new local user account and identify when it is added to the local Administrators group.

⸻

MITRE ATT&CK Mapping

Technique: Create Account
MITRE ID: T1136

Related Technique: Account Manipulation
MITRE ID: T1098

⸻

Lab Environment

* Windows 11 Virtual Machine
* VMware Fusion
* Sysmon
* Windows Security Logs

⸻

Activity Performed

A new local user account was created and then added to the local Administrators group using the following commands:

net user TestU Password123! /add
net localgroup Administrators TestU /add

This simulates how an attacker could create a new administrator account to maintain access to a compromised system.

⸻

Telemetry Generated

Windows Security Event ID 4720 - User Account Created

Windows recorded the creation of the new local user account.

Screenshot:

⸻

Windows Security Event ID 4732 - User Added to Administrators Group

Windows recorded the new user being added to the local Administrators group.

Screenshot:

⸻

Sysmon Event ID 1 - Process Creation

Sysmon recorded the execution of the net user and net localgroup commands used to create the account and assign administrator privileges.

Screenshot:

⸻

Detection Logic

Monitor for:

* Event ID 4720 (New user account created)
* Event ID 4732 (User added to the Administrators group)
* Sysmon Event ID 1 showing net user or net localgroup commands

These events together may indicate an attacker attempting to establish persistence on a system.

⸻

Investigation Steps

1. Identify who created the new account.
2. Verify whether the account creation was authorized.
3. Check if the account was added to the Administrators group.
4. Review recent activity from the same user or device.
5. Investigate any additional suspicious activity on the endpoint.

⸻

False Positives

Legitimate account creation may occur during:

* IT administration
* System deployment
* Help desk support
* Device provisioning

⸻

Response Actions

If the activity is suspicious:

* Disable or remove the unauthorized account.
* Review administrator group membership.
* Investigate the source of the account creation.
* Check for other persistence techniques on the system.

⸻

Lessons Learned

This detection helped me understand:

* How Windows records local account creation.
* How administrator privileges are assigned.
* How Sysmon captures the commands used to create accounts.
* Why monitoring administrator account creation is important for detecting persistence.
