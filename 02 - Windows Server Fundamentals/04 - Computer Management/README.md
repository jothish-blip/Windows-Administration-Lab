# Computer Management

## 1. What is Computer Management?

**Computer Management** is a Windows administrative console that provides a centralized interface for managing and troubleshooting different parts of a Windows computer or server.

Rather than forcing an administrator to open several independent management tools separately, Computer Management groups related tools into a single, unified window.

The overall relationship can be represented as:

```text
                    COMPUTER MANAGEMENT
                           │
          ┌────────────────┼────────────────┐
          │                │                │
    System Tools        Storage         Services
          │                │                │
    ┌─────┼─────┐          │                │
    ↓     ↓     ↓          ↓                ↓
 Events Shared Users/     Disk           Services
        Folders Groups  Management
        Device Manager

```

**Key Concept:** Computer Management is a *container* for administrative tools. It is not a service itself (like DNS or DHCP), but rather a way to access the tools that manage those services and the server's hardware.

## 2. Accessing the Console

On a Windows Server environment (like DC01), Computer Management can be accessed through several paths:

* **Server Manager:** `Tools → Computer Management`
* **Start Menu:** `Start → Windows Tools → Computer Management`
* **Run Dialog:** `Win + R → compmgmt.msc`

*For centralized administration, accessing it via Server Manager is the standard workflow.*

## 3. The Three Major Areas

When the console opens, the navigation pane on the left is divided into three primary categories:

![Computer Management](<../Screenshots/18 - Computer Management.png>)

1. **System Tools:** Utilities for managing events, shares, local users, and hardware.
2. **Storage:** Utilities for managing disks and file systems.
3. **Services and Applications:** Utilities for managing background services and installed applications.

---

## 4. System Tools

The System Tools section contains several critical utilities for day-to-day Windows administration.

### Event Viewer

Event Viewer is a Windows tool used to view and analyze events recorded by the operating system and applications. Windows constantly generates events for actions like user logons, service starts, or application crashes.

![Windows Event Viewer](<../Screenshots/19 - Event Viewer.png>)

**Windows Logs:**
* **Application:** Events logged by software/applications running on the server.
* **Security:** Events related to resource use, logons, and security policies. (Critical for SOC investigations).
* **Setup:** Events related to application and Windows installation.
* **System:** Events logged by Windows operating system components.
* **Forwarded Events:** Events collected from other computers on the network.


### Shared Folders

This section manages folders that are shared over the network (e.g., `\\DC01\SharedFolder`). It provides real-time visibility into network sharing activity.

![Shared Folders](<../Screenshots/20 - Shared Folders.png>)

* **Shares:** Displays all folders/resources currently being shared from the computer.
* **Sessions:** Shows remote computers or users that currently have active network sessions connected to the server.
* **Open Files:** Displays specific files that are currently locked/opened by users across the network.

### Local Users and Groups

This tool manages local accounts and local security groups residing directly on the machine.

* **Users:** Individual local user accounts (e.g., Administrator, Guest).
* **Groups:** Collections of users used to assign permissions efficiently (e.g., Administrators, Users, Backup Operators).

**Important Distinction for Domain Controllers:**
Because DC01 is a Domain Controller, its primary identity management happens in Active Directory. "Local Users and Groups" manages accounts specific to *this individual computer*, whereas Active Directory manages accounts for the entire domain.

### Device Manager

Device Manager displays and manages the hardware devices recognized by Windows (Network adapters, Display adapters, Disk drives, Processors).

![Device Manager](<../Screenshots/21 - Device Manager.png>)

*Note on Virtualization:* In a lab environment, the hardware displayed here is virtualized hardware presented to Windows by the hypervisor (e.g., VirtualBox). Administrators use this tool to check device health, update drivers, and troubleshoot hardware errors.

---

## 5. Storage

### Disk Management

Disk Management is a crucial tool that allows administrators to manage storage devices, partitions, and volumes.

![alt text](<../Screenshots/22 - Disk Management.png>)

It provides detailed information about:

* **Physical disks:** The actual drives attached to the system (Disk 0, Disk 1).
* **Partitions & Volumes:** How the disks are divided (e.g., System/Boot partition, C: drive).
* **File systems:** The format of the drives (typically NTFS or ReFS on Windows Server).
* **Unallocated space:** Storage capacity that has not yet been formatted or assigned to a volume.

Administrators use Disk Management to initialize new drives, extend existing volumes when they run out of space, format partitions, and assign drive letters.

---

## 6. Services and Applications

### Services

A **Windows Service** is a background program or component that performs a specific function without requiring a user to interact with it continuously. Examples include the DNS Server service, DHCP Server service, Windows Update, and the Event Log service.

![Services](<../Screenshots/23 - Services.png>)

When managing services, there are two distinct concepts to understand:

**1. Service State (Current Activity)**
What is the service doing *right now*?

* **Running:** The service is currently active and performing its job.
* **Stopped:** The service is not currently active.

**2. Startup Type (Configuration)**
What should Windows do with this service when the system boots?

* **Automatic:** Windows starts the service automatically during boot.
* **Automatic (Delayed Start):** Starts automatically, but waits until shortly after boot to improve startup performance.
* **Manual:** The service only starts when triggered by a user, an application, or another service.
* **Disabled:** The service is prevented from starting entirely.

### SOC Relevance

Understanding services is fundamental for security operations. If an unexpected service appears, or an unknown executable begins running as a background service, an analyst will use these tools in conjunction with Event Viewer to investigate suspicious behavior.

---

## 7. The Big Picture

Microsoft groups all these tools inside **Computer Management** to provide a cohesive, single-pane-of-glass administrative experience.

Instead of an administrator needing to memorize separate executable names or dig through the Control Panel to check a disk, restart a service, investigate an error log, and check a hardware driver, Computer Management organizes the complete underlying architecture of a single machine into one logical hierarchy.