# Windows Services - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../02%20-%20Windows%20Server%20Fundamentals/05%20-%20Windows%20Services/README.md) | [Related Lab: Explore and Manage Services](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-06) | [Key Terms](../../Key%20Terms/Windows%20Server%20Fundamentals/README.md#5-windows-services-architecture)

---

## Basic

### 1. What is a Windows Service, and how does it differ from a standard desktop application?

**Answer:**
A Windows Service is a long-running background executable managed by the Windows Service Control Manager (SCM). Unlike standard desktop applications, a service:
1. Starts automatically before any user logs in and continues running after users log out.
2. Does not present an interactive graphical user interface (GUI).
3. Executes under dedicated system identities (such as `Local System`, `Network Service`, or custom service accounts).

### 2. What is the difference between Service Status and Startup Type?

**Answer:**
- **Service Status:** Reflects the *current real-time operational state* of the service in memory (Running, Stopped, Paused). Answers: *"Is this process executing right now?"*
- **Startup Type:** The *configuration setting* dictating how Windows handles the service during boot (Automatic, Automatic Delayed, Manual, Disabled). Answers: *"What will Windows do with this service during the next reboot?"*

---

## Intermediate

### 3. What is a Service Dependency, and what happens if a root dependency fails?

**Answer:**
A Service Dependency is an architectural requirement where a service relies on other underlying services to initialize before it can operate. For example, the **Print Spooler** service depends on the **HTTP Service** and **Remote Procedure Call (RPC)**. If RPC is stopped or fails to initialize, the Print Spooler immediately fails to start.

### 4. What are the security risks associated with services running under the `Local System` (`NT AUTHORITY\SYSTEM`) account?

**Answer:**
The `Local System` account possesses complete, unrestricted administrative privileges on the local host operating system. If an attacker identifies a vulnerability (e.g., unquoted service path, DLL hijacking, or remote code execution) in a service running under `Local System`, they immediately gain full SYSTEM-level execution, achieving complete local machine takeover.

---

## Scenario-Based

### 5. An administrator manually clicks "Stop" on the Print Spooler service. What happens to the service when the server is restarted next week?

**Answer:**
When the server restarts, Windows evaluates the configured **Startup Type**. Because stopping a service only changes its real-time *Status* (from Running to Stopped) and does not modify its *Startup Type* (which remained configured as `Automatic`), Windows will automatically start the Print Spooler service upon reboot. To permanently prevent it from running, the administrator must change its Startup Type to `Disabled`.

### 6. How do threat actors abuse Windows Services for persistence and privilege escalation, and how do SOC analysts detect it?

**Answer:**
- **Abuse Techniques:**
  1. **New Service Creation (MITRE ATT&CK T1543.003):** Tools like PsExec or malware deploy malicious executables as new services running under `SYSTEM`.
  2. **Service Binary Path Modification:** Replacing or altering the `ImagePath` registry key of a legitimate service to point to an attacker's payload.
- **SOC Detection:**
  - Windows Security Event ID **7045** ("A new service was installed in the system"), monitoring the Service Name, Service File Name, and Service Account.
  - Windows System Event ID **7036** (Service state change).
  - Sysmon Event ID **1** (Process Creation of `sc.exe`, `net.exe`, or PowerShell `New-Service`).

---

## Navigation

- [Previous: 04 - Computer Management](04%20-%20Computer%20Management.md)
- [Back to Windows Server Interview Hub](README.md)
- [Next: 06 - Local Users and Groups](06%20-%20Local%20Users%20and%20Groups.md)
