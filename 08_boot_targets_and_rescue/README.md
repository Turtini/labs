# Lab 08 — Boot Targets & Rescue Mode

## Objective

Understand and control system boot behavior using systemd targets,
and recover system access using rescue or emergency mode.

This lab mirrors RHCSA recovery scenarios:
something is wrong, access is limited, and you must act deliberately.

---

## Initial State (what the exam gives you)

- The system uses systemd
- You have console access
- The system boots normally
- Root password is known
- SELinux is enforcing

---

## Tasks

### Boot targets
1. Identify the current default boot target
2. Change the default target to multi-user mode
3. Switch targets at runtime
4. Restore the default boot target

### Rescue / emergency mode
5. Boot into rescue mode
6. Remount the root filesystem read-write
7. Verify system state
8. Exit rescue mode cleanly

---

## What to Recognize (exam mindset)

- Boot targets replace SysV runlevels
- Default target ≠ current target
- Rescue mode limits what is mounted and running
- Read-only filesystems are intentional, not errors
- Recovery is about *inspection before action*

---

## What Red Hat Checks (pass/fail behavior)

- Correct identification of default and active targets
- Ability to switch targets safely
- Proper handling of rescue mode constraints
- No permanent damage to boot configuration
