# -------------------------
# Cron job (root)
# -------------------------

# 1) Ensure cron service is running and enabled
systemctl enable --now crond

# Verify
systemctl status crond

# 2) Edit root's crontab
crontab -e

# Add the following line:
# minute hour day month weekday command
30 2 * * * /usr/bin/date >> /var/log/daily_job.log

# 3) Verify cron entry
crontab -l

# -------------------------
# At job (one-time)
# -------------------------

# 4) Ensure at daemon is running and enabled
systemctl enable --now atd

# Verify
systemctl status atd

# 5) Schedule the at job (5 minutes from now)
echo "echo 'Hello from at' > /tmp/at_job.txt" | at now + 5 minutes

# 6) Verify at job is queued
atq

# Inspect the job content (optional, but useful)
at -c <job_id>
