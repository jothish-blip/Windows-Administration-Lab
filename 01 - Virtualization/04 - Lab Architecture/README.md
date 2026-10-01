# Why We Need This Lab

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

---

## Key Terms

* **Windows Server**: An operating system designed to provide services, manage networks, and authenticate users.
* **Domain Controller (DC)**: A server that responds to security authentication requests within a Windows Server domain.
* **Internal Network**: An isolated network setting in VirtualBox allowing VMs to communicate with each other but not with the host or the internet.
* **SOC Lab**: A safe, isolated environment used by Security Operations Center analysts to test, learn, and analyze threats safely.

---

## Interview Questions

* What is the primary purpose of building a SOC Lab?
* What is a Domain Controller and what are its main responsibilities?
* Why do we place the Windows Server and Windows 11 VMs on an Internal Network instead of NAT?
* How does the Windows 11 Client interact with the Domain Controller during a user login?
* What are some key services provided by a Windows Server?

---

## Summary

- Windows Server acts as the Domain Controller.
- Windows 11 acts as the Client Computer.
- Both VMs communicate through an Internal Network.
- This lab simulates a real company's network.
- It is used to learn Windows Administration and SOC fundamentals.