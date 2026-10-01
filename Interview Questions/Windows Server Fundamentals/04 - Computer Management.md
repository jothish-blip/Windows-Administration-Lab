# Computer Management - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../02%20-%20Windows%20Server%20Fundamentals/04%20-%20Computer%20Management/README.md) | [Related Lab: Explore Computer Management](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-05) | [Key Terms](../../Key%20Terms/Windows%20Server%20Fundamentals/README.md#4-system-administration-and-consoles)

---

## Basic

### 1. What is Computer Management (`compmgmt.msc`) and what are its three major divisions?

**Answer:**
Computer Management is a Microsoft Management Console (MMC) snap-in that consolidates essential administrative and troubleshooting tools into a single interface. Its three major divisions are:
1. **System Tools:** Task Scheduler, Event Viewer, Shared Folders, Local Users and Groups (on non-DCs), Performance, and Device Manager.
2. **Storage:** Disk Management (volume formatting, partitioning, and drive letter assignment).
3. **Services and Applications:** Background Windows services and WMI Control.

### 2. How do you launch Computer Management from the command line or Run dialog?

**Answer:**
Press `Win + R`, type `compmgmt.msc`, and press **Enter**. (Alternatively, run `compmgmt.msc` inside PowerShell or Command Prompt).

---

## Intermediate

### 3. What is the difference between the "Shares", "Sessions", and "Open Files" nodes under Shared Folders?

**Answer:**
- **Shares:** Lists all directories and resources currently exposed over SMB by the server (e.g., `SOC-Reports`, `C$`, `ADMIN$`, `IPC$`).
- **Sessions:** Shows real-time network connections from remote computers, displaying the connected username, client IP/hostname, number of open files, and connection duration.
- **Open Files:** Displays live file locks currently held by remote users across the network, showing which specific file is open and with what access permissions (Read/Write).

### 4. Why is the "Local Users and Groups" node unavailable or disabled in Computer Management on DC01?

**Answer:**
When a Windows Server is promoted to an Active Directory Domain Controller, the local Security Account Manager (SAM) database is disabled. The server no longer maintains local users or local groups. All user and group management is transferred to Active Directory Domain Services, managed through **Active Directory Users and Computers (`dsa.msc`)** or the Active Directory Administrative Center.

---

## Scenario-Based

### 5. A SOC analyst investigates an endpoint suspected of data exfiltration over the network. How can Computer Management be used during live triage?

**Answer:**
1. Open **Computer Management -> System Tools -> Shared Folders -> Sessions** to identify unauthorized remote client IP addresses connected over SMB.
2. Inspect **Open Files** to see exactly which documents or sensitive directories are actively being read or copied.
3. Check **Event Viewer -> Windows Logs -> Security** for Event IDs **5140** (Network share accessed) and **5145** (Detailed share access checks) to reconstruct what files were transferred.

### 6. In Disk Management, what is the purpose of the 100MB - 500MB "System Reserved" partition, and should an administrator assign it a drive letter?

**Answer:**
The System Reserved partition holds the Boot Configuration Data (BCD) store, the boot manager (`bootmgr`), and files required for BitLocker Drive Encryption. Administrators should **never** assign it a drive letter or modify its contents, as exposing it risks corruption or accidental deletion, which will render the Windows Server unbootable.

---

## Navigation

- [Previous: 03 - Roles vs Features](03%20-%20Roles%20vs%20Features.md)
- [Back to Windows Server Interview Hub](README.md)
- [Next: 05 - Windows Services](05%20-%20Windows%20Services.md)
