# Windows Administration Lab Setup

[Virtualization Track Overview](../README.md) | [Previous: Lab Architecture](../04%20-%20Lab%20Architecture/README.md) | [First Step: Install VirtualBox](01%20-%20Install%20VirtualBox.md) | [Next Track: Windows Server Fundamentals](../../02%20-%20Windows%20Server%20Fundamentals/README.md)

---

## Overview

This guide explains how to build the Windows Administration Lab used throughout this repository.

The lab is designed to simulate a small enterprise environment using Oracle VirtualBox. It consists of a Windows Server acting as the Domain Controller and a Windows 11 machine acting as the client.

Instead of making configuration changes on the host operating system, all experiments are performed inside virtual machines. This provides a safe environment for learning Windows Administration, Active Directory, networking, and security concepts.

The same lab will be used throughout this repository to learn:

- Windows Server Administration
- Active Directory
- DNS
- DHCP
- Group Policy
- File Sharing
- NTFS Permissions
- PowerShell Administration
- Event Viewer
- Windows Security
- SOC Analyst Fundamentals

---

# Lab Architecture

```text
                  Host Computer
                Windows 11 (Host)
                       │
              Oracle VirtualBox
                       │
          ┌────────────┴────────────┐
          │                         │
     DC01 (Windows Server)    CLIENT01 (Windows 11)
          │                         │
          └──── Internal Network ───┘
                  (SOC-LAB)
```

---

# Lab Components

| Machine | Purpose |
|----------|----------|
| DC01 | Windows Server acting as the Domain Controller |
| CLIENT01 | Windows 11 computer joined to the domain |

---

# Prerequisites

Before starting this guide, ensure you have the following:

- Oracle VirtualBox installed
- Windows Server 2022 ISO
- Windows 11 ISO
- At least 16 GB RAM
- Minimum 120 GB free disk space

---

# Documentation Structure

Follow the setup guides in sequential order:

1. [01 - Install Oracle VirtualBox](01%20-%20Install%20VirtualBox.md)
2. [02 - Create and Configure Virtual Machines](02%20-%20Create%20and%20Configure%20Virtual%20Machines.md)
3. [03 - Configure Networking](03%20-%20Configure%20Networking.md)
4. [04 - Verify Connectivity](04%20-%20Verify%20Connectivity.md)

Each document contains:

- Step-by-step instructions
- Hardware and network configuration details
- Verification steps
- Screenshot evidence from the running lab

Following this guide from start to finish creates a fully working, isolated Windows enterprise lab (`DC01` and `CLIENT01` on `SOC-LAB`).

---

## Navigation

- **Previous Module:** [04 - Lab Architecture](../04%20-%20Lab%20Architecture/README.md)
- **Track Index:** [Virtualization Fundamentals](../README.md)
- **Start Practical Setup:** [01 - Install Oracle VirtualBox](01%20-%20Install%20VirtualBox.md)
- **Next Track:** [Windows Server Fundamentals](../../02%20-%20Windows%20Server%20Fundamentals/README.md)