# 1) Set ownership
chown root:developers /srv/projects

# 2) Set base permissions
# rwx for owner and group, none for others
chmod 2770 /srv/projects

# Explanation:
# 2 = setgid (group inheritance)
# 7 = rwx for owner
# 7 = rwx for group
# 0 = no access for others

# Verify permissions and setgid
ls -ld /srv/projects

# 3) Grant user bob access via ACL (no group change)
setfacl -m u:bob:rwx /srv/projects

# 4) Ensure bob also gets access to NEW files
setfacl -d -m u:bob:rwx /srv/projects

# 5) Verification (critical)

# Show ACLs
getfacl /srv/projects

# Check effective permissions without switching users
namei -l /srv/projects

# Confirm group inheritance behavior (conceptual check)
# New files created here should inherit group 'developers'
