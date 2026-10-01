# Hypervisor

[Virtualization Track Overview](../README.md) | [Previous: VirtualBox Networking](../01%20-%20VirtualBox%20Networking/README.md) | [Next: Snapshots](../03%20-%20Snapshots/README.md) | [Related Lab: Install VirtualBox](../05%20-%20Lab%20Setup/01%20-%20Install%20VirtualBox.md)

---

## What is a Hypervisor?

A **Hypervisor** is software that creates, runs, and manages **Virtual Machines (VMs)**.

Without a Hypervisor, Virtual Machines cannot be created or run.

It acts as a bridge between the **Physical Hardware** and the **Virtual Machines**.

---

# Hypervisor Architecture

```text
           Physical Computer
      (CPU | RAM | SSD | Network)
                  │
                  ▼
             Hypervisor
                  │
      ┌───────────┼───────────┐
      │           │           │
      ▼           ▼           ▼
 Windows VM   Ubuntu VM   Kali Linux VM
```

The Hypervisor takes the physical hardware resources and shares them among multiple Virtual Machines.

---

# Why Do We Need a Hypervisor?

Without a Hypervisor:

- Multiple Operating Systems cannot run on the same computer.
- Every OS would try to control the hardware directly.
- Resource conflicts would occur.

The Hypervisor solves this by:

- Creating Virtual Machines
- Allocating hardware resources
- Keeping each VM isolated
- Managing communication between hardware and VMs

---

# Responsibilities of a Hypervisor

- Create Virtual Machines
- Start and Stop Virtual Machines
- Allocate CPU Cores
- Allocate RAM
- Allocate Storage (Virtual Disk)
- Manage Virtual Networking
- Keep Virtual Machines isolated from each other

---

# Types of Hypervisors

There are **two types** of Hypervisors:

1. Type 1 (Bare-Metal)
2. Type 2 (Hosted)

---

# Type 1 Hypervisor (Bare-Metal)

A **Type 1 Hypervisor** runs **directly on the Physical Hardware**.

There is **no Host Operating System** between the Hypervisor and the hardware.

## Architecture

```text
        Virtual Machines
               │
               ▼
     Type 1 Hypervisor
               │
               ▼
       Physical Hardware
```

### Examples

- VMware ESXi
- Microsoft Hyper-V
- Xen

### Advantages

- High Performance
- Better Security
- Better Hardware Utilization
- Can run hundreds of Virtual Machines
- Used in Enterprise Data Centers

### Disadvantages

- Requires dedicated hardware
- More difficult to configure
- Not suitable for beginners

---

# Type 2 Hypervisor (Hosted)

A **Type 2 Hypervisor** runs **on top of an existing Operating System**.

The Host Operating System starts first, then the Hypervisor runs like a normal application.

## Architecture

```text
        Virtual Machines
               │
               ▼
     Type 2 Hypervisor
               │
               ▼
      Host Operating System
               │
               ▼
       Physical Hardware
```

### Examples

- Oracle VirtualBox
- VMware Workstation
- VMware Fusion

### Advantages

- Easy to install
- Beginner friendly
- Perfect for Home Labs
- Good for Learning and Testing

### Disadvantages

- Slightly lower performance
- Depends on the Host Operating System
- Not recommended for large enterprise environments

---

# Type 1 vs Type 2 Hypervisor

| Type 1 | Type 2 |
|---------|---------|
| Runs directly on Physical Hardware | Runs on top of a Host Operating System |
| Better Performance | Slightly Lower Performance |
| Used in Enterprise Data Centers | Used for Home Labs and Learning |
| More Secure | Good Security |
| Harder to Configure | Easy to Install |
| Example: VMware ESXi, Hyper-V | Example: VirtualBox, VMware Workstation |

---

# Why are we using VirtualBox?

We are building our SOC Lab on a personal laptop.

VirtualBox is a **Type 2 Hypervisor**, which means it runs on top of Windows.

It is:

- Easy to install
- Beginner friendly
- Free to use
- Perfect for Home Labs
- Great for Learning and Testing

## Summary

In this module, I explored hypervisor architectures and their resource allocation mechanics. I learned the critical distinction between Type 1 (Bare-Metal) hypervisors like VMware ESXi that run directly on server hardware for low latency and enterprise workloads, versus Type 2 (Hosted) hypervisors like Oracle VM VirtualBox that run as desktop applications on top of Windows. VirtualBox is the optimal choice for my local training because it allows full emulation of enterprise network topologies directly on a personal computer.

---

## Related Resources

- **Key Terms:** [Hypervisors Key Terms](../../Key%20Terms/Virtualization%20Fundamentals/README.md#2-hypervisors)
- **Interview Preparation:** [Hypervisors Interview Questions & Answers](../../Interview%20Questions/Virtualization%20Fundamentals/03%20-%20Hypervisors.md)
- **Related Setup Lab:** [Install Oracle VirtualBox](../05%20-%20Lab%20Setup/01%20-%20Install%20VirtualBox.md)

---

## Navigation

- **Previous Module:** [01 - VirtualBox Networking](../01%20-%20VirtualBox%20Networking/README.md)
- **Track Index:** [Virtualization Fundamentals](../README.md)
- **Next Module:** [03 - Snapshots](../03%20-%20Snapshots/README.md)
- **Related Setup Lab:** [Install Oracle VirtualBox](../05%20-%20Lab%20Setup/01%20-%20Install%20VirtualBox.md)