# Virtualization Fundamentals

## Overview

Before installing or configuring Windows Server, I needed a safe, reliable, and isolated testing ground. Setting up enterprise services like Active Directory Domain Services, DNS, and network shares on a physical home computer is impractical and risky. Virtualization solves this by allowing multiple independent virtual machines to run concurrently on a single physical computer through a software hypervisor.

This section documents the foundational virtualization knowledge, networking design, and hands-on setup procedures I used to construct my virtual enterprise lab. Using Oracle VirtualBox as a Type 2 hypervisor, I created two isolated virtual machines—`DC01` (Windows Server 2022) and `CLIENT01` (Windows 11)—connected via an internal private network (`SOC-LAB`). This infrastructure serves as the permanent baseline for all practical Windows Server administration and SOC Analyst labs throughout this repository.

---

## What I Covered

Throughout this track, I explored core virtualization principles and completed the end-to-end deployment of the lab environment:

- **Virtualization Core Concepts:** Understanding how hypervisors abstract physical hardware (CPU, RAM, storage, network adapters) to run independent guest operating systems on a single host machine.
- **Hypervisor Architectures:** Differentiating between Type 1 (Bare-Metal) hypervisors (VMware ESXi, Microsoft Hyper-V) used in enterprise data centers, and Type 2 (Hosted) hypervisors (Oracle VirtualBox, VMware Workstation) suited for personal research and home labs.
- **VirtualBox Networking Modes:** Comparing NAT, Internal Network, and Host-Only adapters, and analyzing why an isolated Internal Network is the correct architectural choice for Active Directory testing and malware analysis.
- **Virtual Machine Snapshots:** Capturing exact point-in-time states of virtual disks and configurations, differentiating snapshots from backups, and establishing clean baseline restore points.
- **Enterprise Lab Architecture:** Designing a small corporate network topology featuring a dedicated Domain Controller (`DC01`) and a domain-joined workstation (`CLIENT01`).
- **Hands-On Lab Provisioning:** Executing the complete setup workflow across four step-by-step guides: installing VirtualBox, sizing and creating VMs, assigning static IP addressing, and verifying bidirectional ICMP network connectivity.

---

## Learning Architecture

To support systematic study, terminology revision, and technical interview preparation, each module in this track connects through a structured learning workflow:

```text
Study Concept ──> Concept Summary ──> Practical Setup Lab ──> Key Terms Review ──> Interview Questions
```

---

## Conceptual Modules

The following modules cover the architectural concepts required to understand and operate the virtual lab:

| # | Concept Module | Practical Setup Guide | Key Terms | Interview Preparation |
|:---:|:---|:---|:---|:---|
| — | [Virtualization Concepts](Virtualization.md) | [Create VMs](05%20-%20Lab%20Setup/02%20-%20Create%20and%20Configure%20Virtual%20Machines.md) | [Core Terms](../Key%20Terms/Virtualization%20Fundamentals/README.md#1-core-virtualization) | [Virtualization Q&A](../Interview%20Questions/Virtualization%20Fundamentals/01%20-%20Virtualization.md) |
| 01 | [VirtualBox Networking](01%20-%20VirtualBox%20Networking/README.md) | [Configure Networking](05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md) | [Networking Terms](../Key%20Terms/Virtualization%20Fundamentals/README.md#3-virtual-machine-networking) | [Networking Q&A](../Interview%20Questions/Virtualization%20Fundamentals/02%20-%20VirtualBox%20Networking.md) |
| 02 | [Hypervisors](02%20-%20Hypervisor/README.md) | [Install VirtualBox](05%20-%20Lab%20Setup/01%20-%20Install%20VirtualBox.md) | [Hypervisor Terms](../Key%20Terms/Virtualization%20Fundamentals/README.md#2-hypervisors) | [Hypervisors Q&A](../Interview%20Questions/Virtualization%20Fundamentals/03%20-%20Hypervisors.md) |
| 03 | [Snapshots](03%20-%20Snapshots/README.md) | [Create Snapshots](05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md#create-virtualbox-snapshots) | [Snapshot Terms](../Key%20Terms/Virtualization%20Fundamentals/README.md#4-snapshots-and-state-management) | [Snapshots Q&A](../Interview%20Questions/Virtualization%20Fundamentals/04%20-%20Snapshots.md) |
| 04 | [Lab Architecture](04%20-%20Lab%20Architecture/README.md) | [Verify Connectivity](05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md) | [Architecture Terms](../Key%20Terms/Virtualization%20Fundamentals/README.md#5-lab-architecture-and-infrastructure) | [Architecture Q&A](../Interview%20Questions/Virtualization%20Fundamentals/05%20-%20Lab%20Architecture.md) |
| 05 | [Lab Setup Overview](05%20-%20Lab%20Setup/README.md) | [4-Step Setup Guide](05%20-%20Lab%20Setup/README.md) | [Virtualization Glossary](../Key%20Terms/Virtualization%20Fundamentals/README.md) | [Track Interview Hub](../Interview%20Questions/Virtualization%20Fundamentals/README.md) |

---

## Practical Lab Setup Guides

The actual build instructions, hardware configurations, and verification steps are organized into four sequential implementation guides inside [`05 - Lab Setup/`](05%20-%20Lab%20Setup/README.md):

| Step | Guide | What I Configured & Practiced | Key Evidence / Screenshots |
|:----:|-------|------------------------------|----------------------------|
| 01 | [Install Oracle VirtualBox](05%20-%20Lab%20Setup/01%20-%20Install%20VirtualBox.md) | Installed Oracle VirtualBox on Windows host, verified networking drivers, confirmed hypervisor functionality. | [`01-VirtualBox-Manager.png`](05%20-%20Lab%20Setup/screenshots/01-VirtualBox-Manager.png) |
| 02 | [Create and Configure Virtual Machines](05%20-%20Lab%20Setup/02%20-%20Create%20and%20Configure%20Virtual%20Machines.md) | Created `DC01` (4GB RAM, 2 vCPUs, 80GB VDI) and `CLIENT01` (4GB RAM, 2 vCPUs, 60GB VDI), attached installation ISOs. | [`01-DC01-Configuration.png`](05%20-%20Lab%20Setup/screenshots/01-DC01-Configuration.png)<br>[`02-CLIENT01-Configuration.png`](05%20-%20Lab%20Setup/screenshots/02-CLIENT01-Configuration.png)<br>[`03-DC01-ISO-Attached.png`](05%20-%20Lab%20Setup/screenshots/03-DC01-ISO-Attached.png)<br>[`04-CLIENT01-ISO-Attached.png`](05%20-%20Lab%20Setup/screenshots/04-CLIENT01-ISO-Attached.png) |
| 03 | [Configure Networking](05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md) | Attached both VMs to the `SOC-LAB` Internal Network, assigned static IP `192.168.10.10` to `DC01` and `192.168.10.20` to `CLIENT01`, configured DNS. | [`01-Internal-Network-Settings.png`](05%20-%20Lab%20Setup/screenshots/01-Internal-Network-Settings.png)<br>[`02-DC01-Static-IP.png`](05%20-%20Lab%20Setup/screenshots/02-DC01-Static-IP.png)<br>[`03-CLIENT01-Static-IP.png`](05%20-%20Lab%20Setup/screenshots/03-CLIENT01-Static-IP.png) |
| 04 | [Verify Connectivity](05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md) | Verified IP addressing with `ipconfig`, tested bidirectional `ping` communication, created baseline snapshots (`Clean Windows Server`, `Clean Windows 11`). | [`01-Successful-Ping-Test.png`](05%20-%20Lab%20Setup/screenshots/01-Successful-Ping-Test.png)<br>[`02-IPConfig-Verification.png`](05%20-%20Lab%20Setup/screenshots/02-IPConfig-Verification.png)<br>[`03-VirtualBox-Snapshots.png`](05%20-%20Lab%20Setup/screenshots/03-VirtualBox-Snapshots.png) |

---

## Lab Environment Specifications

| Machine Name | Role | Operating System | RAM | vCPUs | Virtual Disk | Network Mode | IP Address | Subnet Mask | Preferred DNS |
|--------------|------|------------------|-----|:-----:|:------------:|:------------:|:----------:|:-----------:|:-------------:|
| **DC01** | Domain Controller / Server | Windows Server 2022 Std Eval | 4096 MB | 2 | 80 GB (VDI) | Internal (`SOC-LAB`) | `192.168.10.10` | `255.255.255.0` | `192.168.10.10` |
| **CLIENT01** | Domain Member / Client | Windows 11 Pro/Enterprise | 4096 MB | 2 | 60 GB (VDI) | Internal (`SOC-LAB`) | `192.168.10.20` | `255.255.255.0` | `192.168.10.10` |

---

## Concepts to Practical Implementation

| Conceptual Requirement | Practical Implementation | Verified In |
|------------------------|--------------------------|-------------|
| Hypervisor Deployment | Installed Oracle VirtualBox 7.x on physical host | [Setup Guide 01](05%20-%20Lab%20Setup/01%20-%20Install%20VirtualBox.md) |
| Virtual Hardware Allocation | Allocated dedicated RAM, vCPUs, and VDI storage per machine | [Setup Guide 02](05%20-%20Lab%20Setup/02%20-%20Create%20and%20Configure%20Virtual%20Machines.md) |
| Isolated Virtual Networking | Created `SOC-LAB` Internal Network in VirtualBox adapter settings | [Setup Guide 03](05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md) |
| Static IP Addressing | Configured deterministic IPv4 addressing (`192.168.10.0/24`) | [Setup Guide 03](05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md) |
| Network Validation | Executed bidirectional ping tests between `DC01` and `CLIENT01` | [Setup Guide 04](05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md) |
| State Preservation | Captured clean baseline snapshots before configuring server roles | [Setup Guide 04](05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md) |

---

## Why Virtualization Matters for SOC Work

In security operations, working with virtual machines is standard practice:

- **Safe Detonation & Testing:** Suspicious files, scripts, or malware samples can be analyzed inside an isolated virtual network without risking the analyst's host system or corporate network.
- **Instant Rollback:** If an administrative mistake or simulated adversary action damages the operating system, restoring a snapshot takes seconds, eliminating the need to reinstall.
- **Enterprise Emulation:** Organizations run enterprise infrastructure across clusters of virtual machines. Building and managing this lab provides direct insight into how virtual network adapters, shared storage, and hypervisor resources interact.

---

## Repository Navigation

- **Main Repository Hub:** [Windows Administration Lab](../README.md)
- **Virtualization Key Terms:** [Key Terms Directory](../Key%20Terms/Virtualization%20Fundamentals/README.md)
- **Virtualization Interview Questions:** [Interview Questions Hub](../Interview%20Questions/Virtualization%20Fundamentals/README.md)
- **Next Track:** [Windows Server Fundamentals](../02%20-%20Windows%20Server%20Fundamentals/README.md)
- **First Lab Exercise:** [Practical Lab 01: Windows Server Edition](../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-01)
