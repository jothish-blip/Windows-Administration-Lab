# Snapshots

[Virtualization Track Overview](../README.md) | [Previous: Hypervisors](../02%20-%20Hypervisor/README.md) | [Next: Lab Architecture](../04%20-%20Lab%20Architecture/README.md) | [Related Lab: Create Snapshots](../05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md#create-virtualbox-snapshots)

---

## What is a Snapshot?

A **Snapshot** is a saved state of a Virtual Machine at a specific point in time.

It allows us to restore the VM to that exact state if something goes wrong.

Think of it as a **Restore Point** for a Virtual Machine.

---

# Snapshot Workflow

```text
Install Windows
      │
      ▼
Take Snapshot
      │
      ▼
Install Software
      │
      ▼
Something Breaks
      │
      ▼
Restore Snapshot
      │
      ▼
Everything Works Again

```

---

## Why Do We Use Snapshots?

Snapshots help us:

* Save Time
* Recover Quickly
* Test Software Safely
* Undo Mistakes
* Analyze Malware
* Learn Without Fear

---

## When Should We Take Snapshots?

Take a Snapshot before:

* Windows Updates
* Installing Active Directory
* Configuring Networking
* Installing Security Tools
* Malware Testing
* Major System Changes

---

## Snapshot vs Backup

| Snapshot | Backup |
| --- | --- |
| Saves VM state | Creates a copy of the VM |
| Fast to create | Slower to create |
| Fast recovery | Slower recovery |
| Short-term rollback | Long-term protection |

---

## Best Practices

* Take Snapshots before major changes.
* Use meaningful Snapshot names.
* Delete old Snapshots when they are no longer needed.
* Do not use Snapshots as a replacement for backups.

---

## Summary

In this module, I studied virtual machine snapshots, differencing disks, and state management. I learned that a snapshot freezes the base virtual disk and redirects all subsequent writes into a delta file, enabling near-instantaneous rollback if a software update, registry change, or malware execution corrupts the system. I also established the critical distinction that snapshots rely on the underlying base virtual disk and cannot replace independent, long-term backups.

---

## Related Resources

- **Key Terms:** [Snapshots and State Management Key Terms](../../Key%20Terms/Virtualization%20Fundamentals/README.md#4-snapshots-and-state-management)
- **Interview Preparation:** [Snapshots Interview Questions & Answers](../../Interview%20Questions/Virtualization%20Fundamentals/04%20-%20Snapshots.md)
- **Related Setup Lab:** [Create VirtualBox Snapshots](../05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md#create-virtualbox-snapshots)

---

## Navigation

- **Previous Module:** [02 - Hypervisor](../02%20-%20Hypervisor/README.md)
- **Track Index:** [Virtualization Fundamentals](../README.md)
- **Next Module:** [04 - Lab Architecture](../04%20-%20Lab%20Architecture/README.md)
- **Related Setup Lab:** [Create VirtualBox Snapshots](../05%20-%20Lab%20Setup/04%20-%20Verify%20Connectivity.md#create-virtualbox-snapshots)
