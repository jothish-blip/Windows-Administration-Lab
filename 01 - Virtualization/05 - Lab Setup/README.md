# Windows Administration Lab Setup

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

Follow the documents in the following order:

1. Install VirtualBox
2. Create Virtual Machines
3. Configure Networking
4. Verify Connectivity

Each document contains:

- Step-by-step instructions
- Configuration details
- Verification steps
- Screenshots

Following this guide from start to finish will create a working Windows lab that will be used throughout the rest of this repository.
---

**Next**: [Install Oracle VirtualBox](01%20-%20Install%20VirtualBox.md)