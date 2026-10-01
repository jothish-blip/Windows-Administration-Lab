# NTFS Permissions

## 1. What is NTFS?

**NTFS** stands for **New Technology File System**. It is the primary file system used by modern Windows operating systems.

One of its most important capabilities is security: it allows administrators to control exactly *who* can access specific files and folders, and *what* they are permitted to do with them.

Without NTFS permissions, any user who could log into a server could potentially read, modify, or delete any file on the hard drive.

## 2. The Fundamental Concept

NTFS permissions are built around answering two fundamental questions for any given resource:

* **Who?** (The User or Group)
* **What can they do?** (The specific Permission)

```text
     WHO              WHAT             RESOURCE
 User / Group  →   Permission  →   File / Folder

```

## 3. The Six Basic NTFS Permissions

Windows groups file and folder access into six primary standard permissions.

1. **Read:** Allows a user to view the contents of a file and its associated basic information/properties. *(They can open and look at the file).*
2. **Write:** Allows a user to create new files/folders or write data/changes to an existing file. *(They can add data, but Write alone does not mean they have full management over the file).*
3. **List Folder Contents:** A folder-specific permission that allows a user to see the names of files and subfolders contained within a folder.
4. **Read & Execute:** Combines the ability to read a file with the ability to run it if it is an executable program or script. For folders, it allows users to traverse through the directory structure.
5. **Modify:** A powerful permission that combines Read, Write, and Execute, while also granting the ability to **delete** files and folders.
6. **Full Control:** The highest standard permission. It includes everything in Modify, plus the administrative ability to change NTFS permissions for other users and take ownership of the file/folder.

### The Permission Hierarchy (Conceptual)

While Windows permissions are more nuanced than a simple ladder, the conceptual progression of power looks like this:

```text
                Full Control   (Can change permissions)
                     │
                  Modify       (Can delete files)
                     │
              Read & Execute   (Can run programs)
                /        \
             Read        Execute
               │
       List Folder Contents
               │
             Write

```

*Note: Because Full Control allows users to change permissions, it should be heavily restricted to IT administrators.*

## 4. Access Control Lists (ACLs)

Windows stores these security rules in an **Access Control List (ACL)** attached to every file and folder. The ACL contains multiple **Access Control Entries (ACEs)**. Each entry essentially says: *"Group X has Permission Y."*

## 5. Explicit vs. Inherited Permissions

Managing permissions on thousands of individual files would be impossible. NTFS solves this using inheritance.

* **Explicit Permissions:** Permissions assigned directly to a specific file or folder.
* *Think: "An administrator clicked on this exact folder and assigned this rule HERE."*


* **Inherited Permissions:** Permissions that flow downward from a parent folder to its child folders and files.
* *Think: "This rule came FROM THE PARENT."*



**The Inheritance Flow:**

```text
    C:\CompanyData      (Explicitly Assigned: SOC-Analysts → Read)
          │
          └── \Finance  (Inherits: SOC-Analysts → Read)
                │
                └── Budget.xlsx  (Inherits: SOC-Analysts → Read)

```

## 6. Allow vs. Deny

Every permission entry can be set to either **Allow** or **Deny**.

* **Allow:** The user/group is permitted to perform the action.
* **Deny:** The user/group is explicitly blocked from performing the action.

**Why Deny is Dangerous:**
If a user belongs to multiple groups (e.g., Alice is in `HR` and `SOC-Analysts`), and one group is explicitly *Allowed* access but another group is *Denied* access, you create complex access conflicts. Administrators generally prefer designing clean group-based "Allow" architectures rather than scattering "Deny" entries everywhere.

## 7. The Administrative Pattern: Groups + NTFS

This module directly connects to the concepts of Local and Domain Groups. The standard, efficient method for Windows Administration is:

1. Put Users into **Groups** based on their job roles.
2. Assign **NTFS Permissions** to the Group, never to the individual users.
3. Apply the permissions to the **Folders**.

```text
    Users  →   Groups  →   NTFS Permissions  →   Folders / Files

```

If a new analyst is hired, you simply add them to the `SOC-Analysts` group, and they instantly inherit all correct folder permissions across the entire server.

## 8. Least Privilege in File Security

The **Principle of Least Privilege** applies heavily to NTFS. Users should only receive the minimum permission required to do their job.

* If an analyst only needs to read a threat intelligence report: **Read**
* If an analyst needs to update or edit the report: **Modify**
* If an analyst needs to manage who else can see the folder: **Full Control** (Reserved for Admins)

## 9. Inspecting Permissions (Advanced Security Settings)

To view these permissions on a Windows Server:

1. Right-click a folder → `Properties` → `Security` tab.

![Security Permissions](<../Screenshots/27 - Security Permissions.png>)

2. Click the **Advanced** button to open the *Advanced Security Settings* window.

![Advanced Security Permissions](<../Screenshots/28 - Advanced Permissions.png>)

This advanced view breaks down the fundamental questions clearly:

* **Principal:** Who is this rule for?
* **Access:** What are they allowed to do?
* **Inherited from:** Where did this rule come from (Explicit or Parent)?
* **Applies to:** How deep does this rule go (This folder only, or subfolders and files)?