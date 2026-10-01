# Shared Folders & SMB - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../02%20-%20Windows%20Server%20Fundamentals/08%20-%20Shared%20Folders/README.md) | [Related Labs: Labs 11 - 14](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-11) | [Key Terms](../../Key%20Terms/Windows%20Server%20Fundamentals/README.md#8-network-file-sharing-and-smb)

---

## Basic

### 1. What is a Shared Folder in Windows Server, and what protocol is used to access it?

**Answer:**
A Shared Folder is a local folder made accessible to other computers across the network using the **Server Message Block (SMB)** protocol over TCP port 445. It is accessed using Universal Naming Convention (UNC) paths, such as `\\ServerName\ShareName`.

### 2. What are the three basic Share Permissions in Windows?

**Answer:**
1. **Read:** Allows users to view folder contents, open files, and copy files out of the share.
2. **Change:** Allows users to read, create, edit, and delete files and subfolders within the share.
3. **Full Control:** Includes all Change permissions, plus the right to modify Share permissions over the network.

---

## Intermediate

### 3. How does Windows evaluate effective access when both Share and NTFS permissions are configured?

**Answer:**
When a user connects over the network, Windows evaluates both the Share permission (the "front door") and the underlying NTFS permission (the "vault"). The **most restrictive** permission always wins:
- `Share: Read` + `NTFS: Modify` = **Effective Network Access: Read**
- `Share: Full Control` + `NTFS: Modify` = **Effective Network Access: Modify**
- `Share: Full Control` + `NTFS: Read` = **Effective Network Access: Read**

### 4. What is the recommended enterprise best practice for configuring Share vs NTFS permissions?

**Answer:**
The enterprise best practice is:
1. Configure **Share Permissions to Full Control** (or Change) for `Authenticated Users` or `Everyone`.
2. Manage all granular security and least-privilege access using **NTFS Permissions** on the Security tab.
*Rationale:* This prevents confusing bottlenecks (the Effective Permission Trap) and centralizes all access control, auditing, and inheritance within the NTFS file system.

---

## Scenario-Based

### 5. A manager has NTFS Modify permissions on `C:\SOC-Reports`. When accessing `\\DC01\SOC-Reports` from a client machine, they can read files but receive "Access is denied" when trying to save edits. When logging into DC01's desktop directly, they can save edits without issue. What is the cause?

**Answer:**
This is the classic **Effective Permission Trap** demonstrated in Lab 11:
- Over the network (SMB), both Share and NTFS permissions apply. The Share permission was left configured as **Read** for Everyone. Because the most restrictive rule wins, the Share permission caps the manager's effective network access to Read.
- When logging in locally at the DC01 desktop, network Share permissions are completely bypassed; only NTFS applies. Since NTFS grants Modify, local access succeeds.
- **Resolution:** Change the network Share permission to **Full Control** on DC01.

### 6. What is a Hidden Share, and why is appending a `$` character not considered a security measure?

**Answer:**
Appending a `$` to a share name (e.g., `SOC-Secret$`) simply instructs Windows to omit the share from graphical network browsing lists (`NetServerEnum`). 
- **Hidden does NOT mean secure.** It provides zero encryption, zero access restriction, and zero authentication bypass prevention.
- Anyone who types or guesses the exact UNC path (`\\DC01\SOC-Secret$`) can access the files if NTFS permissions allow it. Relying on hidden shares is security through obscurity.

### 7. What are Windows Administrative Shares (`C$`, `ADMIN$`, `IPC$`), and how do attackers abuse them during lateral movement?

**Answer:**
- **`C$`:** Direct remote administrative access to the root of the C: volume.
- **`ADMIN$`:** Maps directly to `C:\Windows` for remote system management.
- **`IPC$`:** Inter-Process Communication named pipes used for RPC authentication.
- **Attacker Abuse (MITRE ATT&CK T1021.002):** Attackers with compromised administrative credentials connect to `\\Target\ADMIN$` or `\\Target\C$`, drop a malicious service binary, and remotely invoke the Service Control Manager via DCE/RPC (`IPC$`) to execute code as `SYSTEM` (as done by PsExec and Impacket).
- **SOC Detection:** Monitor Windows Security Event IDs **5140** and **5145** for non-standard administrative share access.

---

## Navigation

- [Previous: 07 - NTFS Permissions](07%20-%20NTFS%20Permissions.md)
- [Back to Windows Server Interview Hub](README.md)
- [Next Track: Virtualization Interview Hub](../Virtualization%20Fundamentals/README.md)
