# RHCSA Exam Day Playbook

## Purpose

This playbook exists to keep you **calm, methodical, and precise** during the RHCSA exam.

You already know the commands.  
This document is about **how to use them under pressure**.

---

## Before You Start (first 2 minutes)

1. **Breathe. Slow is smooth.**
   - The exam is long enough if you don’t panic.
   - There is no bonus for finishing early.

2. **Read every task once, end to end**
   - Do not touch the keyboard yet.
   - Mark tasks mentally by domain:
     - users
     - permissions
     - storage
     - networking
     - services
     - SELinux
     - scheduling
     - boot

3. **Plan your order**
   - Start with tasks you are strongest in.
   - Leave storage and SELinux until you’re warm, not scared.

---

## Golden Rules (do not violate these)

- **Verification is part of the task**
- **Persistence is assumed unless stated otherwise**
- **If it’s unclear, inspect before changing**
- **Never disable SELinux**
- **Never reboot unless instructed**
- **Do not guess — prove**

These rules alone prevent most failures.

---

## How to Read a Task (micro-framework)

For each task, ask:

1. **What state is required?**
   - running vs enabled
   - mounted vs persistent
   - allowed vs denied

2. **What is the smallest change that achieves that state?**
   - chmod vs ACL
   - chcon vs semanage
   - runtime vs config

3. **How will I prove it worked?**
   - `getent`
   - `id`
   - `ls -l`, `ls -Z`
   - `systemctl is-enabled`
   - `mount -a`

If you can’t answer #3, you’re not done.

---

## Domain-Specific Mindsets

### Users & Groups
- Don’t assume defaults
- Always verify with `getent` and `id`
- Expiration dates are easy points — don’t forget them

---

### Permissions & ACLs
- This is rarely a `777` problem
- setgid on directories is intentional
- Default ACLs affect future files
- Verify with `getfacl`

---

### Storage (LVM)
- Identify the device before touching it
- PV → VG → LV → filesystem → mount → fstab
- Always run `mount -a` after editing fstab

---

### Networking
- Modify the **connection**, not the device
- Apply changes by reloading the connection
- Verify persistence with `nmcli connection show`

---

### Services (systemd)
- Running ≠ enabled
- Know where the unit file comes from
- Logs exist for a reason — check them once, not repeatedly

---

### SELinux
- If permissions look right and access fails, check context
- `chcon` is temporary — don’t use it
- Persistence matters more than speed
- Keep SELinux enforcing

---

### Scheduling (cron / at)
- Use absolute paths
- Know which user owns the job
- Verify with `crontab -l` and `atq`

---

### Boot & Rescue
- Default target ≠ active target
- Rescue mode is intentionally limited
- Remount root RW before changing anything
- Exit cleanly — don’t reboot unless told

---

## Time Management Strategy

- **First pass:** complete everything you know cold
- **Second pass:** storage, SELinux, networking
- **Final pass:** verification sweep

Leave **10 minutes at the end** just to verify.

---

## The Final Verification Sweep (don’t skip)

Before submitting:

- Re-read every task
- Run at least one verification command per task
- Look for:
  - missing persistence
  - wrong user context
  - typos in names
  - services not enabled

Most failures happen here — and are fixable.

---

## If Something Breaks

Pause. Breathe.

1. Inspect state
2. Undo nothing until you understand
3. Make the smallest corrective change
4. Verify again

Panic causes more damage than mistakes.

---

## Final Reminder

RHCSA is not testing:
- how fast you type
- how clever you are
- how many commands you know

It is testing whether you can:
- remain calm
- reason about system state
- apply precise changes
- verify your work

If you followed these labs, you already can.
