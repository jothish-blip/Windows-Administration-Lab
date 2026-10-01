# Practical Lab Exercises - Windows Administration Lab

[Windows Server Fundamentals Hub](README.md) | [Virtualization Fundamentals Hub](../01%20-%20Virtualization/README.md) | [Repository Overview](../README.md)

---

## Overview

This document is my personal technical lab journal recording the 14 practical exercises I completed during my Windows Server administration and SOC Analyst training.

All labs were executed inside a live virtual enterprise environment consisting of:
- **DC01:** Windows Server 2022 Standard Evaluation (Domain Controller, IP: `192.168.10.10`, Domain: `soclab.local`)
- **CLIENT01:** Windows 10/11 Enterprise (Domain-joined client workstation, IP: `192.168.10.20`)
- **Network:** Isolated VirtualBox Internal Network (`SOC-LAB`)

Each lab documents the objective, related conceptual module, exact commands and procedures executed, verification steps, screenshot evidence, troubleshooting notes, and direct lessons learned for SOC defensive work.

---

## Table of Contents

1. [Practical Lab 01 - To Know the Windows Server Edition](#practical-lab-01---to-know-the-windows-server-edition)
2. [Practical Lab 02 - To Know Detailed Information About the System](#practical-lab-02---to-know-detailed-information-about-the-system)
3. [Practical Lab 03 - Explore the Server Manager](#practical-lab-03---explore-the-server-manager)
4. [Practical Lab 04 - Explore Roles and Features](#practical-lab-04---explore-roles-and-features)
5. [Practical Lab 05 - Explore Computer Management](#practical-lab-05---explore-computer-management)
6. [Practical Lab 06 - Explore and Manage Windows Services](#practical-lab-06---explore-and-manage-windows-services)
7. [Practical Lab 07 - Manage Domain Users in Active Directory](#practical-lab-07---manage-domain-users-in-active-directory)
8. [Practical Lab 08 - Manage Security Groups](#practical-lab-08---manage-security-groups)
9. [Practical Lab 09 - Configure NTFS Permissions](#practical-lab-09---configure-ntfs-permissions)
10. [Practical Lab 10 - NTFS Permission Scenarios](#practical-lab-10---ntfs-permission-scenarios)
11. [Practical Lab 11 - Create and Access a Network Shared Folder](#practical-lab-11---create-and-access-a-network-shared-folder)
12. [Practical Lab 12 - Share + NTFS Permission Scenarios](#practical-lab-12---share--ntfs-permission-scenarios)
13. [Practical Lab 13 - Hidden Shares & Administrative Shares](#practical-lab-13---hidden-shares--administrative-shares)
14. [Practical Lab 14 - Complete Access-Control Scenario](#practical-lab-14---complete-access-control-scenario)

---


<a id="practical-lab-01"></a><a id="practical-lab-01--to-know-the-windows-server-edition"></a><a id="practical-lab-01---to-know-the-windows-server-edition"></a>
## Practical Lab 01 - To Know the Windows Server Edition

* **Objective:** Verify the exact edition, build, and version of the installed Windows Server operating system on DC01.
* **Target Machine:** `DC01` (Domain Controller)
* **Related Concept:** [01 - Windows Server Editions](01%20-%20Windows%20Server%20Editions/README.md)
* **Lab Baseline:** Machine provisioned in [Virtualization - Create Virtual Machines](../01%20-%20Virtualization/05%20-%20Lab%20Setup/02%20-%20Create%20and%20Configure%20Virtual%20Machines.md)

---

### Steps Taken

1. I logged into the `DC01` virtual machine desktop.
2. I opened **Command Prompt**.
3. I executed `winver`:

```cmd
winver
```

### Verification & Evidence

![Windows Version](Screenshots/01%20-%20Windows%20Version.png)

From the dialog output, I verified the following system parameters:
* **Operating System:** Microsoft Windows Server
* **Edition:** Windows Server 2022 Standard Evaluation
* **Version:** 21H2 (OS Build 20348)
* **Licensing State:** Time-limited evaluation build for testing and development

### What This Teaches for SOC Work

Verifying the exact edition and build is a fundamental step in asset inventory and vulnerability assessment. During incident response, an analyst must confirm whether a compromised system is running a supported, fully-patched build, and identify which native security capabilities and server roles the edition supports.

---

<a id="practical-lab-02"></a><a id="practical-lab-02--to-know-detailed-information-about-the-system"></a><a id="practical-lab-02---to-know-detailed-information-about-the-system"></a>
## Practical Lab 02 - To Know Detailed Information About the System

* **Objective:** Extract comprehensive operating system, kernel build, hardware architecture, RAM allocation, and domain membership details using the command line.
* **Target Machine:** `DC01`
* **Related Concept:** [01 - Windows Server Editions](01%20-%20Windows%20Server%20Editions/README.md)

---

### Steps Taken

1. In the Command Prompt window on `DC01`, I executed `systeminfo`:

```cmd
systeminfo
```

### Verification & Evidence

![System Information Output](Screenshots/02%20-%20System%20Information.png)

From the command output, I confirmed the following key details:
* **Host Name:** `WIN-DEF8VDFQ099` (default computer name assigned during setup)
* **OS Name:** Microsoft Windows Server 2022 Standard Evaluation
* **OS Version:** 10.0.20348 N/A Build 20348
* **System Type:** x64-based PC
* **Total Physical Memory:** 4,096 MB (confirming the 4GB RAM allocation configured in VirtualBox)
* **Domain:** `soclab.local`

### What This Teaches for SOC Work

1. `systeminfo` is one of the very first commands run by threat actors (and automated recon scripts like WinPEAS) following initial access to fingerprint the target OS, hotfixes applied, network cards, and domain architecture (MITRE ATT&CK T1082 - System Information Discovery).
2. For defenders, baseline system information is essential for patch management, asset tracking, and distinguishing normal system attributes from anomalous configurations.

---

<a id="practical-lab-03"></a><a id="practical-lab-03--explore-the-server-manager"></a><a id="practical-lab-03---explore-the-server-manager"></a>
## Practical Lab 03 - Explore the Server Manager

* **Objective:** Explore and document Server Manager as the centralized administrative dashboard for Windows Server.
* **Target Machine:** `DC01`
* **Related Concept:** [02 - Server Manager](02%20-%20Server%20Manager/README.md)

---

### Task 01 - Server Manager Dashboard

I opened **Server Manager** from the Start menu / taskbar.

![Server Manager Dashboard](Screenshots/31%20-%20Server%20Manager%20Dashboard.png)

I inspected the key elements of the central dashboard:
* **Navigation Pane (Left):**
  * **Dashboard:** Central overview showing server status and deployment options.
  * **Local Server:** Properties and settings of the current machine.
  * **AD DS:** Active Directory Domain Services role management shortcut.
  * **DNS:** Domain Name System role management shortcut.
  * **File and Storage Services:** Storage pools, volumes, shares, and disk management.
* **Top Navigation Bar:**
  * **Notifications (Flag Icon):** Displays operational alerts and task status.
  * **Manage:** Menu to add/remove roles and features or add remote servers to the console.
  * **Tools:** Consolidated launcher for administrative consoles.
  * **View:** Window layout and zoom controls.

---

### Task 02 - Explore Local Server Properties

I clicked **Local Server** in the left navigation pane to inspect the system configuration summary:

![Server Manager Local Server View](Screenshots/32%20-%20Server%20Manager%20-%20Local%20Server.png)

I recorded the baseline server parameters:
* **Computer name:** `WIN-DEF8VDFQ099`
* **Domain:** `soclab.local`
* **Windows Defender Firewall:** Domain: On
* **Remote Management:** Enabled
* **Remote Desktop:** Disabled
* **NIC Configuration:** Static IP `192.168.10.10`, IPv6 Enabled
* **Total Physical Memory:** 4.00 GB
* **Time Zone:** Pacific Time (US & Canada)

---

### Task 03 - Explore the Manage Menu

I clicked the **Manage** menu in the top bar to inspect role and deployment options:

![Server Manager Manage Menu](Screenshots/33%20-%20Server%20Manager%20-%20Manage.png)

The menu provides four primary capabilities:
1. **Add Roles and Features:** Launches the wizard to install server components.
2. **Remove Roles and Features:** Launches the wizard to decommission installed components.
3. **Add Servers:** Connects remote Windows Server instances for centralized multi-server management.
4. **Create Server Group:** Organizes managed servers into logical collections.

---

### Task 04 - Explore Administrative Tools

I clicked the **Tools** menu to review the installed administrative consoles:

![Server Manager Tools Menu](Screenshots/34%20-%20Server%20Manager%20-%20Tools.png)

Key management consoles available:
* **Active Directory Users and Computers (`dsa.msc`):** Manage domain accounts, OUs, and security groups.
* **Computer Management (`compmgmt.msc`):** Consolidated system management (Local Users, Event Viewer, Services, Disks).
* **DNS Manager (`dnsmgmt.msc`):** Configure forward/reverse lookup zones and DNS records.
* **Event Viewer (`eventvwr.msc`):** Inspect Windows Security, System, and Application logs.
* **Services (`services.msc`):** Manage background Windows services and daemon startup states.

### What This Teaches for SOC Work

Server Manager provides a complete inventory of roles running on an asset. In a SOC investigation, knowing what roles a server hosts (e.g., AD DS Domain Controller vs File Server) determines the severity of security alerts and dictates which event logs (Security Event Log vs Directory Service Log) contain forensic evidence.

---

<a id="practical-lab-04"></a><a id="practical-lab-04--explore-roles-and-features"></a><a id="practical-lab-04---explore-roles-and-features"></a>
## Practical Lab 04 - Explore Roles and Features

* **Objective:** Walk through the complete Add Roles and Features Wizard, analyze role dependencies, and examine the installation of Active Directory Domain Services and DNS.
* **Target Machine:** `DC01`
* **Related Concept:** [03 - Roles vs Features](03%20-%20Roles%20vs%20Features/README.md)

---

### Task 01 - Launch Add Roles and Features Wizard

From Server Manager, I clicked **Manage -> Add Roles and Features**.

![Add Roles and Features Wizard](Screenshots/35%20-%20Server%20Manager%20-%20Add%20Roles%20and%20Features%20Wizard.png)

The navigation sidebar outlines the installation process:
* **Before You Begin:** Verifies administrative prerequisites (strong passwords, static IP addresses, Windows updates).
* **Installation Type:** Selects the deployment model.
* **Server Selection:** Targets the destination server.
* **Server Roles:** Selects major server roles.
* **Features:** Selects supporting software components.
* **Confirmation:** Final review before installation.

---

### Task 02 - Select Installation Type

I clicked **Next** to proceed to the Installation Type screen:

![Select Installation Type](Screenshots/36%20-%20Server%20Manager%20-%20Select%20Installation%20Type.png)

I examined the two installation types:
1. **Role-based or feature-based installation:** Configures a single server by adding roles, role services, and features. This is the standard method for general server configuration.
2. **Remote Desktop Services installation:** Deploys Virtual Desktop Infrastructure (VDI) or session-based remote desktop components across multiple servers.

---

### Task 03 - Select Destination Server

I proceeded to the Server Selection screen:

![Select Destination Server](Screenshots/37%20-%20Server%20Manager%20-%20Selection%20Destination%20Server.png)

Windows provides two targeting options:
1. **Select a server from the server pool:** Chooses a server currently managed by Server Manager (local machine `WIN-DEF8VDFQ099` at `192.168.10.10` or a remote server).
2. **Select a virtual hard disk:** Installs roles and features offline directly into a `.vhd` or `.vhdx` file without running the VM.

---

### Task 04 - Inspect Server Roles

On the **Server Roles** page, I reviewed the roles available in Windows Server:

![Select Server Roles](Screenshots/38%20-%20Select%20Server%20Roles.png)

Key roles examined:
* **Active Directory Domain Services (AD DS):** Centralized identity management and authentication for users, computers, and groups.
* **DNS Server:** Name resolution services, translating domain names to IP addresses.
* **File and Storage Services:** Technologies for managing storage volumes, quotas, and SMB file shares.
* **DHCP Server:** Dynamic IP address assignment and network configuration for client workstations.
* **Web Server (IIS):** Microsoft's web application and HTTP hosting platform.

---

### Task 05 - Inspect Features

I proceeded to the **Features** selection screen:

![Select Features](Screenshots/39%20-%20Select%20Features.png)

Key features examined:
* **.NET Framework:** Application framework required by Windows software, management tools, and PowerShell modules.
* **BitLocker Drive Encryption:** Full-disk encryption protecting data at rest on server storage volumes.
* **Failover Clustering:** High-availability clustering allowing secondary nodes to take over workloads if the primary node fails.
* **Telnet Client:** Legacy command-line utility used for testing network port connectivity.

### What This Teaches for SOC Work

1. **Attack Surface Reduction:** Installing unnecessary roles or features increases the server attack surface. Every role introduces background services, listening network ports, and potential vulnerability vectors. Enterprise servers should strictly adhere to least functionality.
2. **Detection of Unauthorized Role Installation:** Installing roles like AD CS (Active Directory Certificate Services) or Hyper-V can indicate attacker persistence or domain escalation (e.g., AD CS abuse / ESC1-ESC8). Monitoring Event ID **4624** (Logon) followed by Event ID **7045** (New Service Installed) or CBS component installation logs in `C:\Windows\Logs\CBS\CBS.log` allows SOC analysts to detect rogue role additions.


<a id="practical-lab-05"></a><a id="practical-lab-05--explore-computer-management"></a><a id="practical-lab-05---explore-computer-management"></a>
## Practical Lab 05 - Explore Computer Management

* **Objective:** Explore Computer Management as the centralized administration console for Windows system tools, storage, and service management.
* **Target Machine:** `DC01`
* **Related Concept:** [04 - Computer Management](04%20-%20Computer%20Management/README.md)

---

### Task 01 - Launch Computer Management

I opened Computer Management using the administrative console launcher:
1. In Server Manager, I clicked **Tools -> Computer Management** (or executed `compmgmt.msc` from Run).
2. I inspected the three primary branches in the console tree:
   * **System Tools:** Utilities for task automation, log analysis, shared folder management, and hardware inspection.
   * **Storage:** Disk partitioning, volume formatting, and filesystem health.
   * **Services and Applications:** Background service control and WMI management.

![Computer Management Console](Screenshots/40%20-%20Computer%20Management%20-%20Task%20-1.png)

---

### Task 02 - Explore System Tools

I expanded the **System Tools** container:

![System Tools Node](Screenshots/41%20-%20System%20Tools.png)

Key utilities evaluated:
* **Task Scheduler:** Schedules automated scripts, routine backups, and maintenance triggers.
* **Event Viewer:** Centralized operating system and security event logging engine.
* **Shared Folders:** Real-time visibility into active SMB network shares, user sessions, and open file handles.
* **Device Manager:** Virtualized hardware inventory and device driver configuration.

---

### Task 03 - Explore Event Viewer

I expanded **System Tools -> Event Viewer -> Windows Logs** to examine event categories:

![Event Viewer Windows Logs](Screenshots/42%20-%20Event%20Viewer.png)

Core log files evaluated:
* **Application:** Events generated by installed applications and third-party software.
* **Security:** Audit records documenting successful and failed logon attempts, privilege escalation, object access, and account management.
* **Setup:** Records relating to operating system updates and role provisioning.
* **System:** Operating system kernel, driver, and system service state changes.
* **Forwarded Events:** Events collected from remote hosts via Windows Event Forwarding (WEF).

---

### Task 04 - Explore Shared Folders Management

I expanded **System Tools -> Shared Folders** to view current file sharing state:

![Shared Folders Node](Screenshots/43%20-%20Shared%20Folders.png)

Three operational views examined:
* **Shares:** All currently exposed SMB shares on the server (e.g., `C$`, `ADMIN$`, `IPC$`, `SYSVOL`, `NETLOGON`).
* **Sessions:** Active remote connections showing client IP addresses, username, and connection duration.
* **Open Files:** Live file locks held by remote users over the network.

---

### Task 05 - Explore Device Manager

I opened **Device Manager** to inspect the virtualized hardware layer:

![Device Manager Virtualized Hardware](Screenshots/44%20-%20Device%20Manager.png)

Because DC01 runs inside VirtualBox, the devices listed (storage controllers, network adapters, display adapters) represent virtualized hardware passed through by the Type-2 hypervisor.

---

### Task 06 - Explore Disk Management

I navigated to **Storage -> Disk Management** to inspect the server's partition scheme:

![Disk Management Partition Layout](Screenshots/45%20-%20Disk%20Management.png)

I recorded the disk geometry:
* **Disk 0:** Basic virtual disk initialized with 80 GB total capacity.
* **System Reserved:** 100 MB partition holding the Boot Configuration Data (BCD).
* **C: Partition:** ~79.90 GB NTFS partition containing the Windows operating system and user directories.
* **Unallocated Space:** 0 MB (all allocated).

---

### Task 07 - Inspect Registered Services

I navigated to **Services and Applications -> Services** to review the background services registered on DC01:

![Services List in Computer Management](Screenshots/46%20-%20Services.png)

Key columns analyzed:
* **Service Name:** Internal system identifier.
* **Description:** Functional description of the service's purpose.
* **Startup Type:** Boot configuration (Automatic, Manual, Disabled).
* **Status:** Live execution state (Running or Stopped).
* **Log On As:** Security principal used to execute the service process (e.g., `Local System`, `Network Service`).

### What This Teaches for SOC Work

Computer Management consolidates the primary tools needed for host-level forensic analysis and triage. In incident response, an analyst examines Task Scheduler for persistence mechanisms (MITRE ATT&CK T1053.005), inspects Shared Folders for active SMB exfiltration sessions, and monitors Services for rogue daemon installation (MITRE ATT&CK T1543.003).

---

<a id="practical-lab-06"></a><a id="practical-lab-06--explore-and-manage-windows-services"></a><a id="practical-lab-06---explore-and-manage-windows-services"></a>
## Practical Lab 06 - Explore and Manage Windows Services

* **Objective:** Understand how Windows services operate, inspect service properties and dependencies, and perform controlled start/stop tests on a non-critical service.
* **Target Machine:** `DC01`
* **Related Concept:** [05 - Windows Services](05%20-%20Windows%20Services/README.md)

---

### Task 01 - Launch Services Console

I opened the Services console using `services.msc` from Run (or via Server Manager -> Tools -> Services).

![Services Console](Screenshots/46%20-%20Services.png)

I identified critical infrastructure services running on this domain controller:
* `NTDS` (Active Directory Domain Services)
* `DNS` (DNS Server)
* `wuauserv` (Windows Update)
* `WinDefend` (Microsoft Defender Antivirus Service)
* `RpcSs` (Remote Procedure Call)

---

### Task 02 - Select a Non-Critical Service for Testing

To avoid destabilizing the domain controller, I selected the **Print Spooler** (`Spooler`) service for live testing. Critical services (NTDS, DNS, RpcSs) must never be stopped during normal operations.

---

### Task 03 - Inspect Print Spooler Properties

I double-clicked **Print Spooler** to open its properties dialog:

![Print Spooler Properties](Screenshots/47%20-%20Print%20Spooler%20Properties.png)

I recorded the following service attributes:
* **Service name:** `Spooler`
* **Display name:** `Print Spooler`
* **Path to executable:** `C:\Windows\System32\spoolsv.exe`
* **Startup type:** `Automatic`
* **Service status:** `Running`
* **Log on as:** `Local System`

---

### Task 04 - Perform Controlled Start/Stop Operations

I tested manual state management:
1. I clicked **Stop**. The service status changed to stopped (blank).
2. I confirmed that stopping the service did not alter its configured `Automatic` startup type; it simply terminated the running `spoolsv.exe` process.
3. I clicked **Start**. The service status returned to `Running`.

---

### Task 05 - Analyze Service Dependencies

I navigated to the **Dependencies** tab of Print Spooler to evaluate cascade failure risk:

![Print Spooler Dependencies](Screenshots/48%20-%20Dependencies%20of%20PS.png)

I observed that Print Spooler depends on two foundational components:
1. **HTTP Service (`HTTP`):** Handles web-based printing and print server network calls.
2. **Remote Procedure Call (`RpcSs`):** Core inter-process communication protocol.

If either `HTTP` or `RpcSs` fails or is stopped, Print Spooler immediately fails as well.

### What This Teaches for SOC Work

1. **Service-Based Persistence & Privilege Escalation:** Attackers frequently create malicious services (e.g., PsExec creating `PSEXESVC`, Metasploit payloads) or modify existing service binary paths (ImageHijack / ImagePath manipulation) to execute arbitrary commands under `NT AUTHORITY\SYSTEM`.
2. **Service Hunting:** SOC analysts use `Get-Service`, `sc query`, and Sysmon Event ID **1** (Process Creation) + Windows Security Event ID **7045** (A new service was installed in the system) to detect persistence.
3. **Print Spooler Risk:** Print Spooler has historically suffered critical vulnerabilities (e.g., PrintNightmare - CVE-2021-34527). On domain controllers that do not handle printing, security hardening standards require disabling Print Spooler entirely.

---

<a id="practical-lab-07"></a><a id="practical-lab-07--manage-domain-users-in-active-directory"></a><a id="practical-lab-07---manage-domain-users-in-active-directory"></a>
## Practical Lab 07 - Manage Domain Users in Active Directory

* **Objective:** Create, configure, manage, and verify domain user accounts in Active Directory Domain Services using the Active Directory Users and Computers (ADUC) console.
* **Target Machine:** `DC01`
* **Related Concept:** [06 - Local Users and Groups](06%20-%20Local%20Users%20and%20Groups/README.md)
* **Domain:** `soclab.local`

---

### Task 01 - Launch Active Directory Users and Computers

I opened **Active Directory Users and Computers** (`dsa.msc`) from Server Manager -> Tools.

![Active Directory Users and Computers Console](Screenshots/49%20-%20ADUC.png)

---

### Task 02 - Explore the Domain Structure & SOC Organizational Unit

I expanded `soclab.local` in the left pane to view the directory tree:

![Domain Tree soclab.local](Screenshots/50%20%20-%20Soclab.local.png)

I located the dedicated **SOC** Organizational Unit (OU) created to house departmental users and groups:

```text
soclab.local
`-- SOC
    |-- Users
    `-- Groups
```

![SOC Organizational Unit Contents](Screenshots/51%20-%20Soc%20users.png)

---

### Task 03 - Create a New Domain User Account

Inside the `SOC` OU, I created a new testing account:
1. I right-clicked the empty space inside the `SOC` OU and selected **New -> User**.
2. I entered the account metadata:
   * **First name:** `Test`
   * **Last name:** `Analyst`
   * **User logon name:** `test.analyst@soclab.local`
3. I assigned a complex password and completed the wizard.

![Test Analyst User Created](Screenshots/52%20-%20SOC%20test%20.png)

---

### Task 04 - Test Account Lifecycle: Disable and Enable Account

To practice security containment, I tested the disable/enable workflow:
1. I right-clicked `Test Analyst` and selected **Disable Account**.
2. A downward-pointing black arrow appeared over the account icon, confirming disabled state.

![Account Disabled with Downward Arrow](Screenshots/53%20-%20Disabled.png)

3. I right-clicked the account and selected **Enable Account**.
4. Windows confirmed the account was re-enabled, and the downward arrow disappeared.

![Account Re-Enabled](Screenshots/54-%20Enabled.png)

**SOC Rationale for Disabling vs Deleting:**
During an incident investigation or employee offboarding, accounts are **disabled** rather than deleted. Deleting an account destroys its unique Security Identifier (SID), breaking audit trails in historical security logs and orphaning file ownership. Disabling cuts off access instantly while preserving forensic evidence.

---

### Task 05 - Reset User Password

I practiced administrative credential resets:
1. I right-clicked `Test Analyst` and selected **Reset Password**.
2. I entered a new temporary password and checked **User must change password at next logon**.
3. Windows confirmed the password was successfully reset.

![Password Reset Confirmation](Screenshots/55-%20%20Password%20Reset.png)

---

### Task 06 - Verify the User in Active Directory

I reviewed the `SOC` OU to verify that the account was properly positioned within the directory hierarchy:

```text
soclab.local
`-- SOC
    |-- SOC Analyst1
    |-- SOC Analyst2
    |-- SOC Manager1
    `-- Test Analyst
```

![SOC OU Directory Structure Verified](Screenshots/52%20-%20SOC%20test%20.png)

### What This Teaches for SOC Work

1. **Identity Threat Detection:** Monitoring user lifecycle events is a primary SOC detection use case:
   * Event ID **4720:** An account was created.
   * Event ID **4722:** An account was enabled.
   * Event ID **4724:** An attempt was made to reset an account's password.
   * Event ID **4725:** An account was disabled.
   * Event ID **4726:** An account was deleted.
2. Threat actors who gain domain persistence often create rogue accounts or re-enable dormant accounts. Correlating these event IDs with administrative change requests helps detect unauthorized access.

---

<a id="practical-lab-08"></a><a id="practical-lab-08--manage-security-groups"></a><a id="practical-lab-08---manage-security-groups"></a>
## Practical Lab 08 - Manage Security Groups

* **Objective:** Create and manage Active Directory security groups, configure group memberships, and implement role-based access control.
* **Target Machine:** `DC01`
* **Related Concept:** [06 - Local Users and Groups](06%20-%20Local%20Users%20and%20Groups/README.md)
* **Domain:** `soclab.local`

---

### Task 01 - Inspect Existing SOC Security Groups

I opened **Active Directory Users and Computers** (`dsa.msc`) and navigated to the `SOC` OU:

![Navigating to SOC OU](Screenshots/50%20%20-%20Soclab.local.png)

I reviewed the baseline security groups already provisioned:
* `SOC-Analysts`
* `SOC-Managers`

I inspected the **Members** tab of `SOC-Analysts`:
* Members: `SOC Analyst1`, `SOC Analyst2`

![SOC-Analysts Group Members](Screenshots/56%20-%20Soc-group.png)

I inspected the **Members** tab of `SOC-Managers`:
* Member: `SOC Manager1`

![SOC-Managers Group Members](Screenshots/57%20-%20Soc-managers.png)

---

### Task 02 - Create the SOC-Admins Security Group

To separate administrative functions from daily analyst duties, I created a dedicated security group:
1. Inside the `SOC` OU, I right-clicked empty space and selected **New -> Group**.
2. I configured the group properties:
   * **Group name:** `SOC-Admins`
   * **Group scope:** `Global`
   * **Group type:** `Security`
3. I clicked **OK** to commit.

![Creating SOC-Admins Group](Screenshots/58%20-%20Soc-admins.png)

---

### Task 03 - Add a User to the SOC-Admins Group

I assigned the `Test Analyst` account to the new administrative group:
1. I opened the properties of `SOC-Admins` and selected the **Members** tab.
2. I clicked **Add**, typed `Test Analyst`, and clicked **Check Names**.
3. I clicked **OK** and **Apply**.

![Test Analyst Added to SOC-Admins](Screenshots/59%20-%20soc-admin-member.png)

---

### Task 04 - Active Directory Security Model

The resulting organizational model maps individual users to functional roles:

```text
Individual Accounts               Domain Security Groups
-------------------               ----------------------
SOC Analyst1  ---+
                 +--------------> SOC-Analysts (Global Security)
SOC Analyst2  ---+

SOC Manager1  ------------------> SOC-Managers (Global Security)

Test Analyst  ------------------> SOC-Admins (Global Security)
```

**Security Principle:**
Permissions must never be assigned directly to individual user accounts. Assigning permissions to security groups enables centralized, scalable access governance. When personnel transfer roles, administrators update group memberships rather than modifying Access Control Lists on individual servers.

### What This Teaches for SOC Work

1. **Privilege Escalation Monitoring:** Adding a user to a high-privilege group is one of the most critical security events in Active Directory:
   * Event ID **4728:** A member was added to a security-enabled global group.
   * Event ID **4732:** A member was added to a security-enabled local group (e.g., local Administrators).
   * Event ID **4756:** A member was added to a security-enabled universal group.
2. Attackers perform "Token Manipulation" or add compromised accounts to privileged groups (e.g., Domain Admins, Enterprise Admins) to achieve persistence (MITRE ATT&CK T1098 - Account Manipulation). Monitoring these event IDs is mandatory in enterprise SOCs.


<a id="practical-lab-09"></a><a id="practical-lab-09--configure-ntfs-permissions"></a><a id="practical-lab-09---configure-ntfs-permissions"></a>
## Practical Lab 09 - Configure NTFS Permissions

* **Objective:** Configure granular NTFS permissions on a dedicated folder structure using Active Directory security groups, observing inheritance and access control entries.
* **Target Machine:** `DC01`
* **Related Concept:** [07 - NTFS Permissions](07%20-%20NTFS%20Permissions/README.md)
* **Domain:** `soclab.local`

---

### Task 01 - Create the Lab Directory Structure

I created a dedicated testing directory on `DC01` to avoid touching operating system directories:
1. I opened File Explorer and navigated to `C:\`.
2. I created a root directory named `SOC-Lab`.
3. Inside `C:\SOC-Lab`, I created a subfolder named `Reports`.

```text
C:\
`-- SOC-Lab
    `-- Reports
```

![Reports Folder Created](Screenshots/60%20-%20Reports.png)

---

### Task 02 - Create Test Documents

To verify file-level permissions during subsequent tests, I created two test files inside `C:\SOC-Lab\Reports`:
1. `Analyst-Report.txt`: Created with baseline triage text and saved.
2. `Manager-Report.txt`: Created with summary text and saved.

![Creating Analyst Report](Screenshots/61%20-%20First%20file.png)

![Creating Manager Report](Screenshots/61%20-%20Second%20file.png)

---

### Task 03 - Inspect NTFS Advanced Security Settings

To manage permissions at the filesystem level, I opened the Advanced Security Settings:
1. I right-clicked `C:\SOC-Lab\Reports` and selected **Properties**.
2. I switched to the **Security** tab and clicked **Advanced**.

![Advanced Security Settings](Screenshots/62%20-%20Security%20Advanced.png)

I analyzed the core components of the Access Control List (ACL):
* **Principal:** The user, group, or service account to which the rule applies.
* **Type:** Allow or Deny.
* **Access:** The granular permission granted (Full control, Modify, Read & execute, Read, Write).
* **Inherited from:** Identifies whether the rule originated from a parent folder (e.g., `C:\SOC-Lab`) or was applied explicitly.
* **Applies to:** Defines the inheritance scope (This folder, subfolders, and files).

---

### Task 04 - Understand Permission Inheritance

By default, new folders inherit permissions from their parent container. In this configuration:
* `C:\SOC-Lab` passes its baseline permissions down to `Reports`.
* `Reports` automatically passes these permissions down to any files created inside it.

```text
C:\SOC-Lab (Parent)
    |
    | (Inherited permissions flow downward)
    v
 Reports (Child)
    |
    v
  Files
```

---

### Task 05 - Assign Read & Execute to SOC-Analysts

1. On the Security tab of `Reports`, I clicked **Edit** and then **Add**.
2. I added `SOC-Analysts` from `soclab.local`.
3. I checked **Allow** for **Read & execute** (which automatically enabled *List folder contents* and *Read*).
4. I clicked **Apply**.

![Assigning Read and Execute to SOC-Analysts](Screenshots/63%20-%20Soc%20analysts%20permissions.png)

---

### Task 06 - Assign Modify to SOC-Managers

1. I clicked **Add** and selected `SOC-Managers`.
2. I checked **Allow** for **Modify** (which automatically enabled *Read & execute*, *List folder contents*, *Read*, and *Write*).
3. I clicked **Apply**.

![Assigning Modify to SOC-Managers](Screenshots/65%20-%20Soc%20manager%20permissions.png)

---

### Task 07 - Assign Full Control to SOC-Admins

1. I clicked **Add** and selected `SOC-Admins`.
2. I checked **Allow** for **Full control**.
3. I clicked **Apply** and **OK**.

![Assigning Full Control to SOC-Admins](Screenshots/64%20-%20Soc%20Admin%20permissions.png)

---

### Task 08 - Permission Design Summary

I established a complete role-based permission hierarchy:

| Group | NTFS Permission | Purpose |
| :--- | :--- | :--- |
| **SOC-Analysts** | Read & Execute | Can view directory contents and open files without altering data. |
| **SOC-Managers** | Modify | Can read, write, edit, and delete reports. |
| **SOC-Admins** | Full Control | Full administrative control, including modifying ACLs and taking ownership. |

### What This Teaches for SOC Work

1. **Principle of Least Privilege:** Standard users (SOC analysts) must never possess write or delete permissions on central report directories. Restricting permissions prevents accidental data destruction or intentional tampering by malicious insiders.
2. **Access Control Auditing:** NTFS permissions are enforced by the Windows Security Reference Monitor (SRM). When a user attempts to access a file, Windows evaluates the user's access token against the Discretionary Access Control List (DACL).

---

<a id="practical-lab-10"></a><a id="practical-lab-10--ntfs-permission-scenarios"></a><a id="practical-lab-10---ntfs-permission-scenarios"></a>
## Practical Lab 10 - NTFS Permission Scenarios

* **Objective:** Test and validate effective NTFS permissions across different user roles, test inheritance and explicit permissions, and analyze permission conflicts.
* **Target Machine:** `DC01`
* **Related Concept:** [07 - NTFS Permissions](07%20-%20NTFS%20Permissions/README.md)
* **Domain:** `soclab.local`

---

### Task 01 - Test Analyst Access (Read-Only Enforcement)

I validated access for standard analysts using the `SOC Analyst2` account:
1. I opened `C:\SOC-Lab\Reports\Analyst-Report.txt`. The file opened successfully (Read access confirmed).
2. I attempted to add text and save the file. Windows rejected the operation with an `Access is denied` prompt.

![Analyst Save Blocked - Access Denied](Screenshots/66%20-%20Soc%20analyst2%20permission%20errors.png)

3. I attempted to delete `Analyst-Report.txt`. Windows blocked the deletion, displaying a permission error dialog.

![Analyst Delete Blocked](Screenshots/67%20-%20File%20Delete%20Permission.png)

**Observation:** The `SOC-Analysts` group permission strictly enforced read-only access. Modification and deletion were completely blocked.

---

### Task 02 - Test Manager Access (Modify Enforcement)

Next, I tested operational rights using the `SOC Manager1` account:
1. I opened `C:\SOC-Lab\Reports\Manager-Report.txt`, added text, and saved. The file saved successfully without error.
2. I created a new text document named `Weekly-Brief.txt`. The file was created immediately.

![Manager Successfully Created File](Screenshots/68%20-%20soc.png)

3. I deleted `Weekly-Brief.txt`. The deletion succeeded without prompting.

![Manager Successfully Deleted File](Screenshots/69%20-%20new.png)

**Observation:** The `SOC-Managers` group held complete operational capability (Read, Write, Create, Delete) under the **Modify** permission.

---

### Task 03 - Test Administrator Access (Full Control Enforcement)

I tested administrative control using the account belonging to `SOC-Admins`:
1. I navigated to `C:\SOC-Lab\Reports`, opened folder Properties, and switched to the Security tab.
2. I opened **Advanced** settings and altered Access Control Entries.

![Admin Full Control Permissions Dialog](Screenshots/70-%20%20Admin%20Permissions.png)

**Observation:** Full Control grants two unique rights not available in Modify:
* **Change Permissions:** The ability to add, edit, or delete entries in the Discretionary Access Control List (DACL).
* **Take Ownership:** The ability to seize ownership of the object even if locked out.

---

### Task 04 - Verified NTFS Access Matrix

| Account | Group | Read Files | Modify Files | Delete Files | Change Permissions |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **SOC Analyst1 / Analyst2** | `SOC-Analysts` | Allowed | Denied | Denied | Denied |
| **SOC Manager1** | `SOC-Managers` | Allowed | Allowed | Allowed | Denied |
| **Admin Account** | `SOC-Admins` | Allowed | Allowed | Allowed | Allowed |

---

### Task 05 - Test Inheritance Propagation

I verified how NTFS permissions propagate to newly created child folders:
1. Inside `C:\SOC-Lab\Reports`, I created a new subfolder named `Daily`.
2. I opened **Properties -> Security -> Advanced** on the `Daily` subfolder.

![Daily SubFolder Inheriting Permissions](Screenshots/71%20-%20Daily%20SubFolder.png)

**Observation:**
The permissions for `SOC-Analysts`, `SOC-Managers`, and `SOC-Admins` appeared automatically. The **Inherited from** column clearly stated `C:\SOC-Lab\Reports\`, proving that child objects inherit DACL entries from their parent containers by default.

---

### Task 06 - Configure and Identify Explicit Permissions

To distinguish between inherited and explicit permissions:
1. Inside the `Daily` folder's Advanced Security settings, I clicked **Add**.
2. I selected `Test Analyst` and granted basic **Read** permission.
3. I inspected the ACL list.

![Explicit Permission on Test Analyst](Screenshots/72%20-%20Test%20Analyst%20Explict%20permissions.png)

**Observation:**
* For `SOC-Analysts`, the "Inherited from" column displayed `C:\SOC-Lab\Reports\`.
* For `Test Analyst`, the "Inherited from" column displayed `None` (or `<not inherited>`).

This visual difference demonstrates how administrators distinguish between inherited baseline rules and explicit overrides applied directly to an individual object.

---

### Task 07 - Permission Evaluation & The Deny Precedence Rule

When Windows evaluates effective access for a user, it follows strict precedence rules:

1. **Explicit Deny** beats **Explicit Allow**.
2. **Explicit Allow** beats **Inherited Deny**.
3. **Inherited Deny** beats **Inherited Allow**.
4. If neither Allow nor Deny is matched, access is implicitly **Denied**.

**Administrative Best Practice:**
Avoid using explicit **Deny** permissions whenever possible. A single explicit Deny on a group overrides all Allow entries for that user across all their group memberships, creating complex troubleshooting issues. Robust security architectures rely exclusively on targeted **Allow** entries and least-privilege group scoping.

### What This Teaches for SOC Work

1. **Detecting Permission Tampering:** Attackers who compromise a domain account often modify NTFS permissions on sensitive directories (e.g., using `icacls`, `takeown`, or PowerShell `Set-Acl`) to stage data or grant persistence. Monitoring Windows Security Event ID **4670** (Permissions on an object were changed) is essential for detecting unauthorized DACL manipulation.
2. **Effective Access Triage:** When investigating data exfiltration or unauthorized file reads, SOC analysts must analyze effective permissions by tracing group memberships, inherited rules, and explicit permissions.

---

<a id="practical-lab-11"></a><a id="practical-lab-11--create-and-access-a-network-shared-folder"></a><a id="practical-lab-11---create-and-access-a-network-shared-folder"></a>
## Practical Lab 11 - Create and Access a Network Shared Folder

* **Objective:** Create a network shared folder on DC01, configure both Share and NTFS permissions, access it remotely from CLIENT01 using domain accounts, and monitor active network sessions.
* **Related Concept:** [08 - Shared Folders](08%20-%20Shared%20Folders/README.md) and [07 - NTFS Permissions](07%20-%20NTFS%20Permissions/README.md)
* **Target Machines:** `DC01` (Domain Controller / File Server) and `CLIENT01` (Domain-joined Windows 10 workstation)
* **Domain:** `soclab.local`

---

### Task 01 - Create the Folder Hierarchy

I logged into **DC01** and created the directory structure on the local `C:\` drive to store SOC operational records:

```text
C:\SOC-Reports
|-- Daily Reports
|-- Incident Reports
`-- Management Reports
```

1. I opened File Explorer on DC01 and navigated to `C:\`.
2. I created a master directory named `SOC-Reports`.
3. Inside `SOC-Reports`, I created three subfolders: `Daily Reports`, `Incident Reports`, and `Management Reports`.

![SOC-Reports Folder Structure](Screenshots/73%20-%20Reports.png)

---

### Task 02 - Create Sample Files

To test read, write, and delete permissions accurately during client testing, I populated each subfolder with a baseline text document:

```text
C:\SOC-Reports\Daily Reports\Daily-Report.txt
C:\SOC-Reports\Incident Reports\Incident-Report.txt
C:\SOC-Reports\Management Reports\Management-Report.txt
```

1. Inside `Daily Reports`, I created `Daily-Report.txt` with sample logging text.
2. Inside `Incident Reports`, I created `Incident-Report.txt` with sample triage data.
3. Inside `Management Reports`, I created `Management-Report.txt` with summary notes.

---

### Task 03 - Share the Folder on the Network

Next, I enabled network file sharing for the `SOC-Reports` directory:

1. On DC01, I right-clicked `C:\SOC-Reports` and selected **Properties**.
2. I navigated to the **Sharing** tab and clicked **Advanced Sharing**.
3. I checked the box labeled **Share this folder**.
4. I kept the default Share name as `SOC-Reports`.

![Advanced Sharing Configuration](Screenshots/74%20-%20Report-Share-Permission.png)

This established the network UNC path as `\\WIN-DEF8VDFQ099\SOC-Reports` (or `\\DC01\SOC-Reports` / `\\192.168.10.10\SOC-Reports`).

---

### Task 04 - Configure Share Permissions

While in the **Advanced Sharing** dialog, I configured the network-level ("front door") permissions:

1. I clicked the **Permissions** button.
2. By default, the `Everyone` group was present.
3. For this initial test, I left `Everyone` set to **Read** only (unchecked Change and Full Control).
4. I clicked **Apply** and **OK**.

![Share Permissions Configured to Read Only](Screenshots/75%20-%20Report-Permissions.png)

**Network Access Architecture:**
When a network user connects, they must traverse two permission layers:

```text
Network Request from CLIENT01
           |
           v
  Share Permission (Network Front Door)
           |
           v
  NTFS Permission (File System ACL)
           |
           v
  Effective Access (Most Restrictive Wins)
```

---

### Task 05 - Configure Granular NTFS Permissions

I navigated to the **Security** tab of `C:\SOC-Reports` to define granular file system permissions for my domain security groups:

| Group | Assigned NTFS Permission | Administrative Intent |
| :--- | :--- | :--- |
| **SOC-Analysts** | Read & Execute | Analysts can read daily logs and templates without modifying records. |
| **SOC-Managers** | Modify | Managers can author, edit, and delete reports. |
| **SOC-Admins** | Full Control | Administrators maintain full management and permission control. |

1. On the **Security** tab, I clicked **Edit** and then **Add**.
2. I added `SOC-Analysts`, `SOC-Managers`, and `SOC-Admins` from `soclab.local`.
3. I assigned the permissions as specified in the table above.

![NTFS Security Permissions Assigned](Screenshots/76%20-%20NTFS-Permissions.png)

**Security Model In Place:**
At this point, I had configured:

```text
                  \\DC01\SOC-Reports
                           |
                      Share: Read
                           |
                           v
                    NTFS Permissions
          +----------------+----------------+
          |                                 |
          v                                 v
    SOC-Analysts                      SOC-Managers
   NTFS: Read & Exec                  NTFS: Modify
```

*Note: This deliberate configuration mismatch between Share (Read) and NTFS (Modify) forms the basis of the troubleshooting test in Task 08.*

---

### Task 06 - Access the Network Share from CLIENT01

I switched to the Windows 10 client machine (**CLIENT01**) to test domain network access:

1. I logged into **CLIENT01** as `soclab\SOC Analyst1`.
2. I opened File Explorer.
3. In the address bar, I typed the UNC path: `\\WIN-DEF8VDFQ099\SOC-Reports` (or `\\192.168.10.10\SOC-Reports`) and pressed **Enter**.

![Navigating to UNC Share from CLIENT01](Screenshots/77%20-%20CLIENT01.png)

**Observation:**
The shared folder opened immediately. CLIENT01 did not have local copies of these files; it accessed the live file system on DC01 over SMB because both systems belong to `soclab.local` on the `SOC-LAB` internal network.

---

### Task 07 - Test Analyst Account Permissions

From CLIENT01, logged in as `SOC Analyst1`, I tested each standard file operation:

1. **Test 1 - Open Folder:** Success. The subfolders opened without error.
2. **Test 2 - Read File:** Success. I opened `Daily-Report.txt` and read the contents.
3. **Test 3 - Create New File:** Failed (`Access is denied`). When I attempted to create a new text file inside the folder, Windows blocked the operation.
4. **Test 4 - Modify Existing File:** Failed (`Access is denied`). I could type text into Notepad, but clicking **Save** prompted a "Save As" dialog because the server rejected the write.
5. **Test 5 - Delete File:** Failed (`File Access Denied`). Pressing Delete generated an error dialog requiring administrative permissions.

![Analyst Access Denied Creating Files](Screenshots/78%20-%20Errors-Folder.png)

![Analyst Access Denied Deleting Files](Screenshots/79%20-%20Folder-Errors.png)

**Conclusion:** The `SOC-Analysts` group configuration functioned exactly as intended for read-only triage personnel.

---

### Task 08 - Test Manager Permissions & The Effective Permission Trap

Next, I logged out of CLIENT01 and logged back in as `soclab\SOC Manager1` to verify manager rights:

1. I opened `\\WIN-DEF8VDFQ099\SOC-Reports`.
2. I tested file operations:
   * **Test 1 - Read File:** Success.
   * **Test 2 - Create File:** Failed (`Access is denied`).
   * **Test 3 - Modify File:** Failed (`Access is denied`).
   * **Test 4 - Delete File:** Failed (`Access is denied`).

![Manager Blocked Creating New Files](Screenshots/81%20-%20Manager%20Creation.png)

![Manager Blocked Deleting Files](Screenshots/80%20-%20Manager-Permissions.png)

**Why Did the Manager Fail Despite NTFS Modify Rights?**
This demonstrated the classic **Effective Permission Trap**:
* On the NTFS Security tab, `SOC-Managers` has **Modify** permissions.
* On the Share Permissions tab, `Everyone` was configured with **Read** only.
* When accessing resources over the network (SMB), Windows evaluates both layers and enforces the **most restrictive** permission:

```text
Share Permission: Read
       +
NTFS Permission:  Modify
       =
Effective Access: Read
```

**Resolution:**
To allow managers to modify files over the network without weakening security, an administrator sets the network **Share permission to Full Control (or Change)** for authenticated users, and allows the granular **NTFS permissions** to govern actual file access.

---

### Task 09 - Compare Local vs Network Access

To solidify this concept, I verified how Windows handles local versus network requests:

```text
Local Access (Logged into DC01 directly):
  User opens C:\SOC-Reports
  Only NTFS permissions apply (Manager has full Modify rights).

Network Access (Connecting from CLIENT01 over SMB):
  User opens \\DC01\SOC-Reports
  Share permissions AND NTFS permissions apply.
  The most restrictive result is enforced.
```

---

### Task 10 - Verify Shares in Computer Management & CLI

I returned to DC01 to verify active shares using both graphical and command-line tools:

**GUI Method:**
1. I opened **Computer Management** (`compmgmt.msc`).
2. I navigated to **System Tools -> Shared Folders -> Shares**.
3. I observed `SOC-Reports` listed alongside system default shares (`C$`, `IPC$`, `ADMIN$`).

![Verifying Shares in Computer Management](Screenshots/82%20-%20Share.png)

**Command-Line Method:**
1. I opened Command Prompt.
2. I ran `net share`:

```cmd
net share
```

![Net Share Command Output](Screenshots/83%20-%20net%20share.png)

The command confirmed that `SOC-Reports` was shared from `C:\SOC-Reports`.

---

### Task 11 - Monitor Active Sessions and Open Files

While keeping `\\WIN-DEF8VDFQ099\SOC-Reports` open on CLIENT01, I monitored the live connection on DC01:

1. In **Computer Management**, I clicked **Shared Folders -> Sessions**.
2. I observed an active session originating from `CLIENT01` under the logged-in user account.
3. I clicked **Open Files** to inspect open file handles and lock statuses across the network.

![Monitoring Active Sessions in Computer Management](Screenshots/84%20-%20Sessions-cmpt.png)

---

### What This Teaches for SOC Work

1. **SMB Session Monitoring:** File sharing leaves detectable traces. Active sessions in Computer Management reflect real-time SMB sessions. In network traffic, this generates SMB2 Tree Connect and Create requests.
2. **Access Control Troubleshooting:** When users report "Access Denied" over the network, SOC analysts and administrators must check both Share and NTFS ACLs. If an attacker gains network share access, their privileges are capped by the most restrictive layer.
3. **Audit Logging:** Access attempts against file shares generate Windows Security Log Event ID **5140** (A network share object was checked) and Event ID **5145** (A network share object was accessed). Monitoring these events helps detect unauthorized file collection or ransomware staging.

---

<a id="practical-lab-12"></a><a id="practical-lab-12--share--ntfs-permission-scenarios"></a><a id="practical-lab-12---share--ntfs-permission-scenarios"></a>
## Practical Lab 12 - Share + NTFS Permission Scenarios

* **Objective:** Test and evaluate the four fundamental Share and NTFS permission combinations to understand effective network permissions, least privilege, and local access bypass.
* **Related Concept:** [08 - Shared Folders](08%20-%20Shared%20Folders/README.md)
* **Target Machines:** `DC01` (File Server) and `CLIENT01` (Network Client)

---

### Scenario 1 - Share Read + NTFS Modify

In this scenario, I configured conflicting permissions on DC01 and verified the result over the network from CLIENT01 using `SOC Manager1`:

* **Share Permission:** Read (assigned to `Everyone`)
* **NTFS Permission:** Modify (assigned to `SOC-Managers`)

```text
      Share Permission = Read
               +
      NTFS Permission  = Modify
               |
               v
  Effective Access     = Read
```

**Observation:**
When `SOC Manager1` connected over SMB, Windows evaluated both sets of permissions. Because the Share permission acts as the outer gate, setting it to Read prevented the user from creating, editing, or deleting any files, regardless of their NTFS Modify right.

---

### Scenario 2 - Share Change + NTFS Read

In this scenario, I tested whether a permissive Share permission could override a restrictive NTFS permission:

* **Share Permission:** Change (assigned to `Everyone`)
* **NTFS Permission:** Read (assigned to `SOC-Managers`)

```text
      Share Permission = Change
               +
      NTFS Permission  = Read
               |
               v
  Effective Access     = Read
```

**The Test:**
From CLIENT01, logged in as `SOC Manager1`, I attempted to create a new folder named `Internal Reports` inside the share.

**Observation:**
The action failed immediately with `Access is denied`. Even though the network share allowed changes, the underlying NTFS file system restricted the account to Read. The most restrictive rule always governs network access. Permissive share permissions cannot bypass restrictive NTFS permissions.

---

### Scenario 3 - Share Full Control + NTFS Modify (Enterprise Best Practice)

In this scenario, I applied the industry standard approach recommended for enterprise file servers:

* **Share Permission:** Full Control (assigned to `Everyone` or `Authenticated Users`)
* **NTFS Permission:** Modify (assigned to `SOC-Managers`)

```text
      Share Permission = Full Control
               +
      NTFS Permission  = Modify
               |
               v
  Effective Access     = Modify
```

**The Test:**
From CLIENT01, `SOC Manager1` attempted all daily file operations (reading, creating, modifying, and deleting files), followed by an attempt to modify the folder's security permissions via the Security tab.

**Observation:**
The manager successfully performed all file read/write/delete operations. However, when attempting to alter ACL permissions on the Security tab, Windows blocked the action. Because Share was set to Full Control, NTFS became the sole governing authority. Since the manager held Modify (not Full Control) in NTFS, permission changes were denied.

---

### Scenario 4 - Local vs Network Access (The Share Bypass)

This scenario demonstrates the critical difference between local interactive logon and remote SMB access:

Using the configuration from Scenario 1:
* **Share Permission:** Read
* **NTFS Permission:** Modify

| Connection Method | User | Pathway | Effective Result | Rationale |
| :--- | :--- | :--- | :--- | :--- |
| **Network (SMB)** | `SOC Manager1` | Connect from CLIENT01 to `\\DC01\SOC-Reports` | **Read** | Share Read restriction is enforced over network. |
| **Local Logon** | `SOC Manager1` | Log directly into DC01 desktop, open `C:\SOC-Reports` | **Modify** | Share permissions are completely bypassed; only NTFS applies. |

---

### Summary of Permission Combinations

| Scenario | Share Permission | NTFS Permission | Network Access Result | Local Access Result |
| :--- | :--- | :--- | :--- | :--- |
| **1** | Read | Modify | Read | Modify |
| **2** | Change | Read | Read | Read |
| **3** | Full Control | Modify | Modify | Modify |
| **4** | Full Control | Read | Read | Read |

---

### What This Teaches for SOC Work

1. **Lateral Movement Dynamics:** Attackers accessing a machine via network shares (e.g., `\\host\C$`, `\\host\shared_data`) are constrained by both Share and NTFS permissions. However, if an attacker elevates to interactive logon (via RDP, PsExec, or WinRM), Share permissions are completely bypassed.
2. **Defensive Architecture:** The enterprise best practice (Share: Full Control, NTFS: Granular) simplifies administration and prevents troubleshooting confusion. It centralizes all security enforcement in the NTFS file system where auditing, inheritance, and ownership can be monitored consistently.

---

<a id="practical-lab-13"></a><a id="practical-lab-13--hidden-shares--administrative-shares"></a><a id="practical-lab-13---hidden-shares--administrative-shares"></a>
## Practical Lab 13 - Hidden Shares & Administrative Shares

* **Objective:** Create and test a hidden network share, demonstrate why hiding a share provides zero security (security through obscurity), and inspect Windows default administrative shares.
* **Related Concept:** [08 - Shared Folders](08%20-%20Shared%20Folders/README.md)
* **Target Machines:** `DC01` (Domain Controller / File Server) and `CLIENT01` (Network Client)
* **Domain:** `soclab.local`

---

### Task 01 - Create a Hidden Share

To demonstrate how hidden shares operate, I created a sensitive test directory and configured it with a trailing dollar sign (`$`):

1. On **DC01**, I navigated to `C:\` and created a folder named `SOC-Secret`.
2. Inside `C:\SOC-Secret`, I created a text file named `Secret-Report.txt`.
3. I right-clicked `SOC-Secret`, opened **Properties -> Sharing -> Advanced Sharing**, and checked **Share this folder**.
4. In the **Share name** field, I entered `SOC-Secret$`.

![Configuring Hidden Share with Dollar Sign](Screenshots/85%20-%20Secret-FF.png)

> **Technical Note:** In Windows networking, appending a `$` character to the end of a share name designates it as a hidden share. Windows will omit this share from standard network browsing lists.

---

### Task 02 - Verify Share is Hidden from Network Browsing

I logged into **CLIENT01** to verify whether the share appeared in standard network listings:

1. I opened File Explorer.
2. In the address bar, I entered the server UNC path without a share name: `\\WIN-DEF8VDFQ099`.
3. I observed the visible shares listed on the server.

![Browsing Server Shares Hides Secret Share](Screenshots/87%20-%20File%20errors%20list.png)

**Observation:**
The standard `SOC-Reports` share was clearly visible, but `SOC-Secret$` did not appear in the directory listing. The share was successfully hidden from passive network browsing.

---

### Task 03 - Attempt Access Without the Trailing Dollar Sign

To test how Windows parses hidden share paths, I attempted to connect using the folder name without the `$` symbol:

1. In the CLIENT01 address bar, I entered `\\WIN-DEF8VDFQ099\SOC-Secret`.
2. Windows returned an error dialog: `Windows cannot access \\WIN-DEF8VDFQ099.soclab.local\SOC-Secret`.

![Windows Error When Accessing Without Dollar Sign](Screenshots/86%20-%20File%20Errors.png)

**Observation:**
Because the share was registered specifically as `SOC-Secret$`, SMB rejected requests directed to `SOC-Secret`. The server does not automatically correlate the share name without its explicit suffix.

---

### Task 04 - Access the Hidden Share Directly

Next, I tested direct access by typing the full, explicit UNC path:

1. In the File Explorer address bar, I entered `\\WIN-DEF8VDFQ099\SOC-Secret$`.
2. I pressed **Enter**.

![Hidden Share Accessed Directly via Full Path](Screenshots/88%20-%20Secret%20Appear.png)

**Observation:**
The folder opened immediately, and `Secret-Report.txt` was fully accessible.

**Key Technical Lesson: Hidden Does Not Mean Secure**
Appending a `$` only prevents a share from appearing in graphical network browse lists (NetServerEnum). It does **not**:
* Encrypt network traffic
* Restrict access permissions
* Provide authentication controls
* Protect data from discovery via port scanning or share enumeration tools

Anyone who knows or guesses the share name can access it directly if Share and NTFS permissions allow it. Security through obscurity is not security.

---

### Task 05 - Inspect Windows Default Administrative Shares

Windows automatically creates several built-in hidden shares for administrative and inter-process operations. I inspected these on DC01:

1. On **DC01**, I opened Command Prompt.
2. I executed `net share`:

```cmd
net share
```

![Default Administrative Shares in Net Share](Screenshots/89%20-%20net%20share.png)

**Administrative Shares Breakdown:**

| Share Name | Resource Path | Purpose |
| :--- | :--- | :--- |
| **`C$`** | `C:\` | Provides remote administrators with direct access to the entire root file system. |
| **`ADMIN$`** | `C:\Windows` | Maps to the Windows installation directory. Used by remote management tools, patch deployment, and RPC services. |
| **`IPC$`** | None (Named Pipes) | Facilitates Inter-Process Communication and remote named-pipe calls used by RPC, SMB authentication, and domain operations. |
| **`NETLOGON`** | `C:\Windows\SYSVOL\sysvol\soclab.local\scripts` | Used by domain controllers to deliver logon scripts and policies to client machines. |
| **`SYSVOL`** | `C:\Windows\SYSVOL\sysvol` | Stores Group Policy objects and domain replication data across domain controllers. |

> **Administrative Warning:** Default administrative shares (`C$`, `ADMIN$`, `IPC$`) must not be deleted or disabled on enterprise domain controllers. Disabling them breaks Active Directory replication, Group Policy processing, and remote management.

---

### What This Teaches for SOC Work

1. **Attacker Reconnaissance:** Threat actors frequently enumerate hidden and administrative shares using tools like `PowerView` (`Find-DomainShare`), BloodHound, or `crackmapexec smb --shares`.
2. **Lateral Movement Target:** Built-in shares like `C$` and `ADMIN$` are primary staging locations for lateral movement tools (e.g., PsExec, Impacket's `psexec.py` and `smbexec.py`). Attackers drop service binaries into `ADMIN$` or `C$\Windows\System32` and remotely create a service via DCE/RPC.
3. **Detection Opportunity:** SOC analysts should monitor Windows Security Event ID **5140** (A network share object was checked) and Event ID **5145** (A network share object was accessed with detailed permissions). High-risk alerts should trigger when non-administrative accounts attempt to access `ADMIN$` or `C$`.

---

<a id="practical-lab-14"></a><a id="practical-lab-14--complete-access-control-scenario"></a><a id="practical-lab-14---complete-access-control-scenario"></a>
## Practical Lab 14 - Complete Access-Control Scenario

* **Objective:** Design, deploy, and validate an end-to-end access-controlled file sharing environment combining Active Directory security groups, Share permissions, and NTFS permissions following the Principle of Least Privilege.
* **Related Concept:** [08 - Shared Folders](08%20-%20Shared%20Folders/README.md) and [07 - NTFS Permissions](07%20-%20NTFS%20Permissions/README.md)
* **Target Machines:** `DC01` (Domain Controller / File Server) and `CLIENT01` (Network Client)
* **Domain:** `soclab.local`

---

### Design Plan: Directory Structure & Access Requirements

I established an enterprise SOC departmental share structure on DC01:

```text
C:\SOC-AccessLab
|-- Analyst
|   `-- Analyst-Report.txt
|-- Manager
|   `-- Manager-Report.txt
`-- Admin
    `-- Admin-Report.txt
```

**Access Control Requirements:**
* **SOC Analysts (`SOC-Analysts`):** Must have Read & Execute access to view reports and operational documents. Must not modify, create, or delete files.
* **SOC Managers (`SOC-Managers`):** Must have Modify access to create, update, and delete departmental files. Must not alter folder security permissions.
* **SOC Administrators (`SOC-Admins`):** Must have Full Control to manage all files, folders, ownership, and Access Control Lists.

---

### Task 01 - Verify Domain Security Groups

I verified that the three domain security groups were active in `soclab.local`:
* `SOC-Analysts` (Member: `SOC Analyst1`)
* `SOC-Managers` (Member: `SOC Manager1`)
* `SOC-Admins` (Member: Domain Administrator account)

---

### Task 02 - Build Folder Structure and Configure NTFS Permissions

1. On **DC01**, I created `C:\SOC-AccessLab` along with the `Analyst`, `Manager`, and `Admin` subdirectories and test text files.

![Directory Structure Created](Screenshots/90%20-%20Tree.png)

2. I right-clicked `C:\SOC-AccessLab`, opened **Properties -> Security**, and clicked **Edit**.
3. I added each group and configured the NTFS permissions:

| Group | NTFS Permission Assigned | Effective Capability |
| :--- | :--- | :--- |
| **SOC-Analysts** | Read & Execute | Read folder contents, view files, execute scripts. |
| **SOC-Managers** | Modify | Read, write, create, edit, and delete files and subfolders. |
| **SOC-Admins** | Full Control | Complete administrative authority, including taking ownership and changing ACLs. |

![NTFS Permissions Configured for All Three Groups](Screenshots/91%20-%20Permission%20set%20.png)

Because inheritance was enabled, these permissions automatically propagated down to the `Analyst`, `Manager`, and `Admin` subfolders.

---

### Task 03 - Share the Master Folder (Enterprise Best Practice)

To avoid the Share-level bottleneck encountered in Lab 11, I applied the recommended enterprise design pattern:

1. On **DC01**, I right-clicked `C:\SOC-AccessLab` -> **Properties -> Sharing -> Advanced Sharing**.
2. I checked **Share this folder** and named the share `SOC-AccessLab`.
3. I clicked **Permissions**.
4. I set the `Everyone` group to **Full Control**.
5. I clicked **Apply** and **OK**.

![Share Permission Configured to Full Control](Screenshots/92%20-%20Share%20set.png)

**Design Rationale:**
By setting Share permissions to Full Control, the network "front door" imposes no artificial bottleneck. All access enforcement is handed off entirely to the granular NTFS Access Control List (The Vault).

---

### Task 04 - Validate Analyst Access from CLIENT01

I logged into **CLIENT01** as `soclab\SOC Analyst1` and connected to `\\WIN-DEF8VDFQ099\SOC-AccessLab`:

1. **Open and Read:** Success. I opened folders and read the contents of `Analyst-Report.txt`.
2. **Create New File:** Failed (`Access is denied`).
3. **Modify Existing File:** Failed (`Access is denied` on save).
4. **Delete File:** Failed (`File Access Denied`).

![Analyst Blocked from Deleting Files](Screenshots/93%20-%20Delete%20errors.png)

**Result:** The analyst account strictly satisfied the Read & Execute constraint.

---

### Task 05 - Validate Manager Access from CLIENT01

I logged out of CLIENT01 and logged back in as `soclab\SOC Manager1`:

1. I connected to `\\WIN-DEF8VDFQ099\SOC-AccessLab`.
2. **Open and Read:** Success.
3. **Create New File:** Success. The manager could create files and subfolders.
4. **Modify Existing File:** Success. Edits were saved directly to the network share.
5. **Delete File:** Success. Files were deleted without restriction.
6. **Change ACL Permissions:** Failed (`Access is denied`). When attempting to edit the **Security** tab to add or remove users, Windows blocked the action.

![Manager Blocked from Modifying Security ACLs](Screenshots/95%20-%20Manager%20Errors.png)

**Result:** The manager account possessed full operational file rights (Modify) but could not tamper with security boundaries.

---

### Task 06 - Validate Administrator Access from CLIENT01

Finally, I logged into CLIENT01 using an administrative account belonging to `SOC-Admins`:

1. I connected to `\\WIN-DEF8VDFQ099\SOC-AccessLab`.
2. **File Operations (Read, Create, Modify, Delete):** All succeeded without restriction.
3. **Change Security Permissions:** Success. The administrator successfully modified the Access Control List on the **Security** tab.

**Result:** The administrative account had full operational and governance control.

---

### Final Validated Access Matrix

The table below summarizes the verified access levels tested across all three tiers:

| Account / Group | Read Files | Modify Files | Delete Files | Modify Security ACLs | Effective Security Tier |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **SOC Analyst1** (`SOC-Analysts`) | Allowed | Denied | Denied | Denied | Read-Only Triage |
| **SOC Manager1** (`SOC-Managers`) | Allowed | Allowed | Allowed | Denied | Operational Contributor |
| **Admin Account** (`SOC-Admins`) | Allowed | Allowed | Allowed | Allowed | Full Security Administrator |

---

### What This Teaches for SOC Work

1. **Principle of Least Privilege:** Users should only possess the minimum permissions necessary to perform their legitimate job functions. Over-privileged accounts represent a critical security vulnerability. If an analyst workstation is compromised, an attacker cannot wipe or tamper with shared organizational files.
2. **Access Control Integrity:** Granular NTFS controls combined with open share permissions represent the standard enterprise architecture for file services. SOC analysts investigating unauthorized file modifications or deletions can quickly correlate user SID, group membership, and NTFS ACLs.
3. **Privilege Escalation Detection:** Any attempt by non-admin users to modify security permissions (generating Event ID 4670 - Permissions on an object were changed) is a significant indicator of compromise (IoC) warranting immediate SOC investigation.

---

## Lab Exercise Summary

Across these 14 practical labs, I built, configured, administered, and verified a complete Windows Server and Active Directory lab environment:

1. **Server Management:** Deployed Windows Server 2022 Standard (Desktop Experience), configured server identity (`DC01`, `192.168.10.10`), and navigated Server Manager.
2. **Roles and Features:** Installed Active Directory Domain Services (AD DS) and DNS Server roles, and promoted the server to the domain controller for `soclab.local`.
3. **System Administration:** Managed local and domain resources via Computer Management (`compmgmt.msc`), configured Windows Services, and analyzed service dependencies.
4. **Active Directory Identity:** Built an organized Organizational Unit (OU) hierarchy, created domain user accounts, created security groups, and managed group memberships.
5. **File System Security:** Mastered NTFS permissions (inheritance, explicit rights, deny overrides) and Share permissions (front-door network controls).
6. **Network File Sharing:** Implemented enterprise network shares (`SOC-Reports`, `SOC-AccessLab`), analyzed the Effective Permission Trap, documented hidden shares (`SOC-Secret$`), and validated least privilege across multiple security tiers from a client workstation (`CLIENT01`).

---

[<- Back to Windows Server Fundamentals](README.md) | [Back to Main Repository Hub](../README.md)