# Lab Architecture - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../01%20-%20Virtualization/04%20-%20Lab%20Architecture/README.md) | [Related Lab: Verify Connectivity](../../01%20-%20Virtualization/05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md) | [Key Terms](../../Key%20Terms/Virtualization%20Fundamentals/README.md#5-lab-architecture-and-infrastructure)

---

## Basic

### 1. What is the primary architectural purpose of building an isolated Windows Administration & SOC Lab?

**Answer:**
The primary purpose is to safely simulate an authentic enterprise corporate network. By deploying a Windows Server Domain Controller and a Windows 10/11 client machine on an isolated virtual network, an analyst can study Active Directory administration, implement least-privilege NTFS and share permissions, and simulate cyber attacks without risking production corporate assets or home network devices.

### 2. What is a Domain Controller (DC) and what are its core responsibilities?

**Answer:**
A Domain Controller is a Windows Server running Active Directory Domain Services (AD DS). Its core responsibilities are:
1. Maintaining the centralized database (`NTDS.dit`) containing all user accounts, computer accounts, security groups, and policies.
2. Authenticating users and computers attempting to log into the domain (Kerberos and NTLM).
3. Enforcing authorization policies and Group Policy Objects (GPOs) across member systems.
4. Providing DNS name resolution for internal domain resources.

---

## Intermediate

### 3. How does the Windows Client (CLIENT01) interact with the Domain Controller (DC01) during a domain user login?

**Answer:**
1. **DNS Lookup:** CLIENT01 queries its configured DNS server (DC01 at `192.168.10.10`) for the Kerberos Service Location (`_kerberos._tcp.dc._msdcs.soclab.local`) SRV record to locate an active Domain Controller.
2. **AS-REQ (Authentication Service Request):** The client sends an AS-REQ containing a timestamp encrypted with the user's password hash to the Key Distribution Center (KDC) running on DC01 (port 88).
3. **AS-REP (Authentication Service Response):** DC01 verifies the password, generates a Ticket Granting Ticket (TGT), and returns it to CLIENT01.
4. **TGS Request & Ticket Issuance:** CLIENT01 requests a service ticket to log onto the local workstation desktop; DC01 validates the TGT and issues the service ticket.
5. **GPO Processing:** CLIENT01 connects over SMB to `\\DC01\SYSVOL` to download and apply Computer and User Group Policy configurations.

### 4. Why is static IP addressing required for DC01 (`192.168.10.10`), while CLIENT01 points its primary DNS to DC01?

**Answer:**
A Domain Controller provides foundational directory and name resolution services. If its IP address changed dynamically via DHCP, client machines would lose connection to their DNS server and be unable to locate domain services or authenticate domain logons. CLIENT01 must explicitly point its DNS to `192.168.10.10` because public DNS servers (like `8.8.8.8`) have zero knowledge of private Active Directory SRV records for `soclab.local`.

---

## Scenario-Based

### 5. In your lab, CLIENT01 attempts to join `soclab.local`, but returns an error: "An Active Directory Domain Controller for the domain 'soclab.local' could not be contacted." What is the root cause?

**Answer:**
The most common root cause is a **DNS configuration mismatch**:
1. CLIENT01 is configured to use an external DNS server (or 127.0.0.1) instead of DC01's static IP (`192.168.10.10`). Because public DNS servers cannot resolve internal Active Directory `_msdcs` SRV records, the domain join fails.
2. Secondary causes: The virtual network adapter is accidentally set to NAT instead of Internal Network (`SOC-LAB`), or Windows Defender Firewall on DC01 is blocking RPC/SMB/DNS traffic.

---

## Navigation

- [Previous: 04 - Snapshots](04%20-%20Snapshots.md)
- [Back to Virtualization Interview Hub](README.md)
- [Next Track: Windows Server Interview Hub](../Windows%20Server%20Fundamentals/README.md)
