# Lab 07 — Scheduling (cron & at)

## Objective

Schedule tasks to run at specific times using `cron` and `at`,
ensuring correctness, minimal scope, and proper verification.

This lab mirrors RHCSA scheduling tasks:
simple requirements, strict syntax, and careful validation.

---

## Initial State (what the exam gives you)

- The system is running normally
- The `cronie` and `at` packages are installed
- The `crond` and `atd` services may or may not be running
- No scheduled jobs exist for this task

---

## Tasks

### Cron task
1. Create a cron job that runs every day at **02:30**
2. The job must append the output of `date` to `/var/log/daily_job.log`
3. The job must run as the **root** user

### At task
4. Schedule a one-time job to write `"Hello from at"` to `/tmp/at_job.txt`
5. The job must run **5 minutes from now**

6. Verify both jobs without waiting for execution time

---

## What to Recognize (exam mindset)

- Cron jobs differ by **user context**
- Output redirection must be explicit
- `cron` syntax errors silently fail
- `at` jobs require a running daemon
- Verification does not require waiting

---

## What Red Hat Checks (pass/fail behavior)

- Cron entry exists with correct timing
- Command and redirection are correct
- Job is installed for the correct user
- `at` job is scheduled and visible
- Required services are running and enabled
