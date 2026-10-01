# Roles vs Features - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../02%20-%20Windows%20Server%20Fundamentals/03%20-%20Roles%20vs%20Features/README.md) | [Related Lab: Explore Roles and Features](../../02%20-%20Windows%20Server%20Fundamentals/Lab-Exercise.md#practical-lab-04) | [Key Terms](../../Key%20Terms/Windows%20Server%20Fundamentals/README.md#3-roles-and-features)

---

## Basic

### 1. What is the fundamental difference between a Server Role and a Feature in Windows Server?

**Answer:**
- **Server Role:** Defines the primary business job or major function of the server on the network (e.g., Active Directory Domain Services, DNS Server, DHCP Server, Web Server IIS).
- **Feature:** A supporting software component, utility, or capability that complements the operating system or enhances specific roles (e.g., .NET Framework, BitLocker Drive Encryption, Failover Clustering, RSAT tools).

### 2. Can a single Windows Server host multiple roles simultaneously?

**Answer:**
Yes. Windows Server is capable of running multiple roles concurrently (for example, hosting both Active Directory Domain Services and DNS Server on DC01). However, enterprise best practice separates conflicting or resource-intensive roles (e.g., never run SQL Server, Exchange, or IIS directly on an Active Directory Domain Controller).

---

## Intermediate

### 3. What is a "Role Service", and why is it distinct from a Role?

**Answer:**
A Role Service is a modular software sub-component within a broader server role. For example, within the **Active Directory Certificate Services (AD CS)** role, individual role services include Certification Authority, Online Responder, and Network Device Enrollment Service. Administrators install only the specific role services needed, minimizing system resource overhead and security exposure.

### 4. What is RSAT (Remote Server Administration Tools), and why is it important for administrative security?

**Answer:**
RSAT is a collection of administrative MMC snap-ins, command-line tools, and PowerShell modules that can be installed on client workstations (Windows 10/11) or management jump boxes. RSAT enables administrators to manage remote server roles (ADUC, DNS, DHCP, Group Policy) without needing to initiate interactive RDP sessions directly on critical Domain Controllers.

---

## Scenario-Based

### 5. Why does the Principle of Least Functionality dictate that unnecessary roles and features should never be installed on production servers?

**Answer:**
Every installed role or feature:
1. Adds background services and system binaries that require ongoing patching and reboots.
2. Frequently opens new network listening ports (e.g., installing IIS opens HTTP/HTTPS ports 80/443), dramatically increasing the server's attack surface.
3. Introduces potential vulnerability vectors. If a server only needs to serve as a DNS server, installing Print Spooler or Web Services exposes it to vulnerabilities like PrintNightmare without any operational justification.

### 6. A SOC analyst detects Windows Security Event ID 7045 ("A new service was installed in the system") followed by multiple component installation entries in `C:\Windows\Logs\CBS\CBS.log`. What might this signify?

**Answer:**
This sequence suggests an adversary who has gained administrative access is installing unauthorized server roles or features to establish persistence or expand capabilities (such as installing AD CS to execute ESC1-ESC8 certificate-based persistence, or enabling Hyper-V / WSL to bypass endpoint detection). The analyst must immediately cross-reference the activity against approved IT change requests.

---

## Navigation

- [Previous: 02 - Server Manager](02%20-%20Server%20Manager.md)
- [Back to Windows Server Interview Hub](README.md)
- [Next: 04 - Computer Management](04%20-%20Computer%20Management.md)
