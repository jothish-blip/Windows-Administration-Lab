# VirtualBox Networking

[Virtualization Track Overview](../README.md) | [Virtualization Concepts](../Virtualization.md) | [Next: Hypervisors](../02%20-%20Hypervisor/README.md) | [Related Lab: Configure Networking](../05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md)

---

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

## Summary

In this module, I studied the primary virtual networking modes in VirtualBox: NAT, Internal Network, Host-Only Adapter, and Bridged Adapter. I learned why an **Internal Network** (`SOC-LAB`) is the mandatory choice for enterprise lab emulation and malware analysis: it confines all DNS, DHCP, and SMB broadcast traffic within a private virtual software switch, preventing accidental collisions with my physical home network while allowing `DC01` and `CLIENT01` to communicate seamlessly.

---

## Related Resources

- **Key Terms:** [Virtual Machine Networking Key Terms](../../Key%20Terms/Virtualization%20Fundamentals/README.md#3-virtual-machine-networking)
- **Interview Preparation:** [Networking Interview Questions & Answers](../../Interview%20Questions/Virtualization%20Fundamentals/02%20-%20VirtualBox%20Networking.md)
- **Related Setup Lab:** [Configure Networking](../05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md)

---

## Navigation

- **Previous:** [Virtualization Concepts](../Virtualization.md)
- **Track Index:** [Virtualization Fundamentals](../README.md)
- **Next Module:** [02 - Hypervisor](../02%20-%20Hypervisor/README.md)
- **Related Setup Lab:** [Configure Networking](../05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md)
