# Snapshots & State Management - Interview Questions & Answers

[Track Interview Hub](README.md) | [Study Concept](../../01%20-%20Virtualization/03%20-%20Snapshots/README.md) | [Related Lab: Create Snapshots](../../01%20-%20Virtualization/05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md#create-virtualbox-snapshots) | [Key Terms](../../Key%20Terms/Virtualization%20Fundamentals/README.md#4-snapshots-and-state-management)

---

## Basic

### 1. What is a Virtual Machine Snapshot?

**Answer:**
A Snapshot is a point-in-time image capturing a virtual machine's disk state, memory contents (if taken while running), and virtual hardware settings at a specific moment. It allows administrators to quickly revert the VM back to that exact recorded state.

### 2. When should an administrator create a Snapshot?

**Answer:**
Snapshots should be captured immediately before performing high-risk or irreversible operations:
1. Installing major Windows updates or Service Packs.
2. Promoting a server to a Domain Controller or modifying directory schema.
3. Changing complex network configurations, firewall policies, or registry settings.
4. Detonating malware, running exploit proof-of-concepts, or executing suspicious scripts.

---

## Intermediate

### 3. What is the fundamental difference between a Snapshot and a Backup?

**Answer:**
- **Snapshot:** An internal pointer and differencing disk mechanism managed by the hypervisor. It is dependent on the original base virtual disk. If the base disk is deleted or corrupts, all snapshots are lost. Snapshots are meant for short-term rollback (hours to days).
- **Backup:** An independent, complete, self-contained copy of the VM data, OS, and configuration stored on a separate physical storage system or cloud repository. Intended for long-term disaster recovery.

### 4. How does a hypervisor technically handle disk writes after a snapshot is taken?

**Answer:**
When a snapshot is created, the hypervisor freezes the base virtual hard disk file (`.vdi` or `.vmdk`) as read-only. It creates a new child file called a **differencing disk** (delta file). All subsequent file creations, modifications, and deletions are written only to this differencing disk. When reverting, the hypervisor simply deletes the differencing disk and reactivates the frozen base state.

---

## Scenario-Based

### 5. Why do SOC analysts and malware reverse engineers rely heavily on VM snapshots?

**Answer:**
During incident response and dynamic malware analysis, analysts must execute unknown, potentially destructive samples in a controlled sandbox. Snapshots allow the analyst to:
1. Capture a clean baseline state with all monitoring tools (Sysmon, Wireshark, Process Monitor) pre-configured.
2. Detonate the malware and observe network C2 beacons and persistence mechanisms.
3. Rapidly revert the virtual machine back to its pristine pre-infection state in seconds without manual cleanup or reinstallation.

### 6. An administrator has left ten snapshots active on a production SQL file server VM for six months. What technical problems will this cause?

**Answer:**
1. **Severe Storage Growth:** Differencing disks continue to grow dynamically as writes occur, risking hypervisor datastore exhaustion and crashing all VMs on that volume.
2. **Disk I/O Latency:** Every read operation must traverse the entire chain of differencing disks from child to parent, causing significant disk latency and severe performance degradation.
3. **Consolidation Risk:** Deleting or consolidating massive snapshot trees locks the VM disks for hours and can lead to corruption if interrupted. Best practice: delete or merge snapshots within 24 to 72 hours.

---

## Navigation

- [Previous: 03 - Hypervisors](03%20-%20Hypervisors.md)
- [Back to Virtualization Interview Hub](README.md)
- [Next: 05 - Lab Architecture](05%20-%20Lab%20Architecture.md)
