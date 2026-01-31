# Lab 04 — SELinux Basics

## Objective

Allow a service to access required files while keeping SELinux in
**enforcing** mode and applying the *minimum* necessary change.

This lab mirrors how SELinux issues appear on RHCSA:
the service is running, permissions look correct, but access is denied.

---

## Initial State (what the exam gives you)

- SELinux is enforcing
- The `httpd` service is installed and running
- Content exists in `/srv/webcontent`
- Accessing the content returns `403 Forbidden`
- File permissions appear correct
- No custom SELinux configuration has been applied

---

## Tasks

1. Confirm SELinux is enforcing
2. Identify why access is denied
3. Apply the correct SELinux context to `/srv/webcontent`
4. Ensure the fix persists across relabels and reboots
5. Verify access without disabling SELinux

---

## What to Recognize (exam mindset)

- This is **not** a chmod or chown problem
- SELinux failures are silent unless you look for them
- Temporary fixes (like `chcon`) are not sufficient
- Persistence matters more than speed

---

## What Red Hat Checks (pass/fail behavior)

- SELinux remains enforcing
- The correct context is applied
- The service can access the content
- No unnecessary booleans are enabled
- No global SELinux configuration is weakened
