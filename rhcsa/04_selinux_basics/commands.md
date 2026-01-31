# 1) Confirm SELinux status
getenforce

# Expected: Enforcing

# 2) Inspect SELinux context on the directory
ls -Zd /srv/webcontent

# Likely incorrect type (e.g., default_t)

# 3) Define the correct persistent context
semanage fcontext -a -t httpd_sys_content_t "/srv/webcontent(/.*)?"

# Explanation:
# -a  = add rule
# -t  = set SELinux type
# Regex ensures all files and subdirectories inherit context

# 4) Apply the context to existing files
restorecon -Rv /srv/webcontent

# 5) Verify the context is now correct
ls -Zd /srv/webcontent

# 6) Verify service access (conceptual check)
curl localhost
