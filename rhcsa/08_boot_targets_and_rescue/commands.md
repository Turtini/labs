# -------------------------
# Boot targets
# -------------------------

# 1) Identify current default target
systemctl get-default

# 2) Identify active target
systemctl list-units --type=target

# 3) Set default target to multi-user (non-graphical)
systemctl set-default multi-user.target

# Verify
systemctl get-default

# 4) Switch targets at runtime (no reboot)
systemctl isolate multi-user.target

# (Optional) Switch back to graphical
systemctl isolate graphical.target

# Restore original default (if graphical was default)
systemctl set-default graphical.target

# -------------------------
# Rescue mode (runtime entry)
# -------------------------

# 5) Enter rescue mode
systemctl rescue

# You will be prompted for the root password

# -------------------------
# Inside rescue mode
# -------------------------

# 6) Check mount status
mount | grep " / "

# Root is typically mounted read-only

# 7) Remount root filesystem read-write
mount -o remount,rw /

# Verify
mount | grep " / "

# 8) Inspect system state (examples)
ls /
getenforce
systemctl list-units --failed

# -------------------------
# Exit rescue mode
# -------------------------

# 9) Exit and return to default target
exit
