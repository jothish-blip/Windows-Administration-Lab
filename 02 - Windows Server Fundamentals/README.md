# Windows Server Fundamentals

## Overview

Windows Server is the backbone of enterprise IT environments, handling centralized identity management, name resolution, network services, access control, and file sharing. As part of my preparation for a Security Operations Center (SOC) Analyst role, I built and administered a live Windows Server 2022 domain controller (`DC01`) in an isolated virtual lab environment.

This section documents my foundational study of Windows Server architecture and administration, combined with 14 hands-on practical labs. The goal was not just to learn how to click through administrative wizards, but to understand how underlying operating system mechanisms, user identities, security groups, file systems, and network shares function—and how they translate to real-world access control, auditing, and security investigations.

---

## What I Covered

Throughout this track, I studied and implemented eight core Windows Server administration concepts and completed fourteen practical lab exercises:

- **Windows Server Editions & Licensing:** Comparing Standard, Datacenter, and Essentials editions, understanding core-based licensing, CALs, and virtualization rights.
- **Server Manager:** Centralized management interface for inspecting server health, local server properties, notifications, events, and the Best Practices Analyzer (BPA).
- **Roles vs. Features:** Understanding the architectural distinction between major server responsibilities (AD DS, DNS, DHCP, IIS) and supporting software capabilities (.NET, BitLocker).
- **Computer Management:** Unified administration using System Tools (Task Scheduler, Event Viewer, Shared Folders, Device Manager), Storage (Disk Management), and Services.
- **Windows Services:** Differentiating between real-time service status (Running vs. Stopped) and configuration startup types (Automatic, Delayed, Manual, Disabled), analyzing dependencies, and understanding service-based persistence mechanisms relevant to SOC work.
- **Identities and Access Control:** Managing local and domain identities, understanding the differences between local SAM and Active Directory Users and Computers (ADUC), implementing the Principle of Least Privilege (PoLP), and organizing users into security groups.
- **NTFS Permissions:** Configuring standard permissions (Read, Write, List, Read & Execute, Modify, Full Control), evaluating Access Control Lists (ACLs) and Access Control Entries (ACEs), managing inheritance, and avoiding problematic Deny rules.
- **Network File Sharing & Effective Access:** Creating and managing shared folders, comparing local access against network access, analyzing the overlap between Share permissions and NTFS permissions (most restrictive rule wins), configuring hidden administrative shares, and inspecting live sessions and open files.

---

## Learning Architecture

To support systematic study, terminology revision, and technical interview preparation, each module in this track connects through a structured learning workflow:

```text
Study Concept ──> Concept Summary ──> Practical Lab ──> Key Terms Review ──> Interview Questions
```

---

## Learning Path

The following table outlines the structured sequence of conceptual modules, practical labs, terminology, and interview preparation covered in this track:

| # | Concept Module | Practical Labs | Key Terms | Interview Preparation |
|:---:|:---|:---|:---|:---|
| 01 | [Server Editions](01%20-%20Windows%20Server%20Editions/README.md) | [Lab 01 (winver)](Lab-Exercise.md#practical-lab-01), [Lab 02 (systeminfo)](Lab-Exercise.md#practical-lab-02) | [Editions Terms](../Key%20Terms/Windows%20Server%20Fundamentals/README.md#1-server-editions-and-licensing) | [Editions Q&A](../Interview%20Questions/Windows%20Server%20Fundamentals/01%20-%20Windows%20Server%20Editions.md) |
| 02 | [Server Manager](02%20-%20Server%20Manager/README.md) | [Lab 03 (Server Manager)](Lab-Exercise.md#practical-lab-03) | [Management Terms](../Key%20Terms/Windows%20Server%20Fundamentals/README.md#2-server-management-and-dashboards) | [Server Manager Q&A](../Interview%20Questions/Windows%20Server%20Fundamentals/02%20-%20Server%20Manager.md) |
| 03 | [Roles vs Features](03%20-%20Roles%20vs%20Features/README.md) | [Lab 04 (Roles Wizard)](Lab-Exercise.md#practical-lab-04) | [Roles & Features Terms](../Key%20Terms/Windows%20Server%20Fundamentals/README.md#3-roles-and-features) | [Roles vs Features Q&A](../Interview%20Questions/Windows%20Server%20Fundamentals/03%20-%20Roles%20vs%20Features.md) |
| 04 | [Computer Management](04%20-%20Computer%20Management/README.md) | [Lab 05 (compmgmt.msc)](Lab-Exercise.md#practical-lab-05) | [Console Terms](../Key%20Terms/Windows%20Server%20Fundamentals/README.md#4-system-administration-and-consoles) | [Computer Mgmt Q&A](../Interview%20Questions/Windows%20Server%20Fundamentals/04%20-%20Computer%20Management.md) |
| 05 | [Windows Services](05%20-%20Windows%20Services/README.md) | [Lab 06 (services.msc)](Lab-Exercise.md#practical-lab-06) | [Services Terms](../Key%20Terms/Windows%20Server%20Fundamentals/README.md#5-windows-services-architecture) | [Services Q&A](../Interview%20Questions/Windows%20Server%20Fundamentals/05%20-%20Windows%20Services.md) |
| 06 | [Local Users & Groups](06%20-%20Local%20Users%20and%20Groups/README.md) | [Lab 07 (Users)](Lab-Exercise.md#practical-lab-07), [Lab 08 (Groups)](Lab-Exercise.md#practical-lab-08) | [Identity Terms](../Key%20Terms/Windows%20Server%20Fundamentals/README.md#6-identity-users-and-groups) | [Users & Groups Q&A](../Interview%20Questions/Windows%20Server%20Fundamentals/06%20-%20Local%20Users%20and%20Groups.md) |
| 07 | [NTFS Permissions](07%20-%20NTFS%20Permissions/README.md) | [Lab 09 (ACLs)](Lab-Exercise.md#practical-lab-09), [Lab 10 (Scenarios)](Lab-Exercise.md#practical-lab-10) | [NTFS Terms](../Key%20Terms/Windows%20Server%20Fundamentals/README.md#7-ntfs-file-system-security) | [NTFS Permissions Q&A](../Interview%20Questions/Windows%20Server%20Fundamentals/07%20-%20NTFS%20Permissions.md) |
| 08 | [Shared Folders](08%20-%20Shared%20Folders/README.md) | [Labs 11 - 14 (Shares & Overlap)](Lab-Exercise.md#practical-lab-11) | [SMB & Share Terms](../Key%20Terms/Windows%20Server%20Fundamentals/README.md#8-network-file-sharing-and-smb) | [Shared Folders Q&A](../Interview%20Questions/Windows%20Server%20Fundamentals/08%20-%20Shared%20Folders.md) |

---

## Completed Practical Labs

All fourteen hands-on practical exercises are documented in detail in [`Lab-Exercise.md`](Lab-Exercise.md), including exact commands, configurations, verification steps, and screenshot evidence from `DC01` and `CLIENT01`:

| Lab # | Lab Title | What I Practiced | Key Evidence / Output | Link |
|:-----:|-----------|------------------|-----------------------|:----:|
| 01 | Verify Windows Server Edition | Used `winver` on `DC01` to verify the installed OS build and licensing edition. | Microsoft Windows Server 2022 Standard Evaluation | [View Lab](Lab-Exercise.md#practical-lab-01--to-know-the-windows-server-edition) |
| 02 | Gather Detailed System Information | Used `systeminfo` in Command Prompt to inspect OS version, system architecture, total physical RAM, and domain configuration. | Build 20348, x64, 4096 MB RAM, Domain `soclab.local` | [View Lab](Lab-Exercise.md#practical-lab-02--to-know-detailed-information-about-the-system) |
| 03 | Explore Server Manager | Explored Server Manager Dashboard, Local Server configuration, Manage menu, administrative Tools, and system Notifications. | Hostname `WIN-DEF8VDFQ099`, IP `192.168.10.10`, AD DS/DNS status | [View Lab](Lab-Exercise.md#practical-lab-03--explore-the-server-manager) |
| 04 | Explore Roles and Features | Navigated the Add Roles and Features Wizard, compared role-based vs. RDS installation types, server pool selection, and browsed available roles/features. | Wizard navigation, AD DS, DNS, DHCP, IIS, .NET, BitLocker | [View Lab](Lab-Exercise.md#practical-lab-04--explore-roles-and-features) |
| 05 | Explore Computer Management | Used `compmgmt.msc` to navigate System Tools, Event Viewer log categories, Shared Folders views, Device Manager virtualized hardware, and Disk Management volumes. | Disk 0 (80 GB), C: partition (79.9 GB), Event Viewer Windows Logs | [View Lab](Lab-Exercise.md#practical-lab-05--explore-computer-management) |
| 06 | Explore and Manage Windows Services | Inspected registered local services, compared Status vs. Startup Type, analyzed Print Spooler properties, tested controlled Stop/Start, and verified service dependencies (HTTP, RPC). | Print Spooler (`Spooler`), Automatic startup, running state, dependencies | [View Lab](Lab-Exercise.md#practical-lab-06--explore-and-manage-windows-services) |
| 07 | Manage Domain Users in Active Directory | Opened ADUC (`dsa.msc`), inspected domain structure `soclab.local`, explored custom `SOC` OU, created `Test Analyst` account, tested account disable/enable lifecycle, and performed a password reset. | `Test Analyst` account in `SOC` OU, down-arrow disabled state, password reset | [View Lab](Lab-Exercise.md#practical-lab-07--manage-domain-users-in-active-directory) |
| 08 | Manage Security Groups | Explored `SOC-Analysts` and `SOC-Managers` groups, created new `SOC-Admins` global security group in `SOC` OU, added `Test Analyst`, and mapped the group-based access model. | `SOC-Admins` created, membership verified, role-based access model | [View Lab](Lab-Exercise.md#practical-lab-08--manage-security-groups) |
| 09 | Configure NTFS Permissions | Created directory structure `C:\SOC-Lab\Reports` and test files, opened Advanced Security Settings, analyzed inheritance, and assigned tiered permissions to `SOC-Analysts`, `SOC-Managers`, and `SOC-Admins`. | ACL configured: Analysts (Read & Execute), Managers (Modify), Admins (Full Control) | [View Lab](Lab-Exercise.md#practical-lab-09--configure-ntfs-permissions) |
| 10 | NTFS Permission Scenarios | Tested effective local NTFS permissions with different accounts, verified Access Denied on write/delete for analyst, verified modify/delete for manager, created a subfolder `Daily` to observe inheritance, and applied an explicit permission to compare against inherited rules. | Permission errors recorded, Access Matrix verified, explicit vs. inherited rules confirmed | [View Lab](Lab-Exercise.md#practical-lab-10--ntfs-permission-scenarios) |
| 11 | Create and Access a Network Shared Folder | Created `C:\SOC-Reports`, shared over network via Advanced Sharing, set Share permissions (`Everyone: Read`), configured NTFS permissions, accessed share over UNC from `CLIENT01`, tested analyst and manager permissions, and inspected active shares and sessions in Computer Management. | `\\WIN-DEF8VDFQ099\SOC-Reports` accessed from `CLIENT01`, session tracked, Effective Permission trap identified | [View Lab](Lab-Exercise.md#practical-lab-11--create-and-access-a-network-shared-folder) |
| 12 | Share + NTFS Permission Scenarios | Deliberately tested combinations of Share and NTFS permissions over the network from `CLIENT01` (Share Read + NTFS Modify, Share Change + NTFS Read, Share Full Control + NTFS Modify), and demonstrated local vs. network access bypass. | Most restrictive permission rule verified across all 4 scenarios | [View Lab](Lab-Exercise.md#practical-lab-12--share--ntfs-permission-scenarios) |
| 13 | Hidden Shares & Administrative Shares | Created hidden share `SOC-Secret$`, confirmed it does not appear in normal network browsing from `CLIENT01`, verified error on accessing without `$`, confirmed successful access via full UNC path `\\DC01\SOC-Secret$`, and inspected default administrative shares (`C$`, `ADMIN$`, `IPC$`) via `net share`. | Hidden ≠ Protected principle proven; administrative shares cataloged | [View Lab](Lab-Exercise.md#practical-lab-13--hidden-shares--administrative-shares) |
| 14 | Complete Access-Control Scenario | Built end-to-end multi-tiered access lab (`C:\SOC-AccessLab`) with subfolders (`Analyst`, `Manager`, `Admin`), applied standard enterprise practice (Share: `Everyone: Full Control`, NTFS: granular tiering), and verified effective access from `CLIENT01` across all three tiers. | End-to-end access matrix validated: Analyst Read-only, Manager Modify, Admin Full Control | [View Lab](Lab-Exercise.md#practical-lab-14--complete-access-control-scenario) |

---

## Concepts to Labs Mapping

To connect theoretical understanding with practical implementation, each conceptual module directly corresponds to one or more hands-on lab exercises:

| Core Concept | Conceptual Module | Practical Implementation Lab |
|--------------|-------------------|------------------------------|
| Windows Server Editions & System Build | [01 - Windows Server Editions](01%20-%20Windows%20Server%20Editions/README.md) | [Lab 01: Verify Edition](Lab-Exercise.md#practical-lab-01--to-know-the-windows-server-edition)<br>[Lab 02: System Information](Lab-Exercise.md#practical-lab-02--to-know-detailed-information-about-the-system) |
| Server Manager Console & Administration | [02 - Server Manager](02%20-%20Server%20Manager/README.md) | [Lab 03: Explore Server Manager](Lab-Exercise.md#practical-lab-03--explore-the-server-manager) |
| Server Roles vs. Supporting Features | [03 - Roles vs Features](03%20-%20Roles%20vs%20Features/README.md) | [Lab 04: Explore Roles and Features](Lab-Exercise.md#practical-lab-04--explore-roles-and-features) |
| Unified System Management & Event Logs | [04 - Computer Management](04%20-%20Computer%20Management/README.md) | [Lab 05: Explore Computer Management](Lab-Exercise.md#practical-lab-05--explore-computer-management) |
| Windows Services, Startup Types & Dependencies | [05 - Windows Services](05%20-%20Windows%20Services/README.md) | [Lab 06: Manage Windows Services](Lab-Exercise.md#practical-lab-06--explore-and-manage-windows-services) |
| Active Directory Identities & User Management | [06 - Local Users and Groups](06%20-%20Local%20Users%20and%20Groups/README.md) | [Lab 07: Manage Domain Users in AD](Lab-Exercise.md#practical-lab-07--manage-domain-users-in-active-directory) |
| Security Groups & Role-Based Access Control | [06 - Local Users and Groups](06%20-%20Local%20Users%20and%20Groups/README.md) | [Lab 08: Manage Security Groups](Lab-Exercise.md#practical-lab-08--manage-security-groups) |
| NTFS Permissions, ACLs & Inheritance | [07 - NTFS Permissions](07%20-%20NTFS%20Permissions/README.md) | [Lab 09: Configure NTFS Permissions](Lab-Exercise.md#practical-lab-09--configure-ntfs-permissions)<br>[Lab 10: NTFS Permission Scenarios](Lab-Exercise.md#practical-lab-10--ntfs-permission-scenarios) |
| Network File Sharing, Permissions & UNC Paths | [08 - Shared Folders](08%20-%20Shared%20Folders/README.md) | [Lab 11: Create & Access Shared Folder](Lab-Exercise.md#practical-lab-11--create-and-access-a-network-shared-folder)<br>[Lab 12: Share + NTFS Scenarios](Lab-Exercise.md#practical-lab-12--share--ntfs-permission-scenarios) |
| Hidden Shares, Administrative Shares & Auditing | [08 - Shared Folders](08%20-%20Shared%20Folders/README.md) | [Lab 13: Hidden & Admin Shares](Lab-Exercise.md#practical-lab-13--hidden-shares--administrative-shares)<br>[Lab 14: Complete Access Control Scenario](Lab-Exercise.md#practical-lab-14--complete-access-control-scenario) |

---

## Learning Progress

- [x] Foundation: Virtualization & Hypervisor Setup (`01 - Virtualization`)
- [x] Lab Infrastructure Provisioning (`DC01` and `CLIENT01` on internal network `SOC-LAB`)
- [x] Module 01: Windows Server Editions & Licensing
- [x] Module 02: Server Manager Interface & Operations
- [x] Module 03: Roles vs. Features Architectural Distinction
- [x] Module 04: Computer Management & Unified Administration
- [x] Module 05: Windows Services Management & Dependency Analysis
- [x] Module 06: Active Directory Identities, OUs & Security Groups
- [x] Module 07: NTFS File System Security & ACL Configuration
- [x] Module 08: Network Shared Folders, Effective Permissions & Access Scenarios
- [x] Practical Labs: All 14 hands-on labs executed, verified, and documented with screenshots

---

## Relevance to SOC Analyst Work

Understanding Windows Server fundamentals is not just an administrative skill; it directly underpins defensive cybersecurity operations:

- **Incident Investigation:** Recognizing standard vs. anomalous system services, processes, and service startup configurations is essential for identifying persistence mechanisms.
- **Log Analysis:** Familiarity with Event Viewer categories (`Security`, `System`, `Application`) is required to trace authentication events (Event ID 4624/4625), privilege escalation, and object access attempts.
- **Access Control Auditing:** Knowing how NTFS permissions and network shares interact allows analysts to identify misconfigurations that lead to unauthorized lateral movement, data exfiltration, or privilege creep.
- **Identity Architecture:** Understanding how Active Directory organizes objects (OUs, Groups, User Accounts) helps analysts evaluate attack paths and enforce the Principle of Least Privilege.

---

## Repository Navigation

- **Main Repository Hub:** [Windows Administration Lab](../README.md)
- **Previous Track:** [Virtualization Fundamentals](../01%20-%20Virtualization/README.md)
- **Windows Server Key Terms:** [Key Terms Directory](../Key%20Terms/Windows%20Server%20Fundamentals/README.md)
- **Windows Server Interview Questions:** [Interview Questions Hub](../Interview%20Questions/Windows%20Server%20Fundamentals/README.md)
- **Full Lab Exercises:** [14 Practical Labs](Lab-Exercise.md)
