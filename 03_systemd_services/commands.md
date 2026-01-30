# 1) Start the service
systemctl start httpd

# 2) Enable service at boot
systemctl enable httpd

# 3) Verify runtime status
systemctl status httpd

# 4) Verify enablement state
systemctl is-enabled httpd

# 5) Confirm the unit file location
systemctl show httpd -p FragmentPath

# 6) Identify logs (do not tail blindly on exam)
journalctl -u httpd --no-pager
