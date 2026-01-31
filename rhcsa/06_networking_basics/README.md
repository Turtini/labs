# Lab 06 — Networking Basics (nmcli)

## Objective

Configure a network interface with a static IPv4 address, hostname,
and DNS settings, ensuring all changes persist across reboots.

This lab mirrors RHCSA networking tasks:
clear requirements, strict persistence, and verification without guesswork.

---

## Initial State (what the exam gives you)

- NetworkManager is running
- At least one Ethernet interface exists (e.g., `ens160`, `eth0`)
- The system currently uses DHCP
- Connectivity is working

---

## Tasks

1. Identify the active network interface and connection
2. Configure a static IPv4 address
3. Configure a default gateway
4. Configure DNS servers
5. Set the system hostname
6. Apply changes without rebooting
7. Verify persistence and connectivity

---

## What to Recognize (exam mindset)

- Interfaces and connections are **not the same thing**
- Changes must be applied to the **connection**
- Runtime connectivity does not imply persistence
- `nmcli` output is authoritative — not assumptions

---

## What Red Hat Checks (pass/fail behavior)

- Correct static IP configuration
- Gateway and DNS are set correctly
- Hostname is set correctly
- Configuration survives connection reload
- NetworkManager remains enabled and running
