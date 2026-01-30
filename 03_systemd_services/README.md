# Lab 03 — systemd Services

## Objective

Ensure a service is correctly configured to:
- start successfully
- run persistently across reboots
- fail loudly and visibly when misconfigured

This lab mirrors how RHCSA evaluates service management:
clear requirements, strict verification, no assumptions.

---

## Initial State (what the exam gives you)

- The system uses systemd
- The `httpd` package is installed
- The service is currently stopped
- No guarantee the service is enabled at boot

---

## Tasks

1. Start the `httpd` service
2. Enable `httpd` to start at boot
3. Verify the service is running and enabled
4. Confirm which unit file is being used
5. Identify where logs would appear if the service failed

---

## What to Recognize (exam mindset)

- Starting a service is **not** the same as enabling it
- systemd tracks:
  - runtime state
  - enablement state
  - unit file location
- Verification commands matter more than success messages

---

## What Red Hat Checks (pass/fail behavior)

- Service is running
- Service is enabled
- No errors are masked
- The administrator understands *where* systemd is sourcing configuration
