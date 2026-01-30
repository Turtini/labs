# Lab 02 — Permissions & ACLs

## Objective

Configure file access so multiple users can read and write shared content
without granting excessive permissions.

This lab reinforces correct use of:
- traditional UNIX permissions
- group ownership
- setgid on directories
- POSIX ACLs

---

## Initial State (what the exam gives you)

- Users `alice` and `bob` exist
- Group `developers` exists
- Directory `/srv/projects` exists
- SELinux is enforcing
- No ACLs are currently set

---

## Tasks

1. Set ownership of `/srv/projects` so:
   - Owner: `root`
   - Group: `developers`

2. Ensure all members of `developers` can:
   - Read
   - Write
   - Create files in `/srv/projects`

3. Ensure new files created in `/srv/projects`:
   - Inherit the `developers` group automatically

4. Grant user `bob` access **without**:
   - Changing group membership
   - Changing base permissions

5. Verify access without switching users

---

## What to Recognize (exam mindset)

- This is **not** a chmod-only problem
- Group inheritance matters more than owner permissions
- ACLs should be precise and minimal
- Default ACLs affect future files

---

## What Red Hat Checks (pass/fail behavior)

- Correct ownership and permissions on the directory
- setgid is applied correctly
- ACLs exist and are scoped properly
- No unnecessary world (`other`) permissions
- Access works for both current and future files
