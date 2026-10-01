# Hypervisor

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

---

# Interview Questions

1. What is a Hypervisor?
2. Why do we need a Hypervisor?
3. What are the responsibilities of a Hypervisor?
4. What is the difference between Type 1 and Type 2 Hypervisors?
5. Why is VirtualBox called a Type 2 Hypervisor?
6. Which Hypervisor would you recommend for an Enterprise Data Center? Why?

---

# Summary

- A Hypervisor creates and manages Virtual Machines.
- It allocates CPU, RAM, Storage, and Networking resources.
- It keeps every VM isolated from one another.
- There are two types of Hypervisors:
  - Type 1 (Bare-Metal)
  - Type 2 (Hosted)
- VirtualBox is a Type 2 Hypervisor because it runs on top of the Host Operating System.
- VMware ESXi is a Type 1 Hypervisor because it runs directly on the Physical Hardware.