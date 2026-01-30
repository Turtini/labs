# Lab 05 — Storage (LVM & Persistent Mounts)

## Objective

Provision additional storage using LVM, format it with a filesystem,
mount it at a specific location, and ensure the mount persists
across reboots.

This lab mirrors how RHCSA tests storage:
explicit requirements, strict order of operations, and state verification.

---

## Initial State (what the exam gives you)

- An additional disk is available (e.g. `/dev/sdb`)
- The disk is unused
- No volume groups or logical volumes exist for this disk
- The system is running normally

---

## Tasks

1. Initialize `/dev/sdb` as a physical volume
2. Create a volume group named `vg_data`
3. Create a logical volume named `lv_projects` using **100% of free space**
4. Format the logical volume with the `xfs` filesystem
5. Mount the filesystem at `/mnt/projects`
6. Ensure the mount persists across reboots
7. Verify everything without rebooting

---

## What to Recognize (exam mindset)

- Storage is **sequential** — skipping steps causes failure
- Device names matter (verify before acting)
- Filesystem choice must match requirements
- Persistence (`/etc/fstab`) is part of the task, not optional

---

## What Red Hat Checks (pass/fail behavior)

- Physical volume exists
- Volume group and logical volume names are correct
- Filesystem type is correct
- Mount point exists and is mounted
- Mount persists via `/etc/fstab`
- No destructive operations were performed
