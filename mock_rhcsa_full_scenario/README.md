# Mock RHCSA Scenario — Full Practice

## Instructions

This is a full mock RHCSA-style scenario.
You are expected to complete the tasks exactly as written.

- Read all tasks before starting
- Do not reboot unless explicitly instructed
- Verify each task before moving on
- Partial completion may result in failure

---

## Initial State (what the exam gives you)

- You are logged in as `root`
- SELinux is enforcing
- NetworkManager is running
- The system has:
  - one extra disk: `/dev/sdb`
  - one active network interface using DHCP
- No prior configuration related to these tasks exists

---

## Tasks

### 1) User and group management

1. Create a group named `ops`
2. Create a user named `deploy`
   - Primary group: `ops`
   - Supplementary group: `wheel`
   - Login shell: `/bin/bash`
   - Home directory: `/home/deploy`
3. Set the password for `deploy`
4. Configure the account to expire on **December 31, 2026**

---

### 2) Permissions and ACLs

5. Create a directory `/srv/appdata`
6. Set ownership so:
   - Owner: `root`
   - Group: `ops`
7. Configure permissions so:
   - Members of `ops` can read/write/create files
   - Others have no access
8. Ensure new files inherit the `ops` group
9. Grant user `deploy` full access using ACLs (do not change group membership)

---

### 3) Storage (LVM)

10. Initialize `/dev/sdb` for use with LVM
11. Create a volume group named `vg_app`
12. Create a logical volume named `lv_data` using all available space
13. Format the logical volume with `xfs`
14. Mount it at `/srv/appdata`
15. Ensure the mount persists across reboots

---

### 4) Networking

16. Configure the active network connection with:
    - Static IP: `192.168.100.50/24`
    - Gateway: `192.168.100.1`
    - DNS: `8.8.8.8`
17. Set the system hostname to `node1.lab.example`
18. Apply changes without rebooting

---

### 5) Services

19. Ensure the `httpd` service is:
    - running
    - enabled at boot
20. Identify the unit file path used by `httpd`

---

### 6) SELinux

21. Content exists in `/srv/appdata/web`
22. Accessing the content via `httpd` returns `403 Forbidden`
23. Fix the issue while keeping SELinux enforcing
24. Ensure the fix is persistent

---

### 7) Scheduling

25. Create a cron job that runs daily at **01:15**
26. The job must append the output of `date` to `/var/log/app_heartbeat.log`
27. The job must run as `root`

28. Schedule a one-time `at` job that writes:
    `"RHCSA mock complete"`
    to `/tmp/mock_complete.txt`
    **10 minutes from now**

---

### 8) Boo
