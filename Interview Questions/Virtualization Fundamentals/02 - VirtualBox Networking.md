# VirtualBox Networking - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../01%20-%20Virtualization/01%20-%20VirtualBox%20Networking/README.md) | [Related Lab: Configure Networking](../../01%20-%20Virtualization/05%20-%20Lab%20Setup/03%20-%20Configure%20Networking.md) | [Key Terms](../../Key%20Terms/Virtualization%20Fundamentals/README.md#3-virtual-machine-networking)

---

## Basic

### 1. What is NAT (Network Address Translation) mode in VirtualBox?

**Answer:**
NAT is the default network mode where VirtualBox translates the VM's private IP requests into the host machine's IP address. It allows the VM to reach the external Internet to download software or updates, while preventing outside systems from initiating inbound connections into the VM.

### 2. What is an Internal Network in VirtualBox?

**Answer:**
An Internal Network is a completely isolated virtual software switch created within VirtualBox. Only virtual machines connected to the same named internal network (e.g., `SOC-LAB`) can communicate with each other. The host machine and the outside Internet have zero network connectivity to this segment.

### 3. What is a Host-Only Adapter?

**Answer:**
A Host-Only Adapter creates a private virtual network exclusively between the host physical machine and designated virtual machines using a virtual loopback adapter. VMs can communicate with the host and each other, but cannot communicate with the outside physical LAN or Internet.

---

## Intermediate

### 4. What are the key operational differences between NAT, Internal Network, and Bridged Adapter?

**Answer:**
- **NAT:** VM can reach the Internet through the host's IP; host cannot directly reach VM ports without explicit port-forwarding rules; other LAN devices cannot see the VM.
- **Internal Network:** Zero external Internet and zero host connectivity; strict peer-to-peer traffic solely among connected VMs on the same virtual segment.
- **Bridged Adapter:** VM connects directly to the physical network router as an independent physical peer; receives a LAN DHCP lease; full bidirectional access with all devices on the local physical network.

### 5. Why is an Internal Network preferred for an enterprise SOC lab or Active Directory build?

**Answer:**
Active Directory requires enterprise infrastructure services like a Domain Controller acting as a authoritative DNS server and potentially a DHCP server. Running unauthorized DNS/DHCP servers or domain broadcasts across a home or corporate physical LAN (which happens in Bridged mode) causes network collisions and security alerts. Internal Network ensures all domain traffic, DNS queries, and simulated attacks remain 100% contained within the isolated virtual switch.

---

## Scenario-Based

### 6. You are preparing to execute a suspected malware sample inside a Windows 10 VM. Which network adapter mode should you configure, and why?

**Answer:**
You must configure an **Internal Network** (or completely disconnect the virtual network adapter). 
- If Bridged mode is used, wormable malware (like WannaCry SMB exploits) or scanning bots could infect your physical host and other devices on your home or enterprise LAN.
- If NAT is used, the malware could communicate with external Command-and-Control (C2) servers or launch DDoS attacks.
- Internal Network guarantees complete isolation from both the host and the external world.

### 7. You have configured DC01 with static IP `192.168.10.10` and CLIENT01 with `192.168.10.20` on Internal Network `SOC-LAB`, but ping between them fails. What are the first three things you troubleshoot?

**Answer:**
1. **Network Name Mismatch:** Verify in VirtualBox VM Network Settings that both VMs are configured for "Internal Network" and use the exact same case-sensitive network name (`SOC-LAB`).
2. **Windows Defender Firewall ICMP Blocking:** By default, Windows Server and Windows 10 block inbound ICMPv4 Echo Requests (ping). Verify whether Windows Defender Firewall rules for File and Printer Sharing (Echo Request - ICMPv4-In) are enabled.
3. **Subnet Mask & IP Addressing:** Verify via `ipconfig /all` that both machines share the identical subnet mask (`255.255.255.0`) and have proper IP addressing without duplicate IP conflicts.

---

## Navigation

- [Previous: 01 - Virtualization Concepts](01%20-%20Virtualization.md)
- [Back to Virtualization Interview Hub](README.md)
- [Next: 03 - Hypervisors](03%20-%20Hypervisors.md)
