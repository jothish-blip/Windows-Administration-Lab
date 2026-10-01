# Virtualization Fundamentals - Key Terms

[Key Terms Directory](../README.md) | [Virtualization Track Hub](../../01%20-%20Virtualization/README.md) | [Repository Overview](../../README.md) | [Virtualization Interview Questions](../../Interview%20Questions/Virtualization%20Fundamentals/README.md)

---

## Overview

This reference glossary defines the foundational terminology studied in the **Virtualization Fundamentals** track. Terms are organized by conceptual domain, with direct cross-references to the corresponding study modules and practical setup labs.

---

## Table of Contents

1. [Core Virtualization](#1-core-virtualization)
2. [Hypervisors](#2-hypervisors)
3. [Virtual Machine Networking](#3-virtual-machine-networking)
4. [Snapshots and State Management](#4-snapshots-and-state-management)
5. [Lab Architecture and Infrastructure](#5-lab-architecture-and-infrastructure)

---

## 1. Core Virtualization

Related Concept: [Virtualization Concepts](../../01%20-%20Virtualization/Virtualization.md)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Virtualization** | The technology that abstracts physical computer hardware (CPU, RAM, storage, network) to allow multiple isolated operating systems to execute concurrently on a single physical host. | Enables creation of isolated malware analysis sandboxes, attack simulation networks, and scalable enterprise server farms. |
| **Virtual Machine (VM)** | A software-based emulation of a physical computer that executes an operating system and applications as if it were a physical machine. | Each VM operates with virtual CPU, memory, virtual disks, and virtual network interfaces isolated from adjacent VMs. |
| **Host Machine** | The physical hardware system that provides the physical processor, RAM, storage drives, and network controllers to the hypervisor. | If the host is compromised or exhausts hardware capacity, all child guest VMs running on it are directly impacted. |
| **Guest Operating System** | The operating system installed and executing inside a virtual machine (e.g., Windows Server 2022 on DC01 or Windows 11 on CLIENT01). | The guest OS is unaware that it is virtualized unless hypervisor integration guest tools are inspected. |
| **Hardware Abstraction** | The decoupling of physical hardware architectures from software execution, mediated by the hypervisor layer. | Allows VMs to be migrated across heterogeneous physical hardware without operating system reconfiguration. |

---

## 2. Hypervisors

Related Concept: [02 - Hypervisors](../../01%20-%20Virtualization/02%20-%20Hypervisor/README.md) | Related Lab: [Install VirtualBox](../../01%20-%20Virtualization/05%20-%20Lab%20Setup/01%20-%20Install%20VirtualBox.md)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Hypervisor (VMM)** | Virtual Machine Monitor software that provisions, schedules, and manages virtualized access to physical hardware resources. | Enforces process and memory boundaries preventing guest VMs from escaping their virtual containers into the host. |
| **Type 1 Hypervisor** | A "bare-metal" hypervisor that installs and executes directly on physical server hardware without an underlying host OS (e.g., VMware ESXi, Proxmox VE, Microsoft Hyper-V Server). | The enterprise standard for production data centers and cloud platforms due to low latency, high throughput, and minimal attack surface. |
| **Type 2 Hypervisor** | A "hosted" hypervisor that runs as an application on top of an existing host operating system (e.g., Oracle VM VirtualBox, VMware Workstation). | Ideal for student home labs, development workstations, and security research because it requires no dedicated bare-metal server hardware. |
| **Host OS Overhead** | The system resource penalty incurred when guest VM operations must pass through both the hypervisor and the host operating system kernel. | Type 2 hypervisors incur higher latency and CPU overhead than bare-metal hypervisors due to this dual-layer scheduling. |

---

## 3. Virtual Machine Networking

Related Concept: [01 - VirtualBox Networking](../../01%20-%20Virtualization/01%20-%20VirtualBox%20Networking/README.md) | Related Lab: [Configure Networking](../../01%20-%20Virtualization/05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **NAT (Network Address Translation)** | A networking mode where the hypervisor translates private VM IP addresses into the host machine's IP address to grant outbound Internet connectivity. | Outside hosts on the LAN cannot initiate inbound connections to the VM; useful for downloading initial patches and OS installers safely. |
| **Internal Network** | An isolated virtual software switch that confines network traffic strictly between virtual machines assigned to the same named segment. | The mandatory configuration for attack simulation and domain administration labs (`SOC-LAB`); prevents malware or lab DHCP/DNS from leaking into the home LAN. |
| **Host-Only Adapter** | A private virtual network that connects guest VMs only to the host machine via a dedicated virtual loopback adapter, with no routing to the outside Internet. | Useful for managing headless lab servers via SSH or RDP from the host machine without exposing the VMs to the local physical network. |
| **Bridged Networking** | A mode where the VM adapter connects directly to the host's physical network card, receiving an IP address directly from the physical router's DHCP pool. | Treats the VM as a distinct physical machine on your home LAN; risky for malware labs because infected traffic can reach home devices. |

---

## 4. Snapshots and State Management

Related Concept: [03 - Snapshots](../../01%20-%20Virtualization/03%20-%20Snapshots/README.md) | Related Lab: [Create Snapshots](../../01%20-%20Virtualization/05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md#create-virtualbox-snapshots)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Snapshot** | A point-in-time image capturing a virtual machine's disk state, memory contents, and virtual hardware configuration. | Invaluable for malware detonation and risky server changes; allows an analyst to revert a damaged VM back to clean baseline in seconds. |
| **Differencing Disk** | A virtual disk structure where the original base disk is frozen as read-only, and all subsequent writes are redirected into a delta/child image file. | Understanding differencing disks clarifies why running many long-term snapshots degrades disk I/O performance. |
| **Rollback / Revert** | The administrative action of discarding recent changes and returning a virtual machine to an earlier snapshot state. | Used immediately after detonating an artifact or testing a destructive security exploit to restore pristine baseline lab conditions. |
| **Snapshot vs. Backup** | A snapshot is an internal hypervisor state marker dependent on base disks; a backup is an independent, complete, external copy of VM data. | Snapshots are not disaster recovery solutions. Deleting or corrupting base VM disk files destroys all dependent snapshots. |

---

## 5. Lab Architecture and Infrastructure

Related Concept: [04 - Lab Architecture](../../01%20-%20Virtualization/04%20-%20Lab%20Architecture/README.md) | Related Lab: [Verify Connectivity](../../01%20-%20Virtualization/05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md)

| Term | Technical Definition | SOC & Practical Context |
| :--- | :--- | :--- |
| **Domain Controller (DC)** | A Windows Server running Active Directory Domain Services (AD DS) that responds to security authentication and directory query requests. | The core identity anchor (`DC01` at `192.168.10.10`) governing user accounts, groups, and security policies for `soclab.local`. |
| **Client Workstation** | A client operating system joined to the domain that authenticates against the Domain Controller and accesses shared resources. | Represented by `CLIENT01` (`192.168.10.20`), used to simulate typical end-user workstation activity, triage testing, and SMB file sharing. |
| **Subnet (`/24`)** | A logical partition of an IP network. In this lab, `192.168.10.0/24` defines a 256-address block (254 usable hosts, subnet mask `255.255.255.0`). | Consistent static IP planning prevents network conflicts and simplifies firewall rules and SIEM log filtering. |
| **Internal Broadcast Domain** | The network segment in which any device can send a broadcast frame directly to all other devices attached to the same virtual switch. | Confining broadcast domains inside `SOC-LAB` prevents ARP poisoning, LLMNR/NBT-NS spoofing, and rogue DHCP traffic from reaching external networks. |

---

## Navigation

- [Back to Key Terms Directory](../README.md)
- [Next: Windows Server Key Terms](../Windows%20Server%20Fundamentals/README.md)
- [Go to Virtualization Interview Questions](../../Interview%20Questions/Virtualization%20Fundamentals/README.md)
- [Back to Virtualization Track Hub](../../01%20-%20Virtualization/README.md)
