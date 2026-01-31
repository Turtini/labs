# Lab 01 — Users & Groups

## Objective

Create and manage local users and groups according to explicit requirements,
ensuring correct UID/GID assignment, group membership, home directories,
and account settings.

This lab mirrors the style of tasks commonly evaluated in the RHCSA exam.

---

## Initial State (what the exam gives you)

- You are logged in as a privileged user (root or sudo)
- No users or groups referenced in this lab exist yet
- Default system configuration is unchanged

---

## Tasks

1. Create a group named `developers`
2. Create a user named `alice`
   - Primary group: `developers`
   - Supplementary group: `wheel`
   - Home directory: `/home/alice`
   - Login shell: `/bin/bash`
3. Set a password for `alice`
4. Ensure `alice`’s account expires on **December 31, 2026**
5. Verify all settings without logging in as the user

---

## What to Recognize (exam mindset)

- User creation is **not just `useradd alice`**
- Group membership must be verified, not assumed
- Account expiration is often forgotten
- Red Hat expects verification via system files and commands

---

## What Red Hat Checks (pass/fail behavior)

- User exists with correct UID/GID relationships
- Group membership is correct
- Home directory exists with proper ownership
- Shell is set correctly
- Account expiration date is set exactly

## License

This repository is licensed under the MIT License and is intended for
educational use and skill development.

