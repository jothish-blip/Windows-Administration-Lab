# Windows Administration Lab

## Overview

The **Windows Administration Lab** documents my hands-on learning journey and practical lab work in building and managing a Windows enterprise environment for Security Operations Center (SOC) Analyst preparation.

Rather than relying purely on theoretical cybersecurity concepts, I built a multi-system enterprise lab from scratch inside Oracle VirtualBox. The lab consists of a Windows Server 2022 Domain Controller (`DC01`) and a Windows 11 client machine (`CLIENT01`) communicating across an isolated private network (`SOC-LAB`) under the Active Directory domain `soclab.local`.

This repository serves as my technical lab journal and reference manual. It combines conceptual architecture notes, step-by-step configuration workflows, actual command outputs, real troubleshooting experiences, 106 verified screenshots documenting my practical work, dedicated key terminology glossaries, and tiered technical interview preparation.

---

## Learning Architecture: 4-Pillar Educational Framework

The repository is built around a structured 4-pillar learning methodology designed to reinforce theoretical knowledge through practical execution and interview-ready technical articulation:

```text
Study Concept  ──>  Summary  ──>  Practical Lab  ──>  Key Terms  ──>  Interview Questions
```

1. **Study Concepts:** In-depth technical guides covering operating system architecture, identity management, access control lists, networking models, and enterprise virtualization.
2. **Summaries:** High-yield executive summaries at the conclusion of every concept page highlighting core lessons learned for rapid revision.
3. **Practical Labs:** 14 step-by-step lab exercises executed on live virtual machines with command line syntax, UI configuration steps, 106 verified screenshot artifacts, and SOC defensive takeaways.
4. **Key Terms:** Dedicated glossaries defining industry-standard terminology, core mechanisms, and practical security context.
5. **Interview Questions:** Dedicated interview preparation modules tiered into Basic, Intermediate, and Scenario-based technical questions with concise, technically accurate answers.

---

## Learning Tracks & Repository Layout

The repository is organized into two primary technical tracks supported by centralized reference modules:

```text
Windows-Administration-Lab
│
├── 01 - Virtualization/
│   ├── Concepts: Hypervisors, VirtualBox Networking, Snapshots, Topology
│   └── Hands-On Build: 4-Step Lab Provisioning & Verification Guides
│
├── 02 - Windows Server Fundamentals/
│   ├── Concepts: Editions, Server Manager, Roles/Features, Services, ADUC, NTFS, Shares
│   └── Hands-On Labs: 14 Practical Exercises with Verified Screenshots
│
├── Key Terms/
│   ├── Virtualization Fundamentals (Glossary of core virtualization terms)
│   └── Windows Server Fundamentals (Glossary of core server & identity terms)
│
└── Interview Questions/
    ├── Virtualization Fundamentals (Tiered Q&A by virtualization concept)
    └── Windows Server Fundamentals (Tiered Q&A by Windows Server concept)
```

---

## Lab Architecture & Environment

```text
                     Host Computer (Physical Hardware)
                                     │
                     Oracle VirtualBox (Type 2 Hypervisor)
                                     │
         ┌───────────────────────────┴───────────────────────────┐
         │                                                       │
         ▼                                                       ▼
+-----------------------------------+   Internal Network    +-----------------------------------+
|               DC01                |       (SOC-LAB)       |             CLIENT01              |
|   Windows Server 2022 Std Eval    | <───────────────────> |            Windows 11             |
|        Domain Controller          |                       |         Domain-Joined Client      |
|           192.168.10.10           |                       |            192.168.10.20          |
+-----------------------------------+                       +-----------------------------------+
```

### Environment Specifications

| Component | Specification | Description |
|-----------|---------------|-------------|
| **Hypervisor** | Oracle VirtualBox 7.x | Type 2 hosted hypervisor running on physical host |
| **Server VM (`DC01`)** | Windows Server 2022 Standard Evaluation (Build 20348) | Domain Controller for `soclab.local`, DNS Server, File Server |
| **Server Hardware Sizing** | 4096 MB RAM, 2 vCPUs, 80 GB VDI Storage | Static IP `192.168.10.10/24`, Preferred DNS `192.168.10.10` |
| **Client VM (`CLIENT01`)** | Windows 11 | Domain-joined client workstation |
| **Client Hardware Sizing** | 4096 MB RAM, 2 vCPUs, 60 GB VDI Storage | Static IP `192.168.10.20/24`, Preferred DNS `192.168.10.10` |
| **Virtual Network** | Internal Network (`SOC-LAB`) | Fully isolated from host and external internet |
| **Domain** | `soclab.local` | Centralized identity and directory service namespace |

---

## Repository Structure

### Track 1: Virtualization Fundamentals

The [Virtualization Fundamentals](01%20-%20Virtualization/README.md) track covers the foundational technologies required to build and isolate a virtual enterprise network:

| Module / Guide | Focus Area | Concept Guide | Key Terms | Interview Questions |
|---|---|:---:|:---:|:---:|
| **Virtualization Overview** | Central hub for virtualization concepts, architecture, and navigation | [View Hub](01%20-%20Virtualization/README.md) | [Key Terms](Key%20Terms/Virtualization%20Fundamentals/README.md) | [Interview Hub](Interview%20Questions/Virtualization%20Fundamentals/README.md) |
| **Core Concepts** | VM components, hypervisor responsibilities, benefits, physical vs. virtual | [Read Guide](01%20-%20Virtualization/Virtualization.md) | [Section 1](Key%20Terms/Virtualization%20Fundamentals/README.md#1-core-virtualization) | [Q&A Guide](Interview%20Questions/Virtualization%20Fundamentals/01%20-%20Virtualization.md) |
| **01 - VirtualBox Networking** | NAT, Internal Network, Host-Only modes, traffic flow, selection criteria | [Read Guide](01%20-%20Virtualization/01%20-%20VirtualBox%20Networking/README.md) | [Section 3](Key%20Terms/Virtualization%20Fundamentals/README.md#3-virtual-machine-networking) | [Q&A Guide](Interview%20Questions/Virtualization%20Fundamentals/02%20-%20VirtualBox%20Networking.md) |
| **02 - Hypervisors** | Type 1 (Bare-Metal) vs. Type 2 (Hosted), ESXi, Hyper-V, VirtualBox | [Read Guide](01%20-%20Virtualization/02%20-%20Hypervisor/README.md) | [Section 2](Key%20Terms/Virtualization%20Fundamentals/README.md#2-hypervisors) | [Q&A Guide](Interview%20Questions/Virtualization%20Fundamentals/03%20-%20Hypervisors.md) |
| **03 - Snapshots** | Point-in-time VM saved states, rollback workflows, snapshots vs. backups | [Read Guide](01%20-%20Virtualization/03%20-%20Snapshots/README.md) | [Section 4](Key%20Terms/Virtualization%20Fundamentals/README.md#4-snapshots-and-state-management) | [Q&A Guide](Interview%20Questions/Virtualization%20Fundamentals/04%20-%20Snapshots.md) |
| **04 - Lab Architecture** | Small enterprise network design, Domain Controller and Client interaction | [Read Guide](01%20-%20Virtualization/04%20-%20Lab%20Architecture/README.md) | [Section 5](Key%20Terms/Virtualization%20Fundamentals/README.md#5-lab-architecture-and-infrastructure) | [Q&A Guide](Interview%20Questions/Virtualization%20Fundamentals/05%20-%20Lab%20Architecture.md) |
| **05 - Lab Setup Overview** | End-to-end build roadmap, hardware sizing, deployment prerequisites | [Read Guide](01%20-%20Virtualization/05%20-%20Lab%20Setup/README.md) | - | - |
| ↳ *Step 01: Install VirtualBox* | Installing the hypervisor on the physical host and verifying drivers | [Setup Step 1](01%20-%20Virtualization/05%20-%20Lab%20Setup/01%20-%20Install%20VirtualBox.md) | - | - |
| ↳ *Step 02: Create & Configure VMs* | Sizing and provisioning `DC01` and `CLIENT01`, attaching installation ISOs | [Setup Step 2](01%20-%20Virtualization/05%20-%20Lab%20Setup/02%20-%20Create%20and%20Configure%20Virtual%20Machines.md) | - | - |
| ↳ *Step 03: Configure Networking* | Setting the `SOC-LAB` internal network and assigning deterministic static IPs | [Setup Step 3](01%20-%20Virtualization/05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md) | - | - |
| ↳ *Step 04: Verify Connectivity* | Verifying IP parameters, testing bidirectional ICMP ping, capturing baseline snapshots | [Setup Step 4](01%20-%20Virtualization/05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md) | - | - |

---

### Track 2: Windows Server Fundamentals

The [Windows Server Fundamentals](02%20-%20Windows%20Server%20Fundamentals/README.md) track covers operating system administration, identity management, permissions, and network file sharing across eight conceptual modules, fourteen hands-on labs, key terminology, and interview preparation:

| Module | Conceptual Topic | Hands-On Practical Lab | Key Terms | Interview Questions |
|---|---|:---:|:---:|:---:|
| **Track Overview** | Central hub for Windows Server modules, lab index, and concepts mapping | [View Hub](02%20-%20Windows%20Server%20Fundamentals/README.md) | [Key Terms](Key%20Terms/Windows%20Server%20Fundamentals/README.md) | [Interview Hub](Interview%20Questions/Windows%20Server%20Fundamentals/README.md) |
| **01 - Editions & Licensing** | Standard, Datacenter, Essentials, core licensing, CALs, virtualization rights | [Lab 01 & Lab 02](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-01) | [Section 1](Key%20Terms/Windows%20Server%20Fundamentals/README.md#1-server-editions-and-licensing) | [Q&A Guide](Interview%20Questions/Windows%20Server%20Fundamentals/01%20-%20Windows%20Server%20Editions.md) |
| **02 - Server Manager** | Centralized dashboard, Local Server properties, Manage, Tools, BPA | [Lab 03](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-03) | [Section 2](Key%20Terms/Windows%20Server%20Fundamentals/README.md#2-server-management-and-dashboards) | [Q&A Guide](Interview%20Questions/Windows%20Server%20Fundamentals/02%20-%20Server%20Manager.md) |
| **03 - Roles vs. Features** | Major server responsibilities vs. supporting capabilities, Add Roles Wizard | [Lab 04](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-04) | [Section 3](Key%20Terms/Windows%20Server%20Fundamentals/README.md#3-roles-and-features) | [Q&A Guide](Interview%20Questions/Windows%20Server%20Fundamentals/03%20-%20Roles%20vs%20Features.md) |
| **04 - Computer Management** | System Tools, Event Viewer logs, Device Manager, Disk Management | [Lab 05](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-05) | [Section 4](Key%20Terms/Windows%20Server%20Fundamentals/README.md#4-system-administration-and-consoles) | [Q&A Guide](Interview%20Questions/Windows%20Server%20Fundamentals/04%20-%20Computer%20Management.md) |
| **05 - Windows Services** | Real-time Status vs. Startup Type, dependencies, service lifecycle, SOC context | [Lab 06](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-06) | [Section 5](Key%20Terms/Windows%20Server%20Fundamentals/README.md#5-windows-services-architecture) | [Q&A Guide](Interview%20Questions/Windows%20Server%20Fundamentals/05%20-%20Windows%20Services.md) |
| **06 - Local Users & Groups** | Authentication vs. Authorization, SAM vs. ADUC, Principle of Least Privilege | [Lab 07 & Lab 08](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-07) | [Section 6](Key%20Terms/Windows%20Server%20Fundamentals/README.md#6-identity-users-and-groups) | [Q&A Guide](Interview%20Questions/Windows%20Server%20Fundamentals/06%20-%20Local%20Users%20and%20Groups.md) |
| **07 - NTFS Permissions** | Standard permissions, ACLs/ACEs, explicit vs. inherited rules, Allow vs. Deny | [Lab 09 & Lab 10](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-09) | [Section 7](Key%20Terms/Windows%20Server%20Fundamentals/README.md#7-ntfs-file-system-security) | [Q&A Guide](Interview%20Questions/Windows%20Server%20Fundamentals/07%20-%20NTFS%20Permissions.md) |
| **08 - Shared Folders** | UNC paths, Share vs. NTFS permissions, effective access overlap, hidden shares | [Labs 11 - 14](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-11) | [Section 8](Key%20Terms/Windows%20Server%20Fundamentals/README.md#8-network-file-sharing-and-smb) | [Q&A Guide](Interview%20Questions/Windows%20Server%20Fundamentals/08%20-%20Shared%20Folders.md) |

---

## Practical Labs Summary

All fourteen hands-on exercises are fully documented in [`02 - Windows Server Fundamentals/Lab-Exercise.md`](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md):

1. **[Practical Lab 01](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-01):** To Know the Windows Server Edition (`winver` on `DC01`)
2. **[Practical Lab 02](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-02):** To Know Detailed Information About the System (`systeminfo` on `DC01`)
3. **[Practical Lab 03](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-03):** Explore the Server Manager (Dashboard, Local Server, Manage, Tools, Notifications)
4. **[Practical Lab 04](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-04):** Explore Roles and Features (Add Roles and Features Wizard exploration)
5. **[Practical Lab 05](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-05):** Explore Computer Management (Event Viewer, Shares, Device Manager, Disk Management)
6. **[Practical Lab 06](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-06):** Explore and Manage Windows Services (Print Spooler testing, dependencies HTTP/RPC)
7. **[Practical Lab 07](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-07):** Manage Domain Users in Active Directory (ADUC `dsa.msc`, `SOC` OU, account lifecycle)
8. **[Practical Lab 08](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-08):** Manage Security Groups (Creating `SOC-Admins`, group-based permission mapping)
9. **[Practical Lab 09](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-09):** Configure NTFS Permissions (`C:\SOC-Lab\Reports`, ACL configuration)
10. **[Practical Lab 10](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-10):** NTFS Permission Scenarios (Testing Read/Modify/Delete, inheritance, explicit rules)
11. **[Practical Lab 11](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-11):** Create and Access a Network Shared Folder (Network UNC access from `CLIENT01`)
12. **[Practical Lab 12](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-12):** Share + NTFS Permission Scenarios (Effective permission analysis, most restrictive rule)
13. **[Practical Lab 13](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-13):** Hidden Shares & Administrative Shares (`SOC-Secret$`, `C$`, `ADMIN$`, `IPC$`)
14. **[Practical Lab 14](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-14):** Complete Access-Control Scenario (End-to-end `C:\SOC-AccessLab` multi-tier validation)

---

## Dedicated Learning Sections

### Key Terms Glossaries

The [Key Terms Directory](Key%20Terms/README.md) provides centralized terminology glossaries connecting academic definitions with real-world SOC defensive applications:

- **[Virtualization Key Terms](Key%20Terms/Virtualization%20Fundamentals/README.md):** Hypervisors, virtual hardware abstraction, host-only vs. internal networks, differencing disks, and rollback mechanisms.
- **[Windows Server Key Terms](Key%20Terms/Windows%20Server%20Fundamentals/README.md):** Operating system editions, CAL licensing, MMC architecture, SCM service control, security identifiers (SIDs), access control entries (ACEs), DACLs, and SMB network shares.

### Technical Interview Preparation

The [Interview Questions Directory](Interview%20Questions/README.md) contains structured technical questions tiered into Basic, Intermediate, and Scenario-based categories:

- **[Virtualization Fundamentals Interview Questions](Interview%20Questions/Virtualization%20Fundamentals/README.md):** 5 concept modules covering virtualization benefits, network isolation, hypervisor architecture, snapshot differencing, and lab topology.
- **[Windows Server Fundamentals Interview Questions](Interview%20Questions/Windows%20Server%20Fundamentals/README.md):** 8 concept modules covering edition selection, remote management with WinRM, role service attack surfaces, service persistence, security group nesting, NTFS inheritance rules, and effective SMB access resolution.

---

## What This Teaches for SOC Analyst Work

This repository connects routine Windows system administration to the defensive responsibilities of a SOC Analyst:

- **Persistence Analysis:** Adversaries frequently establish persistence via malicious Windows services, scheduled tasks, or hidden network shares. Understanding baseline system services and startup types is necessary to spot deviations.
- **Log Correlation:** Windows Event Viewer categorizes security-relevant events (`Security`, `System`, `Application`). Hands-on familiarity with the Event Viewer layout enables faster investigation of authentication attempts, account creation, and privilege modifications.
- **Privilege Auditing & Principle of Least Privilege:** Misconfigured NTFS and network share permissions create attack paths for unauthorized lateral movement and data exfiltration. The effective permission scenarios demonstrate how restrictive permissions block unauthorized activity at the file-system level.
- **Identity & Access Management (IAM):** Knowing how Active Directory organizes security principals (users, groups, OUs) helps analysts understand domain trust boundaries, credential abuse, and privilege escalation risks.

---

## Future Learning Roadmap

As I continue my SOC Analyst preparation, I plan to expand this repository with additional practical modules:

- **Active Directory Deep Dive:** Domain joins, Kerberos authentication flows, and trusts.
- **DNS & DHCP Architecture:** Dynamic DNS registration, forwarders, and DHCP scope administration.
- **Group Policy Objects (GPOs):** Centralized baseline security hardening and audit policy enforcement.
- **PowerShell Administration:** Automating administration and querying Active Directory with PowerShell (`Get-ADUser`, `Get-Service`, `Get-Acl`).
- **SOC Monitoring & Event Log Analysis:** Analyzing Windows Security Event IDs (4624, 4625, 4688, 4720, 4728) and deploying Sysmon.

---

## Getting Started

1. **Study the Concept:** Begin with [Virtualization Fundamentals](01%20-%20Virtualization/README.md) or [Windows Server Fundamentals](02%20-%20Windows%20Server%20Fundamentals/README.md) and review the concept architecture.
2. **Review the Summary:** Read the high-yield `Summary` section at the end of each module for rapid knowledge retention.
3. **Execute the Labs:** Follow the step-by-step guides in [Lab Setup](01%20-%20Virtualization/05%20-%20Lab%20Setup/README.md) and [Lab Exercises](02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md), comparing your results with the verified screenshot evidence.
4. **Master Key Terms:** Study the technical definitions in the [Key Terms Directory](Key%20Terms/README.md) to build vocabulary precision.
5. **Prepare for Technical Interviews:** Work through the tiered questions in the [Interview Questions Directory](Interview%20Questions/README.md) to practice articulating technical concepts.

---

## License

This repository is maintained for educational purposes, technical documentation, and personal learning.