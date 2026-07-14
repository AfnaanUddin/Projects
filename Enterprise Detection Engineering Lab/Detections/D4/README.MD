Detection 04: Failed Logon Brute Force Detection

Overview

Attackers often attempt to gain unauthorized access by repeatedly guessing passwords. Monitoring failed authentication attempts helps security teams detect possible brute-force or password-spraying attacks.

This detection focuses on identifying failed and successful Windows login activity.

⸻

Objective

Detect suspicious authentication activity by analyzing failed login attempts and successful logins on a Windows endpoint.

⸻

MITRE ATT&CK Mapping

Technique: Brute Force
MITRE ID: T1110

Related Techniques:

* T1110.001 — Password Guessing
* T1110.003 — Password Spraying

⸻

Lab Environment

* Windows 11 Virtual Machine
* VMware Fusion
* Windows Security Event Logs

⸻

Activity Performed

A test user account was created and multiple incorrect password attempts were performed to generate failed authentication events.

A successful login was then performed to observe successful authentication telemetry.

⸻

Telemetry Generated

Windows Security Event ID 4625 - Failed Logon

Event ID 4625 records unsuccessful login attempts.

Important information:

* Account name
* Failure reason
* Logon type
* Source information


⸻

Windows Security Event ID 4624 - Successful Logon

Event ID 4624 records successful authentication events.

Important information:

* Account name
* Logon type
* Authentication details

⸻

Detection Logic

Monitor for:

* Multiple Event ID 4625 failures within a short time period.
* Multiple failed login attempts against one account.
* Multiple accounts being targeted from the same source.
* A successful login occurring after many failed attempts.

A high number of failed logins may indicate brute-force or password-spraying activity.

⸻

Investigation Steps

1. Identify the targeted account.
2. Review the number of failed login attempts.
3. Check the source of the authentication attempts.
4. Determine whether the activity is expected.
5. Check if a successful login occurred after multiple failures.
6. Investigate additional activity from the same user or device.

⸻

False Positives

Possible legitimate causes:

* Users entering incorrect passwords.
* Forgotten credentials.
* Expired passwords.
* Automated services using outdated credentials.

⸻

Response Actions

If the activity is suspicious:

* Verify the user account activity.
* Reset compromised credentials if required.
* Investigate the source device or IP address.
* Monitor for additional suspicious authentication activity.

⸻

Lessons Learned

This detection helped me understand:

* How Windows records authentication activity.
* The difference between failed and successful logon events.
* How SOC analysts investigate authentication attacks.
* Why authentication telemetry is important for detecting unauthorized access.
