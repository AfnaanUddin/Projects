# Detection 07: Windows Service Creation
## Overview

Windows Services are background processes that run automatically on a system. While services are commonly used by legitimate applications, attackers can abuse them to maintain persistence after compromising a machine.
This detection focuses on identifying newly created Windows Services.

---

## Objective

Detect unauthorized Windows Services created for persistence or malicious execution.

---

## MITRE ATT&CK Mapping

**Technique:** Create or Modify System Process: Windows Service  
**MITRE ID:** T1543.003

---

## Lab Environment

- Windows 11 Virtual Machine
- VMware Fusion
- Sysmon
- Windows Event Logs

---

## Activity Performed

A new Windows Service was created using the following command:

```powershell
sc.exe create SecurityLabService binPath= "C:\Windows\System32\notepad.exe" start= auto

Telemetry Generated

Windows System Event ID 7045 - Service Created

Event ID 7045 records when a new Windows Service is installed.

Important information:

* Service name
* Service path
* Startup type
* Account information

Sysmon Event ID 1 - Process Creation

Sysmon captured the execution of sc.exe used to create the service.

Important information:

* Process name
* Command line
* Parent process
* User account

Detection Logic

Monitor for:

* New Windows Services being created.
* Services with suspicious executable paths.
* Services created by unusual users.
* Services configured for automatic startup.

Suspicious examples:

* Executables running from user directories.
* Unknown binaries.
* Services created outside normal software installation processes.

⸻

Investigation Steps

1. Identify the newly created service.
2. Review the service executable path.
3. Determine who created the service.
4. Verify whether the service creation was authorized.
5. Investigate related processes and activity.

⸻

False Positives

Legitimate service creation may occur during:

* Software installation.
* Windows updates.
* Security tool deployment.
* Enterprise application setup.

⸻

Response Actions

If the service is suspicious:

* Stop and remove the service.
* Investigate the executable associated with the service.
* Check the system for additional persistence mechanisms.
* Review user activity that created the service.

⸻

Lessons Learned

This detection helped me understand:

* How attackers abuse Windows Services for persistence.
* How Event ID 7045 provides visibility into service creation.
* How Sysmon helps identify processes responsible for creating services.
* Why investigating executable paths and context is important in security alerts.
