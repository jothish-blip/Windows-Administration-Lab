# Windows Server Editions - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../02%20-%20Windows%20Server%20Fundamentals/01%20-%20Windows%20Server%20Editions/README.md) | [Related Labs: Lab 01 & Lab 02](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-01) | [Key Terms](../../Key%20Terms/Windows%20Server%20Fundamentals/README.md#1-server-editions-and-licensing)

---

## Basic

### 1. What are the primary editions of Windows Server, and how do they differ?

**Answer:**
- **Standard Edition:** Designed for physical servers or lightly virtualized environments. Includes licensing rights to run up to 2 virtual machines or Hyper-V containers.
- **Datacenter Edition:** Designed for enterprise data centers and highly virtualized cloud environments. Grants rights to run unlimited virtual machines on licensed physical cores, plus advanced features like Shielded VMs and Storage Spaces Direct.
- **Essentials Edition:** Sized for small businesses with up to 25 users and 50 devices, without requiring separate CAL purchases.
- **Evaluation Edition:** A full-featured 180-day trial edition provided by Microsoft for testing and training.

### 2. How can an administrator verify the exact Windows Server edition, build, and version from the command line?

**Answer:**
- Running `winver` opens the graphical Windows Version dialog showing OS edition and build number.
- Running `systeminfo` outputs detailed operating system metadata, kernel version, hotfix list, physical RAM, network cards, and domain membership.

---

## Intermediate

### 3. How does Microsoft's core-based licensing model work for Windows Server?

**Answer:**
Microsoft licenses Windows Server Standard and Datacenter based on physical processor cores rather than physical CPU sockets:
1. Every physical processor must be licensed for a minimum of 8 cores.
2. Every physical server must be licensed for a minimum of 16 cores (even if the server only possesses 8 total cores).
3. In addition to core licenses, organizations must purchase Client Access Licenses (CALs) for each user or device connecting to the server.

### 4. What are Virtualization Rights in Windows Server Standard vs Datacenter?

**Answer:**
- **Standard Edition:** Licensing all physical cores on a host grants rights to run **2 virtual instances** of Windows Server. If the organization wishes to run 4 VMs on that same physical server, they must "stack" or re-license all physical cores again.
- **Datacenter Edition:** Licensing all physical cores on a host grants rights to run an **unlimited number of virtual instances** of Windows Server on that licensed host without buying additional VM operating system licenses.

---

## Scenario-Based

### 5. An enterprise plans to deploy a single physical server hosting 24 virtualized Windows Server instances. Which edition should they purchase, and why?

**Answer:**
They should purchase **Windows Server Datacenter Edition**. 
If they chose Standard Edition, they would have to license all physical cores 12 times over (since each full license only covers 2 VMs). Stacking Standard licenses 12 times is far more expensive, administratively complex, and difficult to audit than purchasing a single Datacenter core license that grants unlimited virtual machines.

### 6. During a SOC incident triage on an unfamiliar Windows Server, an analyst runs `systeminfo` and observes that the OS Version is `10.0.14393` and the Domain is `WORKGROUP`. What does this indicate to the analyst?

**Answer:**
- Build `14393` corresponds to **Windows Server 2016**.
- `WORKGROUP` indicates the server is an unmanaged standalone or perimeter server (DMZ), not joined to Active Directory.
- To the analyst: The system relies strictly on its local SAM database for user authentication, cannot receive domain Group Policies, and may be a perimeter bastion host or unmanaged shadow IT asset requiring isolated credential investigation.

---

## Navigation

- [Back to Windows Server Interview Hub](README.md)
- [Study Concept: Server Editions](../../02%20-%20Windows%20Server%20Fundamentals/01%20-%20Windows%20Server%20Editions/README.md)
- [Next Concept Questions: 02 - Server Manager](02%20-%20Server%20Manager.md)
