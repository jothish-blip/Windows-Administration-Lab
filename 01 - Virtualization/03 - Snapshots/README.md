# Snapshots

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

## Key Terms

* **Snapshot**: A saved state of a Virtual Machine's disk, memory, and settings at a specific point in time.
* **Restore / Rollback**: The process of reverting a Virtual Machine back to a previously saved Snapshot.
* **Backup**: A complete, independent copy of the Virtual Machine data, intended for long-term protection and disaster recovery.
* **State**: The exact condition and configuration of the VM at the exact moment a snapshot is captured.

---

## Interview Questions

* What is a Snapshot?
* Why are Snapshots useful?
* When should you create a Snapshot?
* What is the difference between a Snapshot and a Backup?
* Why do SOC analysts frequently use Snapshots?

---

# Summary

* A Snapshot is a saved state of a Virtual Machine at a specific point in time.
* It allows you to restore the VM quickly if something goes wrong.
* Snapshots are ideal before major changes like software installation or malware testing.
* They save time and make experimentation much safer.
* Snapshots should complement backups, not replace them.
