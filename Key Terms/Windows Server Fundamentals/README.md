# Windows Server Fundamentals - Key Terms

[Key Terms Directory](../README.md) | [Windows Server Track Hub](../../02%20-%20Windows%20Server%20Fundamentals/README.md) | [Repository Overview](../../README.md) | [Windows Server Interview Questions](../../Interview%20Questions/Windows%20Server%20Fundamentals/README.md)

---

## Overview

This reference glossary defines the core terminology studied across the eight conceptual modules and fourteen practical labs of the **Windows Server Fundamentals** track. Each entry includes its authoritative technical definition and practical relevance to SOC security operations.

---

## Table of Contents

1. [Server Editions and Licensing](#1-server-editions-and-licensing)
2. [Server Management and Dashboards](#2-server-management-and-dashboards)
3. [Roles and Features](#3-roles-and-features)
4. [System Administration and Consoles](#4-system-administration-and-consoles)
5. [Windows Services Architecture](#5-windows-services-architecture)
6. [Identity, Users, and Groups](#6-identity-users-and-groups)
7. [NTFS File System Security](#7-ntfs-file-system-security)
8. [Network File Sharing and SMB](#8-network-file-sharing-and-smb)

---

## 1. Server Editions and Licensing

Related Concept: [01 - Windows Server Editions](../../02%20-%20Windows%20Server%20Fundamentals/01%20-%20Windows%20Server%20Editions/README.md) | Related Labs: [Lab 01 & Lab 02](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-01)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Standard Edition** | The mainstream edition of Windows Server designed for physical or lightly virtualized environments. Includes licensing rights for 2 virtual operating system environments (OSEs) or Hyper-V containers. | The baseline operating system deployed on `DC01` for enterprise domain administration in this lab. |
| **Datacenter Edition** | The top-tier edition of Windows Server designed for highly virtualized enterprise data centers and hybrid clouds. Provides rights to run unlimited virtual machines on licensed physical cores, along with Shielded VMs and Storage Spaces Direct. | Used in high-density corporate server clusters hosting dozens of departmental VMs. |
| **Evaluation Edition** | A time-limited (180-day) full-featured build of Windows Server provided by Microsoft for testing, lab learning, and evaluation without upfront licensing costs. | Used for our lab `DC01`. Can be converted to full licensed retail/volume editions using DISM if desired. |
| **Core-Based Licensing** | Microsoft's enterprise licensing model where servers are licensed according to physical processor cores (minimum of 8 cores per processor, 16 cores per server) rather than per socket. | Auditors and IT asset managers must ensure licensed core counts match hypervisor allocations. |
| **Client Access License (CAL)** | A commercial license that grants a user or device the legal right to access services provided by a Windows Server (e.g., AD authentication, file storage). | Understanding CAL types (User CAL vs Device CAL) is standard in enterprise IT operations. |

---

## 2. Server Management and Dashboards

Related Concept: [02 - Server Manager](../../02%20-%20Windows%20Server%20Fundamentals/02%20-%20Server%20Manager/README.md) | Related Lab: [Lab 03](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-03)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Server Manager** | The centralized management console in Windows Server providing an overview of server status, installed roles, operational events, and quick launches for administrative consoles. | The primary GUI dashboard used by administrators on `DC01` to monitor local server properties, NIC settings, and role health. |
| **Local Server View** | The properties panel in Server Manager detailing hostname, domain membership, firewall profile, remote desktop status, IP configuration, and installed RAM. | One-stop verification panel for establishing system baselines during administrative onboarding and security auditing. |
| **Best Practices Analyzer (BPA)** | A built-in diagnostic tool that scans installed server roles against Microsoft configuration best practices and generates compliance reports. | Helps identify insecure default configurations or non-compliant operational settings before systems go into production. |

---

## 3. Roles and Features

Related Concept: [03 - Roles vs Features](../../02%20-%20Windows%20Server%20Fundamentals/03%20-%20Roles%20vs%20Features/README.md) | Related Lab: [Lab 04](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-04)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Server Role** | A primary workload or major business function that a server performs on the network (e.g., Active Directory Domain Services, DNS Server, DHCP Server, Web Server IIS). | A server is fundamentally defined by its roles. Adding a role alters network behavior and increases attack surface. |
| **Feature** | An auxiliary software component or capability that supports the operating system or enhances specific server roles (e.g., .NET Framework, BitLocker, Failover Clustering, RSAT). | Features provide modular utilities without turning the server into a dedicated role-based appliance. |
| **Role Service** | A modular sub-component of a broader server role that provides specific functions (e.g., Certification Authority is a role service of Active Directory Certificate Services). | Allows administrators to deploy only the specific capabilities required, minimizing overhead and risk. |
| **RSAT (Remote Server Administration Tools)** | A collection of GUI snap-ins and PowerShell modules allowing administrators to remotely manage server roles from a client workstation. | Prevents administrators from routinely logging directly into Domain Controller consoles over RDP. |

---

## 4. System Administration and Consoles

Related Concept: [04 - Computer Management](../../02%20-%20Windows%20Server%20Fundamentals/04%20-%20Computer%20Management/README.md) | Related Lab: [Lab 05](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-05)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Computer Management (`compmgmt.msc`)** | A Microsoft Management Console (MMC) snap-in consolidating System Tools, Storage, and Services into a unified administration window. | Rapid host-level triage console used during initial host audits and live forensics. |
| **Task Scheduler** | A Windows service and management interface used to automate scripts, programs, and maintenance routines based on time or system events. | Frequently abused by threat actors for persistence (MITRE ATT&CK T1053.005); defenders must audit scheduled task creation. |
| **Event Viewer (`eventvwr.msc`)** | The built-in log viewing console that displays Windows event logs (Application, Security, Setup, System, and Forwarded Events). | The primary host log tool used by SOC analysts to trace logon attempts (Event ID 4624/4625), service installations (7045), and account modifications. |
| **Disk Management** | The system utility used to partition, format, shrink, extend, and manage physical and virtual hard disks and filesystem volumes. | Used to inspect partition geometry and verify storage allocations across C: and data volumes. |

---

## 5. Windows Services Architecture

Related Concept: [05 - Windows Services](../../02%20-%20Windows%20Server%20Fundamentals/05%20-%20Windows%20Services/README.md) | Related Lab: [Lab 06](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-06)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Windows Service** | A long-running background executable process managed by the Service Control Manager (SCM) that executes without requiring an interactive user desktop session. | Core server functions (AD DS, DNS, Windows Update, Defender) run as background services. |
| **Service Status** | The real-time operational state of a service (Running, Stopped, Paused, or Pending). | Checking status answers: "Is this daemon currently active in memory right now?" |
| **Startup Type** | The configuration rule governing how Windows initializes a service at system boot (Automatic, Automatic Delayed, Manual, Disabled). | Checking startup type answers: "What will Windows do with this service during the next system reboot?" |
| **Service Dependency** | An architectural requirement where a service cannot start or operate correctly unless prerequisite services are running first. | Print Spooler depends on HTTP and RPC. Stopping a root dependency cascades failures to all child services. |
| **`Local System` Account (`NT AUTHORITY\SYSTEM`)** | A built-in Windows security principal with complete, unrestricted administrative privileges on the local machine. | Services running under `Local System` operate with highest privilege; compromising such a service yields full machine compromise. |

---

## 6. Identity, Users, and Groups

Related Concept: [06 - Local Users and Groups](../../02%20-%20Windows%20Server%20Fundamentals/06%20-%20Local%20Users%20and%20Groups/README.md) | Related Labs: [Lab 07 & Lab 08](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-07)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Security Identifier (SID)** | A unique string of characters assigned by Windows to every security principal (user, group, computer). SIDs remain immutable across renames. | Windows enforces permissions by checking SIDs, not usernames. Deleting an account destroys its SID forever. |
| **Active Directory Domain Services (AD DS)** | Microsoft's distributed directory service storing identity records and authenticating users and computers across a domain. | The central identity backbone of enterprise corporate networks; managing `soclab.local`. |
| **Organizational Unit (OU)** | A container object inside an Active Directory domain used to organize users, groups, and computers for delegation and Group Policy application. | In this lab, the `SOC` OU organizes analysts, managers, and administrative groups into a structured hierarchy. |
| **Security Group** | A collection of user accounts or other groups used by Windows to assign permissions to resources and grant rights across the domain. | Permissions should always be assigned to Security Groups (e.g., `SOC-Analysts`, `SOC-Managers`), never to individuals directly. |
| **SAM Database** | The Security Account Manager database storing local user and group accounts on standalone workstations or member servers. | On Domain Controllers, the local SAM is disabled and replaced entirely by the Active Directory database (`NTDS.dit`). |
| **Authentication vs. Authorization** | Authentication proves *who you are* (verifying credentials); Authorization determines *what you are allowed to do* (evaluating permissions). | Authentication occurs against the Domain Controller; Authorization is evaluated by the file server hosting the resource. |
| **Principle of Least Privilege (PoLP)** | The security practice of granting users only the minimum permissions necessary to perform their authorized job responsibilities. | Standard analysts receive read-only permissions; write and administrative capabilities are strictly reserved for higher tiers. |

---

## 7. NTFS File System Security

Related Concept: [07 - NTFS Permissions](../../02%20-%20Windows%20Server%20Fundamentals/07%20-%20NTFS%20Permissions/README.md) | Related Labs: [Lab 09 & Lab 10](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-09)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **NTFS (New Technology File System)** | The default proprietary journaling file system for Windows providing security permissions, encryption (EFS), compression, and auditing. | Enforces file-level security regardless of whether access occurs locally at the server desktop or remotely over the network. |
| **Access Control List (ACL)** | A list of permissions attached to an object (file, folder, Active Directory object) specifying which principals have access. | Governed by the Windows Security Reference Monitor (SRM) inside the kernel. |
| **DACL vs SACL** | Discretionary ACL (DACL) defines who can access an object; System ACL (SACL) controls what access events generate audit logs in the Security event log. | SOC auditing relies on SACLs to generate Event ID 4663 (Attempt made to access an object). |
| **Access Control Entry (ACE)** | A single rule inside an ACL granting or denying a specific permission (e.g., Allow `SOC-Managers` Modify). | An ACL consists of an ordered array of individual ACE rules evaluated by Windows from top to bottom. |
| **Permission Inheritance** | The automatic propagation of permissions from a parent directory down to child subdirectories and files. | Subfolder `Daily` inherits rules from `Reports` unless inheritance is explicitly disabled and converted. |
| **Explicit Permission** | A permission rule applied directly to a specific folder or file, taking precedence over inherited rules. | Indicated by `<not inherited>` in Advanced Security Settings. |
| **Deny Precedence Rule** | The Windows evaluation rule where an explicit Deny permission overrides any conflicting Allow permissions granted through other group memberships. | Explicit Deny should be avoided in enterprise administration as it causes unpredictable permission collisions. |

---

## 8. Network File Sharing and SMB

Related Concept: [08 - Shared Folders](../../02%20-%20Windows%20Server%20Fundamentals/08%20-%20Shared%20Folders/README.md) | Related Labs: [Labs 11, 12, 13 & 14](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-11)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **SMB (Server Message Block)** | The network file sharing protocol used by Windows systems to share files, printers, and serial ports over port 445 (TCP). | The underlying protocol carrying file access requests from `CLIENT01` to `DC01`. |
| **UNC Path (Universal Naming Convention)** | The standardized syntax used in Windows networking to specify the location of a shared resource: `\\ServerName\ShareName`. | For example: `\\WIN-DEF8VDFQ099\SOC-Reports` or `\\192.168.10.10\SOC-AccessLab`. |
| **Share Permissions** | Basic network-level permissions (Read, Change, Full Control) that act as the outer gate for incoming SMB network connections. | Do not apply to users logging into the server locally; only evaluated when crossing the network. |
| **Effective Access (The Overlap)** | When connecting over the network, Windows evaluates both Share and NTFS permissions; the **most restrictive** permission wins. | `Share: Read` + `NTFS: Modify` = `Effective Access: Read` (The Effective Permission Trap documented in Lab 11/12). |
| **Hidden Share (`$`)** | A network share whose name ends with a dollar sign (`$`), instructing Windows to omit it from graphical network browse listings. | **Hidden does not mean secure.** Anyone who knows the full UNC path (`\\DC01\SOC-Secret$`) can connect if permissions allow. |
| **Administrative Shares** | Built-in default hidden shares created by Windows for remote administration (`C$`, `ADMIN$`, `IPC$`, `SYSVOL`, `NETLOGON`). | Attackers use administrative shares for lateral movement (e.g., PsExec targeting `ADMIN$`); must never be deleted on a DC. |

---

## Navigation

- [Back to Key Terms Directory](../README.md)
- [Previous: Virtualization Key Terms](../Virtualization%20Fundamentals/README.md)
- [Go to Windows Server Interview Questions](../../Interview%20Questions/Windows%20Server%20Fundamentals/README.md)
- [Back to Windows Server Track Hub](../../02%20-%20Windows%20Server%20Fundamentals/README.md)
