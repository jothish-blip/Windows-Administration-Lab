# Shared Folders

[Windows Server Fundamentals Overview](../README.md) | [Previous: NTFS Permissions](../07%20-%20NTFS%20Permissions/README.md) | [Related Labs: Labs 11, 12, 13, 14](../Lab-Exercise.md#practical-lab-11--create-and-access-a-network-shared-folder)

---

## 1. What is a Shared Folder?

A **Shared Folder** is a directory that Windows makes available to other computers over a network. This enables centralized file storage, allowing multiple users to access the same files from different workstations instead of storing copies on every individual PC.

When a folder is shared, it is accessed using a **UNC (Universal Naming Convention)** path rather than a local drive letter.

* **Local Path (on the server):** `C:\CompanyData\SOC-Reports`
* **Network Path (UNC):** `\\DC01\SOC-Reports` (Format: `\\ServerName\ShareName`)

## 2. Share Permissions vs. NTFS Permissions

To understand network file access, you must understand the distinction between the two layers of security Windows uses.

### Share Permissions

Share permissions control what a user can do *only when accessing the resource through the network*.

* **Common permissions:** Read, Change, Full Control.
* *Think:* The "front door" for network access.

### NTFS Permissions

NTFS permissions apply to the actual file-system objects (files and folders) stored on the hard drive. They apply regardless of how the file is accessed.

* **Common permissions:** Read, Write, Modify, Read & Execute, Full Control.
* *Think:* The fundamental security rules of the file system.

## 3. Local Access vs. Network Access

The way a user accesses the folder determines which permissions apply. This is a critical troubleshooting concept for Windows Administrators.

* **Local Access:** If an administrator logs directly into DC01 and opens `C:\SOC-Reports`, they are accessing the file locally. **Only NTFS permissions apply.**
* **Network Access:** If a user logs into CLIENT01 and accesses `\\DC01\SOC-Reports`, they are coming over the network. **Both Share Permissions and NTFS Permissions apply.**

## 4. Effective Permissions (The Overlap)

When a user accesses a folder over the network, Windows evaluates both the Share permissions and the NTFS permissions.

**Rule:** The effective permission is generally the *more restrictive* result of the two.

**Example A: Share restricts NTFS**

* **Share Permission:** SOC-Analysts → `Read`
* **NTFS Permission:** SOC-Analysts → `Modify`
* **Effective Access:** `Read` *(The network share limits what the user can do, even though the file system would allow modifications).*

**Example B: NTFS restricts Share**

* **Share Permission:** SOC-Analysts → `Full Control`
* **NTFS Permission:** SOC-Analysts → `Read`
* **Effective Access:** `Read` *(The network share is wide open, but the underlying file system restricts the user).*

### The Access Model

```text
                 USER
                   │
          Network Share Access
                   │
          ┌────────┴────────┐
          │ Share Permission│
          └────────┬────────┘
                   │
          ┌────────┴────────┐
          │ NTFS Permission │
          └────────┬────────┘
                   │
              FILE/FOLDER

```

*Administrative Best Practice Pattern:* Because managing two complex layers of permissions is prone to error, many organizations simplify their design. They set the **Share Permission** very broadly (e.g., granting "Change" or "Full Control" to all authenticated users) and use the granular **NTFS Permissions** to strictly control actual access.

## 5. Hidden and Administrative Shares

Not all network shares are meant for standard users. Windows utilizes special shares for administrative operations.

### Hidden Shares (`$`)

If a share name ends with a dollar sign (e.g., `Secret$`), it is a hidden share.

* It will not appear when a user browses the network graphically.
* It can still be accessed if the user manually types the exact UNC path (e.g., `\\DC01\Secret$`).
* **Important:** Hidden does *not* mean secure. The `$` simply makes the share invisible to casual browsing; it does not replace the need for proper authentication and NTFS permissions.

### Administrative Shares

Windows creates default administrative shares to allow IT staff to manage the system remotely. Accessing these requires administrative credentials.

* **`C$`:** Provides remote administrative access to the entire root of the C: drive (e.g., `\\DC01\C$`).
* **`ADMIN$`:** Maps directly to the Windows system directory (usually `C:\Windows`), intended for remote administrative operations.
* **`IPC$`:** Inter-Process Communication. Used by Windows for underlying network communication mechanisms and remote administrative tasks rather than standard file sharing.

## 6. Inspecting Shares

To observe the shared folders currently configured on a Windows Server without making changes:

* **GUI Method:** Open `Computer Management → System Tools → Shared Folders → Shares`. This provides a visual list of share names, folder paths, and current client connections.

![Shared Folders](<../Screenshots/29 - Shared Folders.png>)

* **CLI Method:** Open Command Prompt and type `net share`. This outputs a simple list of all active shares (including hidden administrative shares) on the local machine.

![Shared Folder](<../Screenshots/30 - Shared Folders - CMD.png>)

## Summary

In this module, I studied network file sharing using SMB and UNC paths. I analyzed the dual-layer permission model where Windows evaluates both the network Share permission and underlying NTFS file-system permissions, strictly enforcing the most restrictive result. I learned why enterprise file servers configure Share permissions to Full Control while governing access through NTFS, demonstrated how hidden shares (`$`) hide from browsing without providing actual security, and explored default administrative shares (`C$`, `ADMIN$`, `IPC$`).

---

## Related Resources

- **Key Terms:** [Network File Sharing and SMB Key Terms](../../Key%20Terms/Windows%20Server%20Fundamentals/README.md#8-network-file-sharing-and-smb)
- **Interview Preparation:** [Shared Folders & SMB Interview Questions & Answers](../../Interview%20Questions/Windows%20Server%20Fundamentals/08%20-%20Shared%20Folders.md)
- **Practical Labs:** [Labs 11 to 14 (Network Shares & Permission Scenarios)](../Lab-Exercise.md#practical-lab-11)

---

## Navigation

- **Previous Module:** [07 - NTFS Permissions](../07%20-%20NTFS%20Permissions/README.md)
- **Track Index:** [Windows Server Fundamentals Overview](../README.md)
- **All Practical Labs:** [Lab Exercises Index](../Lab-Exercise.md)
- **Corresponding Labs:**
  - [Practical Lab 11 - Create and Access a Network Shared Folder](../Lab-Exercise.md#practical-lab-11)
  - [Practical Lab 12 - Share + NTFS Permission Scenarios](../Lab-Exercise.md#practical-lab-12)
  - [Practical Lab 13 - Hidden Shares & Administrative Shares](../Lab-Exercise.md#practical-lab-13)
  - [Practical Lab 14 - Complete Access-Control Scenario](../Lab-Exercise.md#practical-lab-14)