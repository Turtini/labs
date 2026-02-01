# RHCE Lab 01 — Ansible Execution Model (CLI Fundamentals)

This lab builds your "Ansible muscle memory" for the RHCE-style environment.

You are not learning *everything* Ansible here — you are learning the **execution model**:
- how Ansible decides what to run
- how to target hosts
- how to interpret output
- how to verify results quickly

This lab is designed to be **studied and practiced**, not treated like a one-click script.

---

## Objectives

By the end of this lab, you should be able to:

1. Run an ad-hoc command against a host group
2. Run a playbook with clear targeting and privilege escalation
3. Use `-i`, `-l`, `-b`, `-K`, `-u`, and `--become-method` intentionally
4. Use `-v/-vv/-vvv` to debug, and know when to stop increasing verbosity
5. Use `--check` and `--diff` safely
6. Verify results on the managed nodes using native Linux commands

---

## Assumptions / Environment

This lab intentionally avoids requiring a specific Red Hat exam image.

You need **at least two Linux hosts** you can SSH to:
- one control node (where you run `ansible` / `ansible-playbook`)
- one or more managed nodes

Examples:
- local VMs
- cloud instances
- lab environment hosts

> If you only have one machine, you can still practice by targeting `localhost`
> (but RHCE is fundamentally about managing remote nodes).

---

## Recommended approach

1. **Read `commands.md` once end-to-end**
2. **Type every command manually** (no copy/paste during practice sessions)
3. **After each step, verify** using the verification commands provided
4. **Repeat** until you can do the core flow from memory:
   - inventory -> ping -> ad-hoc -> playbook -> check/diff -> verify

---

## Files in this lab

- `commands.md` — the exact commands to practice (and what they teach)

---

## What you are practicing (and why RHCE cares)

### 1) Inventory awareness
RHCE tasks often fail because the candidate targets the wrong host(s) or uses the wrong inventory.

### 2) Privilege escalation discipline
Most tasks require root-level changes. You must become root reliably and predictably.

### 3) Idempotence mindset
You will run playbooks multiple times. "OK vs CHANGED" matters.

### 4) Verification habits
Passing is about outcomes. You must confirm your work quickly using Linux primitives.

---

## Exit criteria (pass this lab)

You can do all of the following without notes:

- Create an inventory with groups
- Run `ansible all -m ping`
- Run an ad-hoc command to install a package (or create a file) with `-b`
- Run a playbook that changes something once, then shows **0 changes** on second run
- Use `--check --diff` and explain what it means
- Verify results on the managed host(s)

---

## Troubleshooting quick hits

- **SSH issues**: confirm `ssh user@host` works *before* blaming Ansible
- **Python missing**: some minimal distros need python installed on managed nodes
- **Permission denied**: you forgot `-b` or the remote user lacks sudo
- **Wrong hosts targeted**: re-check `-i` and group names, use `--list-hosts`

When in doubt, add verbosity:
- `-v` for normal debugging
- `-vv` for connection troubleshooting
- `-vvv` when you truly need deep detail (then stop and read)

---

## Next lab

Lab 02 will build on this by introducing:
- inventories at scale
- host/group vars
- precedence (the quiet killer)
- fact gathering and what it does to runtime
