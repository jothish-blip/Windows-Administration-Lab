# NTFS Permissions - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../02%20-%20Windows%20Server%20Fundamentals/07%20-%20NTFS%20Permissions/README.md) | [Related Labs: Lab 09 & Lab 10](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-09) | [Key Terms](../../Key%20Terms/Windows%20Server%20Fundamentals/README.md#7-ntfs-file-system-security)

---

## Basic

### 1. What are NTFS Permissions in Windows?

**Answer:**
NTFS permissions are file-system-level access rules enforced by the Windows kernel (Security Reference Monitor) on volumes formatted with the New Technology File System (NTFS). They govern access to files and folders regardless of whether a user logs in locally at the console or connects remotely over the network.

### 2. What are the six standard NTFS permissions?

**Answer:**
1. **Full Control:** Read, write, modify, delete, change permissions (DACL), and take ownership.
2. **Modify:** Read, write, create, edit, and delete files and subfolders. Cannot alter permissions or ownership.
3. **Read & Execute:** View folder contents, read file data, and run executable programs and scripts.
4. **List Folder Contents:** View the names of files and subfolders within a directory.
5. **Read:** View file contents and inspect file attributes and permissions.
6. **Write:** Create new files and subfolders, write data, and modify file attributes.

---

## Intermediate

### 3. What is the difference between Inherited Permissions and Explicit Permissions?

**Answer:**
- **Inherited Permissions:** Access rules that automatically propagate downward from a parent directory to child subfolders and files (indicated by parent path in the "Inherited from" column).
- **Explicit Permissions:** Access rules configured directly on a specific folder or file (indicated by `None` or `<not inherited>`). Explicit permissions override conflicting inherited permissions.

### 4. What is the Windows permission evaluation precedence order for Allow and Deny?

**Answer:**
Windows evaluates permissions in strict four-tier hierarchy:
1. **Explicit Deny** (Highest precedence - beats all Allow entries)
2. **Explicit Allow**
3. **Inherited Deny**
4. **Inherited Allow** (Lowest precedence)
*If no Allow ACE matches the requested action, access is implicitly Denied.*

---

## Scenario-Based

### 5. Why do enterprise system administrators avoid using explicit "Deny" permissions?

**Answer:**
Because an **Explicit Deny** overrides all Allow permissions regardless of which group granted them. If User A is in `SOC-Analysts` (Allow Read) and `Incident-Responders` (Allow Modify), adding an explicit Deny Write to `SOC-Analysts` immediately strips User A's Modify rights inherited from `Incident-Responders`. Explicit Deny introduces hidden permission conflicts that are difficult to troubleshoot. Best practice is to design clean, role-based **Allow-only** models.

### 6. A SOC analyst investigates unauthorized permission modifications on a secure data folder. What Windows Security Event ID logs permission tampering?

**Answer:**
- **Event ID 4670:** "Permissions on an object were changed."
- The event log records the Subject (account that made the change), the Object Name (file/folder path), the Old SDDL (Security Descriptor Definition Language) permissions string, and the New SDDL string. Correlating this event reveals who modified the DACL to grant unauthorized access or weaken security boundaries.

---

## Navigation

- [Previous: 06 - Users and Groups](06%20-%20Local%20Users%20and%20Groups.md)
- [Back to Windows Server Interview Hub](README.md)
- [Next: 08 - Shared Folders](08%20-%20Shared%20Folders.md)
