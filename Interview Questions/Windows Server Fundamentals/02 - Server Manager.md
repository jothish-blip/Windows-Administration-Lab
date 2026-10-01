# Server Manager - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../02%20-%20Windows%20Server%20Fundamentals/02%20-%20Server%20Manager/README.md) | [Related Lab: Explore Server Manager](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-03) | [Key Terms](../../Key%20Terms/Windows%20Server%20Fundamentals/README.md#2-server-management-and-dashboards)

---

## Basic

### 1. What is Server Manager in Windows Server?

**Answer:**
Server Manager is the centralized administration console in Windows Server. It provides an operational overview of the server, displays status and alerts for installed roles, enables role and feature installation/removal, and serves as a unified launchpad for administrative tools (ADUC, DNS Manager, Event Viewer, Services).

### 2. What essential configuration properties are displayed in the "Local Server" view?

**Answer:**
- Computer name (hostname) and workgroup/domain membership
- Windows Defender Firewall profiles (Domain, Private, Public)
- Remote Management (WinRM) and Remote Desktop (RDP) operational states
- Network interface card properties (IP address, IPv6, DHCP status)
- Last installed Windows Update timestamp and update settings
- Hardware overview (installed physical RAM, processor model)
- System time zone and product licensing activation status

---

## Intermediate

### 3. What is the Best Practices Analyzer (BPA) inside Server Manager?

**Answer:**
The Best Practices Analyzer is a diagnostic tool built into Server Manager that scans installed server roles (such as AD DS, DNS, Hyper-V) against Microsoft's recommended configuration guidelines. It reports operational issues categorized into Information, Warnings, and Errors, providing specific remediation steps to optimize performance, scalability, and security.

### 4. How can Server Manager be used to manage multiple remote servers simultaneously?

**Answer:**
Under the **Manage** menu, an administrator can select **Add Servers** to query Active Directory or DNS and add remote Windows Server instances to the console pool. Once added, the administrator can view events, check service statuses, and deploy roles and features across remote servers from a single dashboard using Windows Remote Management (WinRM).

---

## Scenario-Based

### 5. An administrator opens Server Manager and notices the Notification Flag has turned red. What does this mean and how should they proceed?

**Answer:**
A red notification flag indicates that a deployment, background task, or role health check has failed or requires post-installation administrative action (e.g., AD DS was installed, but the server has not yet been promoted to a Domain Controller). The administrator should click the flag icon, inspect the detailed task message, and follow the link to complete or troubleshoot the pending configuration.

### 6. Why is managing servers through Remote Desktop (RDP) directly to the desktop generally discouraged in enterprise production environments?

**Answer:**
1. **Interactive Session Overhead:** Logging into GUI desktops consumes CPU and RAM on production servers.
2. **Credential Theft Risk:** Logging onto servers via interactive RDP leaves cleartext credentials or Kerberos tickets in LSASS memory, exposing them to attackers using tools like Mimikatz (MITRE ATT&CK T1003.001).
3. **Enterprise Alternative:** Administrators should manage servers remotely using Server Manager, Remote Server Administration Tools (RSAT), or PowerShell Remoting (WinRM) from a hardened administrative workstation.

---

## Navigation

- [Previous: 01 - Server Editions](01%20-%20Windows%20Server%20Editions.md)
- [Back to Windows Server Interview Hub](README.md)
- [Next: 03 - Roles vs Features](03%20-%20Roles%20vs%20Features.md)
