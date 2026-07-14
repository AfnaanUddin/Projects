# Detection 09: Microsoft Defender Tampering

## Overview

Attackers often attempt to disable antivirus or endpoint protection after gaining access to a system. Disabling Microsoft Defender helps attackers avoid detection and continue their activities without interruption.

This detection focuses on identifying attempts to modify Microsoft Defender settings.

---

## Objective

Detect attempts to disable or modify Microsoft Defender protection settings.

---

## MITRE ATT&CK Mapping

**Technique:** Impair Defenses  

**MITRE ID:** T1562.001

---

## Lab Environment

- Windows 11 Virtual Machine

- VMware Fusion

- Microsoft Defender

- Sysmon

- PowerShell

---

## Activity Performed

Microsoft Defender Real-Time Monitoring was temporarily disabled using PowerShell.

Command used:

```powershell

Set-MpPreference -DisableRealtimeMonitoring $true

```

The setting was verified and then restored to its original state.

```powershell

Set-MpPreference -DisableRealtimeMonitoring $false

```

This simulated how an attacker may attempt to weaken endpoint security after compromising a system.

---

## Telemetry Generated

### Microsoft Defender Configuration

The Defender configuration was checked before and after the change using:

```powershell

Get-MpPreference | Select-Object DisableRealtimeMonitoring

```

---

### Sysmon Event ID 1 - Process Creation

Sysmon captured the PowerShell process used to modify Microsoft Defender settings.

Important information:

- Process name

- Command line

- User account

- Timestamp

---

## Detection Logic

Monitor for:

- PowerShell commands modifying Microsoft Defender settings.

- Attempts to disable Real-Time Monitoring.

- Changes to Microsoft Defender configuration.

- Unusual administrative activity targeting security controls.

---

## Investigation Steps

1. Identify who executed the PowerShell command.

2. Review which Defender setting was modified.

3. Verify whether the change was authorized.

4. Check for additional suspicious activity on the endpoint.

5. Confirm that Microsoft Defender protection has been restored.

---

## False Positives

Legitimate changes may occur during:

- Security testing

- IT administration

- Software troubleshooting

- Enterprise security management

---

## Response Actions

If suspicious:

- Re-enable Microsoft Defender protection.

- Investigate the user or process responsible.

- Review the system for additional malicious activity.

- Check for other attempts to disable security controls.

---

## Lessons Learned

This detection helped me understand:

- How attackers attempt to impair security defenses.

- How Microsoft Defender settings can be monitored.

- How PowerShell can be used to modify Defender configuration.

- Why disabling security tools is an important indicator of compromise.
