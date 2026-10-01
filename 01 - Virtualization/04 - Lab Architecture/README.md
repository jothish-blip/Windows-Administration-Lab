# Lab Architecture & Topology

[Virtualization Track Overview](../README.md) | [Previous: Snapshots](../03%20-%20Snapshots/README.md) | [Next: Lab Setup](../05%20-%20Lab%20Setup/README.md) | [Next Track: Windows Server Fundamentals](../../02%20-%20Windows%20Server%20Fundamentals/README.md)

---

## Purpose

The goal of this lab is to create a small company network inside VirtualBox.

This lab will help us learn:

- Windows Server Administration
- Active Directory
- Networking
- Domain Management
- Basic SOC Operations

---

# Lab Architecture

```text
                     Host Laptop
                          │
               VirtualBox (Type 2 Hypervisor)
                          │
        ┌─────────────────┴─────────────────┐
        │                                   │
        ▼                                   ▼
 +------------------+              +------------------+
 | Windows Server   |              | Windows 11       |
 | Domain Controller|              | Client Computer  |
 +------------------+              +------------------+
        │                                   │
        └──────── Internal Network ─────────┘
                  (SOC-LAB)
```

---

## Windows Server

Windows Server manages the network.

It provides services like:

- Active Directory
- DNS
- DHCP
- User Authentication
- Group Policy

---

## Domain Controller

A Domain Controller is a Windows Server that manages:

- Users
- Computers
- Authentication
- Security Policies

Instead of creating users on every computer, they are created once on the Domain Controller.

---

## Windows 11 Client

The Windows 11 VM acts as an employee's computer.

It will:

- Join the Domain
- Log in using Domain Accounts
- Receive Group Policies
- Communicate with the Domain Controller

---

## Internal Network

The Windows Server and Windows 11 Client communicate using an Internal Network. 

This provides:

- VM ↔ VM Communication
- No Internet
- Safe and Isolated Environment

---

## Why SOC Analysts Use Labs

SOC Labs provide a safe environment to:

- Practice Active Directory
- Analyze Malware
- Test Security Tools
- Simulate Cyber Attacks
- Learn Windows Administration

## Summary

In this module, I designed the network architecture and identity topology for the SOC environment. By placing `DC01` (Windows Server at `192.168.10.10`) and `CLIENT01` (Windows 11 at `192.168.10.20`) on the private `SOC-LAB` internal network segment, I created an isolated enterprise domain (`soclab.local`). This architecture establishes the dual-machine foundation needed to study Active Directory authentication, Group Policy delivery, SMB file sharing, and security monitoring.

---

## Related Resources

- **Key Terms:** [Lab Architecture and Infrastructure Key Terms](../../Key%20Terms/Virtualization%20Fundamentals/README.md#5-lab-architecture-and-infrastructure)
- **Interview Preparation:** [Lab Architecture Interview Questions & Answers](../../Interview%20Questions/Virtualization%20Fundamentals/05%20-%20Lab%20Architecture.md)
- **Related Setup Lab:** [Verify Connectivity](../05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md)

---

## Navigation

- **Previous Module:** [03 - Snapshots](../03%20-%20Snapshots/README.md)
- **Track Index:** [Virtualization Fundamentals](../README.md)
- **Next Module:** [05 - Lab Setup](../05%20-%20Lab%20Setup/README.md)
- **Next Track:** [Windows Server Fundamentals](../../02%20-%20Windows%20Server%20Fundamentals/README.md)