# Detection 10: Shadow Copy Deletion

## Overview

Volume Shadow Copies are Windows backups that allow users to restore previous versions of files. Attackers, especially ransomware operators, often delete Shadow Copies to prevent recovery after encrypting a system.

This detection focuses on monitoring the use of `vssadmin.exe`, a tool commonly abused to manage or delete Shadow Copies.

---

## Objective

Detect the use of `vssadmin.exe` and identify activity that may indicate attempts to inhibit system recovery.

---

## MITRE ATT&CK Mapping

**Technique:** Inhibit System Recovery  

**MITRE ID:** T1490

---

## Lab Environment

- Windows 11 Virtual Machine

- VMware Fusion

- Sysmon

- PowerShell

---

## Activity Performed

The following command was executed to safely query existing Shadow Copies:

```cmd

vssadmin list shadows

```

This simulated attacker interaction with the Volume Shadow Copy Service without modifying or deleting any Shadow Copies.

---

## Telemetry Generated

### Sysmon Event ID 1 - Process Creation

Sysmon captured the execution of `vssadmin.exe`.

Important information:

- Process name

- Command line

- Parent process

- User account

- Timestamp

---

### Shadow Copy Query

The output of the `vssadmin list shadows` command was recorded to verify successful execution.

---

## Detection Logic

Monitor for:

- Execution of `vssadmin.exe`

- Commands attempting to delete Shadow Copies

- Administrative commands related to Volume Shadow Copy Service

High-risk examples:

```cmd

vssadmin delete shadows /all /quiet

```

```cmd

wmic shadowcopy delete

```

---

## Investigation Steps

1. Identify who executed `vssadmin.exe`.

2. Review the command line arguments.

3. Determine whether Shadow Copies were deleted or only queried.

4. Investigate additional suspicious activity on the endpoint.

5. Check for signs of ransomware or other destructive behavior.

---

## False Positives

Legitimate use may occur during:

- System administration

- Backup management

- IT maintenance

- Disaster recovery testing

---

## Response Actions

If suspicious:

- Investigate the user or process responsible.

- Verify whether Shadow Copies were removed.

- Isolate the endpoint if ransomware activity is suspected.

- Review backup integrity and system recovery options.

---

## Lessons Learned

This detection helped me understand:

- What Volume Shadow Copies are.

- Why ransomware attempts to delete them.

- How Sysmon detects the execution of `vssadmin.exe`.

- Why monitoring recovery-related commands is important for detecting ransomware activity.
