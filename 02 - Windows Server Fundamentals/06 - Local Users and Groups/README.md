# Local Users and Groups (and Domain Identities)

## 1. What is a User Account?

A **User Account** represents an individual identity that can authenticate to Windows and perform actions according to the permissions assigned to that account.

It provides a way for the operating system to distinguish exactly *who* is performing an action, which is the foundation of access control.

```text
    User (Jothish)
          ↓
    Authenticates
          ↓
    Windows determines allowed actions

```

If 100 employees shared a single account, the system would have no way to enforce individual access rules or audit who deleted a file. Individual accounts allow Windows to restrict "Alice" to HR files, "Bob" to Finance files, and "John" to IT administration.

## 2. Built-in User Accounts

Windows systems include default accounts with specific intended purposes:

* **Administrator:** A highly privileged account associated with system-wide administrative control (installing software, managing security, altering configurations).
* **Guest:** Historically designed to provide very limited, temporary access to a machine without granting normal privileges. In modern secure environments, the Guest account is generally kept disabled.

## 3. What is a Group?

A **Group** is a collection of user accounts used to manage access and permissions efficiently.

Groups allow administrators to manage permissions based on job function or access requirements, rather than micromanaging every individual user.

**Without Groups (Inefficient):**

```text
    Folder
     ├── Alice → Assign permission
     ├── Bob → Assign permission
     └── Charlie → Assign permission

```

**With Groups (Efficient):**

```text
    SOC Analysts Group (Contains Alice, Bob, Charlie)
          ↓
    Folder → Assign permission to Group

```

Groups are not strictly for "people with the same job." They are a mechanism for managing access. You might have separate groups for `Finance-Read` and `Finance-Write` to control exactly how different employees interact with the same data.

## 4. Built-in Groups

Windows provides several default groups with predefined operational capabilities:

* **Administrators:** Members have powerful, system-wide administrative privileges.
* **Users:** Represents ordinary users with standard permissions for normal Windows usage. Membership does not guarantee unrestricted access.
* **Backup Operators:** Provides specific rights allowing members to back up and restore files, regardless of standard file permissions, without granting them full administrative control.
* **Remote Desktop Users:** Associated with allowing members to access the computer via Remote Desktop (RDP), provided the system is configured to accept remote connections.

## 5. Authentication vs. Authorization

These two concepts are the core of cybersecurity access control and must be kept distinct.

* **Authentication ("Who are you?"):** The process of verifying identity.
* *Example:* Entering a Username + Password.


* **Authorization ("What are you allowed to do?"):** The process of verifying permissions after identity is confirmed.
* *Example:* Windows checking if authenticated-user "Alice" is in the "Finance" group before letting her open a folder.



## 6. Local Users vs. Domain Users (The Domain Controller Twist)

In previous modules, `Local Users and Groups` was visible in Computer Management. On DC01, it is missing. This is due to the difference between local and domain architectures.

* **Local User:** Exists only on a specific, standalone, or member computer.
* *Managed via:* Local Users and Groups (`lusrmgr.msc`)


* **Domain User:** Exists centrally in Active Directory and can authenticate to any domain-joined resource.
* *Managed via:* Active Directory Users and Computers (`dsa.msc`)



Because DC01 is a **Domain Controller**, its primary job is managing the directory for the entire domain. It does not use the standard local Security Account Manager (SAM) database in the same way a normal workstation does. Therefore, the local management console is removed to prevent conflicts and enforce central management.

## 7. Principle of Least Privilege (PoLP)

The **Principle of Least Privilege** dictates that a user, account, process, or system should only be given the absolute minimum permissions necessary to perform its required task.

* If an employee only needs to read a document, they receive **Read** access, not Full Control.
* If an employee needs to edit, they receive **Read + Write**.

**Why it matters for SOC Analysts:**
If malware compromises an ordinary user account adhering to Least Privilege, the blast radius is limited to what that user can touch. If malware compromises an account where everyone is given Administrator privileges out of convenience, the attacker immediately gains total control over the system.

## 8. Exploring Active Directory Users and Computers (ADUC)

To manage identities on a Domain Controller, administrators use ADUC instead of Computer Management.

**Access Path:**
`Server Manager → Tools → Active Directory Users and Computers` (or `Win + R → dsa.msc`)

![AD](<../Screenshots/26 - AD.png>)

Inside ADUC, administrators can view Organizational Units (OUs), create Domain Users (e.g., SOC Analyst 1), create Domain Groups (e.g., Analysts), and nest users inside those groups to prepare for efficient permission assignments.