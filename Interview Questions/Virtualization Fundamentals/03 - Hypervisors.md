# Hypervisors - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../01%20-%20Virtualization/02%20-%20Hypervisor/README.md) | [Related Lab: Install VirtualBox](../../01%20-%20Virtualization/05%20-%20Lab%20Setup/01%20-%20Install%20VirtualBox.md) | [Key Terms](../../Key%20Terms/Virtualization%20Fundamentals/README.md#2-hypervisors)

---

## Basic

### 1. What is a Hypervisor and what are its core responsibilities?

**Answer:**
A Hypervisor (Virtual Machine Monitor) is the core software engine that abstracts physical hardware to manage virtual machines. Its responsibilities are:
1. Allocating physical CPU time, physical memory blocks, virtual disk space, and virtual network traffic across guest VMs.
2. Maintaining strict memory and process isolation so a failure or breach in one VM cannot impact another VM or the host.
3. Managing virtual hardware BIOS/UEFI, storage I/O, and virtual network adapters.

### 2. What is the fundamental difference between Type 1 and Type 2 Hypervisors?

**Answer:**
- **Type 1 (Bare-Metal):** Installs and runs directly on bare physical server hardware without any underlying operating system (e.g., VMware ESXi, Proxmox VE, Hyper-V Server). The hypervisor *is* the operating system.
- **Type 2 (Hosted):** Installs and runs as an application on top of an existing host operating system (e.g., Oracle VM VirtualBox, VMware Workstation running on Windows 11).

### 3. Why is Oracle VM VirtualBox classified as a Type 2 Hypervisor?

**Answer:**
VirtualBox is a Type 2 Hypervisor because it requires a pre-existing host operating system (such as Windows, macOS, or Linux) to be installed first. VirtualBox runs as an application inside that host OS and relies on the host OS kernel and drivers to access the physical hardware.

---

## Intermediate

### 4. Which hypervisor architecture would you recommend for an Enterprise Data Center, and why?

**Answer:**
An enterprise data center must use a **Type 1 (Bare-Metal) Hypervisor** (such as VMware ESXi, Microsoft Hyper-V, or Nutanix AHV) because:
- **Performance & Low Latency:** It eliminates the resource consumption and scheduling latency of an intermediary host OS.
- **Reliability:** Lacks consumer applications, third-party software, or desktop updates that could cause host operating system crashes.
- **Security:** Has an extremely small codebase and minimal attack surface compared to a general-purpose host OS.

### 5. Why are Type 2 Hypervisors like VirtualBox ideal for student labs and security researchers?

**Answer:**
Type 2 hypervisors run directly on regular laptops or desktop computers without requiring dedicated server hardware. Students and analysts can quickly test multiple operating systems, snapshot states, and isolate networks while retaining their normal desktop environment for documentation, web research, and tools.

---

## Scenario-Based

### 6. What is a "Hypervisor Escape" vulnerability, and why is it considered a critical security threat?

**Answer:**
A Hypervisor Escape (e.g., CVE-2018-0798 in VirtualBox or vulnerabilities in virtual SVGA/NIC drivers) occurs when exploit code executing inside a guest virtual machine breaks out of the VM container and executes arbitrary code directly on the host operating system or hypervisor kernel. This is a catastrophic failure because a compromised low-privilege guest VM can achieve complete control over the physical host and all other co-located guest VMs.

---

## Navigation

- [Previous: 02 - VirtualBox Networking](02%20-%20VirtualBox%20Networking.md)
- [Back to Virtualization Interview Hub](README.md)
- [Next: 04 - Snapshots](04%20-%20Snapshots.md)
