# Virtualization

## Definition

**Virtualization** is the technology that allows **one physical computer** to run **multiple independent operating systems** by creating **Virtual Machines (VMs)** using a **Hypervisor**.

### Example

Instead of buying four separate computers:

- Windows Server
- Windows 11
- Ubuntu
- Kali Linux

You can buy **one powerful computer** and run all four operating systems as Virtual Machines.

## Why Virtualization?

Modern organizations rarely deploy one physical server for every service. Instead, they use virtualization to run multiple virtual servers on a single physical machine.

For example, one physical server can host:

- Active Directory
- DNS
- DHCP
- SQL Server
- Web Server
- File Server

This approach reduces hardware costs, improves resource utilization, simplifies management, and makes testing and recovery much easier.

---

# Core Concepts

## Virtual Machine (VM)

A **Virtual Machine (VM)** is a **software-based computer** that behaves like a real physical computer.

Each VM has its own virtual:

- CPU
- RAM
- Storage (Virtual Hard Disk)
- Operating System
- Network Card
- BIOS/UEFI

Each VM works independently, even though they share the same physical hardware.

## Hypervisor

A **Hypervisor** is software that creates, manages, and runs Virtual Machines.

### Responsibilities

- Creates Virtual Machines
- Allocates CPU
- Allocates RAM
- Allocates Storage
- Manages Networking
- Keeps VMs isolated from each other

## Host vs Guest OS

### Host Machine
The **Host Machine** is the physical computer that runs the Hypervisor.

**Example:**
- Laptop
- Desktop
- Physical Server

### Guest Operating System
A **Guest Operating System** is the operating system installed inside a Virtual Machine.

**Examples:**
- Windows Server
- Ubuntu
- Kali Linux
- Windows 11

---

# Virtualization Architecture

```text
                Physical Computer
        (CPU | RAM | SSD | Network)

                     │
                     ▼

                Hypervisor
        (Manages Virtual Machines)

     ┌─────────┬─────────┬─────────┬─────────┐
     ▼         ▼         ▼         ▼

 Windows    Ubuntu    Kali    Windows
 Server      Linux      Linux       11
   VM          VM         VM         VM

```

---

# Real-World Example

A company has one powerful server with:

* 128 GB RAM
* 32 CPU Cores
* 4 TB SSD

Instead of purchasing six physical servers, it creates six Virtual Machines:

* Active Directory Server
* DNS Server
* DHCP Server
* SQL Server
* Web Server
* Linux Server

All six servers run independently on the same physical machine.

---

# Benefits and Use Cases

## Advantages of Virtualization

### 1. Saves Money

Instead of buying multiple physical servers, companies buy a few powerful servers and create many Virtual Machines.
This saves:

* Hardware Cost
* Electricity
* Cooling
* Maintenance

### 2. Better Hardware Utilization

Many physical servers use only a small percentage of their resources.
Virtualization allows multiple VMs to share the same hardware, improving CPU, RAM, and storage utilization.

### 3. Easy Testing

Virtual Machines are ideal for testing:

* Malware
* New Software
* Windows Server
* Linux Distributions
* Applications

If something goes wrong, simply delete or restore the VM.

### 4. Isolation

Each Virtual Machine is isolated from the others.
**Example:** If a Kali Linux VM gets infected with malware, the Windows Server VM remains unaffected (unless resources are intentionally shared).

### 5. Snapshots

A **Snapshot** is a saved state of a Virtual Machine.
It allows you to restore the VM to an earlier point if something goes wrong.
**Example:**
Install Windows → Take Snapshot → Install Software → Software crashes → Restore Snapshot

### 6. Disaster Recovery

Virtual Machines can be backed up and restored quickly.
If the physical server fails, the VM can be restored on another server with minimal downtime.

## Where Virtualization is Used

* Data Centers
* Cloud Platforms (AWS, Azure, Google Cloud)
* Cybersecurity Labs
* SOC Operations
* Penetration Testing
* Software Development
* DevOps
* IT Training Labs
* Testing Environments

## Virtualization vs Physical Computer

| Feature | Virtualization | Physical Computer |
| --- | --- | --- |
| **Form** | Software-based Virtual Machines | Real Physical Computer |
| **OS Count** | Multiple Operating Systems | Usually One Operating System |
| **Scalability** | Easy to Scale | Expensive to Scale |
| **State Saving** | Snapshots Available | No Snapshots |
| **Recovery** | Faster Recovery | Slower Recovery |
| **Utilization** | Better Resource Utilization | Lower Resource Utilization |
| **Cost** | Lower Hardware Cost | Higher Hardware Cost |

---

# Review and Assessment

## Key Terms

* **Virtualization:** Running multiple operating systems on one physical computer.
* **Virtual Machine (VM):** A software-based computer that behaves like a real computer.
* **Hypervisor:** Software that creates and manages Virtual Machines.
* **Host Machine:** The physical computer running the Hypervisor.
* **Guest Operating System:** The operating system installed inside a Virtual Machine.
* **Snapshot:** A saved state of a Virtual Machine that allows quick recovery.

## Summary

* One physical computer can run multiple operating systems.
* Virtual Machines are software-based computers.
* A Hypervisor creates and manages Virtual Machines.
* Virtualization reduces hardware costs and improves resource utilization.
* Snapshots allow quick recovery.
* Virtualization is widely used in Data Centers, Cloud Computing, Cybersecurity, DevOps, and Software Development.

## Interview Questions

1. What is Virtualization?
2. What is a Virtual Machine?
3. What is a Hypervisor?
4. What is the difference between a Host Machine and a Guest Operating System?
5. What are the advantages of Virtualization?
6. What is a Snapshot?
7. Why do companies prefer Virtualization over Physical Servers?
8. Where is Virtualization commonly used?

---

# Module Navigation

## Learning Path

| Step | Topic |
| --- | --- |
| 1 | [VirtualBox Networking](https://www.google.com/search?q=./01%2520-%2520VirtualBox%2520Networking/README.md) |
| 2 | [Hypervisor](https://www.google.com/search?q=./02%2520-%2520Hypervisor/README.md) |
| 3 | [Snapshots](https://www.google.com/search?q=./03%2520-%2520Snapshots/README.md) |
| 4 | [Lab Architecture](https://www.google.com/search?q=./04%2520-%2520Lab%2520Architecture/README.md) |
| 5 | [Lab Setup](https://www.google.com/search?q=./05%2520-%2520Lab%2520Setup/README.md) |

Complete the topics in order to build a strong foundation before moving to the Windows Server module.

## Next Module

→ **Windows Server** *(Coming Next)*