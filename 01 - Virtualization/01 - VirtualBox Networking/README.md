# VirtualBox Networking

## Why do Virtual Machines need Networking?

Think about a normal Physical Computer.

```text
Laptop
   │
   ▼
Internet

```

A physical computer needs networking to:

* Access websites
* Download software
* Install Windows Updates
* Communicate with other computers

A **Virtual Machine** is also a computer running inside the Host Computer.

So, it also needs a network to:

* Access the Internet
* Download software
* Communicate with other Virtual Machines
* Join an Active Directory Domain
* Transfer files

VirtualBox provides different network modes depending on what we want our VM to do.

---

## Types of Networks in VirtualBox

There are three main networking modes that we will use:

1. NAT (Network Address Translation)
2. Internal Network
3. Host-Only Adapter

Each network mode has a different purpose.

---

## 1. NAT (Network Address Translation)

NAT (Network Address Translation) allows a Virtual Machine to access the Internet by sharing the Host Computer's IP address.

The VM does not connect directly to the Internet.

Instead:

VM → Host → Internet

## Architecture

```text
        Internet
            │
            ▼
      Host Computer
            │
      (NAT Service)
            │
            ▼
       Virtual Machine

```

### Characteristics

* Internet Access (Yes)
* Download Software (Yes)
* Windows Updates (Yes)
* Browse Websites (Yes)
* VM ↔ VM Communication (No)
* Host ↔ VM Communication (No)

### When to Use NAT

Use NAT when you need:

* Windows Updates
* Download Software
* Install Applications
* Browse the Internet

---

## 2. Internal Network

An **Internal Network** creates a private network only for Virtual Machines.

Only Virtual Machines connected to the same Internal Network can communicate.

The Host Computer cannot communicate with the VMs.

There is no Internet connection.

## Architecture

```text
          Internal Network
             (SOC-LAB)
        ┌────────┴────────┐
        ▼                 ▼
 Windows Server       Windows 11

```

### Characteristics

* VM ↔ VM Communication (Yes)
* Internet Access (No)
* Host ↔ VM Communication (No)
* Safe for Malware Testing (Yes)

### When to Use Internal Network

* Active Directory Labs
* SOC Labs
* Malware Analysis
* Penetration Testing
* Blue Team / Red Team Practice

---

# 3. Host-Only Adapter

A **Host-Only Adapter** creates a private network between the Host Computer and the Virtual Machines.

The Host can communicate with every VM.

The VMs can also communicate with each other.

However, there is no Internet connection.

## Architecture

```text
          Host Computer
                │
      Host-Only Adapter
        ┌───────┴────────┐
        ▼                ▼
 Windows Server     Windows 11

```

### Characteristics

* Host ↔ VM Communication (Yes)
* VM ↔ VM Communication (Yes)
* Internet Access (No)

### When to Use Host-Only Adapter

* File Sharing
* Remote Desktop (RDP)
* SSH
* Managing Virtual Machines
* Testing Applications

---

## Comparison Table

| Feature | NAT | Internal Network | Host-Only Adapter |
| --- | --- | --- | --- |
| Internet Access | Yes | No | No |
| VM ↔ VM | Limited | Yes | Yes |
| Host ↔ VM | No | No | Yes |
| Windows Updates | Yes | No | No |
| Malware Labs | No | Yes | Yes |
| Active Directory | No | Yes | Yes |

---

## Which Network Will We Use?

During Windows installation:

Use **NAT** so the VM can:

* Download Updates
* Install Software

After installation:

Switch both Virtual Machines to an **Internal Network**.

```text
          Internal Network
             (SOC-LAB)
        ┌────────┴────────┐
        ▼                 ▼
 Windows Server       Windows 11

```

This creates a safe and isolated environment for our SOC Lab.

---

## Key Terms

* **Host Computer**: The physical physical machine that runs the virtualization software (like VirtualBox).
* **Virtual Machine (VM)**: A software-based computer running inside a physical Host Computer.
* **NAT (Network Address Translation)**: A network mode that allows a VM to share the host's IP address to access the external internet.
* **Internal Network**: An isolated network where only connected Virtual Machines can communicate with each other.
* **Host-Only Adapter**: A private network configuration that allows communication between the Host Computer and its VMs, but provides no internet access.

---

## Interview Questions

* What is NAT?
* What are the advantages of NAT?
* What is an Internal Network?
* Why is an Internal Network preferred for SOC labs?
* What is a Host-Only Adapter?
* Which network type allows the Host to communicate with the VM?
* Which network type provides Internet access?
* Which network type is the safest for malware analysis?

---

## Summary

* NAT provides Internet access by sharing the Host's IP address.
* Internal Network allows only Virtual Machines to communicate with each other.
* Host-Only Adapter allows communication between the Host and Virtual Machines without Internet access.
* Internal Network is the safest option for SOC Labs and Malware Analysis.
