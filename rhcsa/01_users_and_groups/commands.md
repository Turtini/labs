# 1) Create the group
groupadd developers

# Verify group creation
getent group developers

# 2) Create the user with required settings
useradd \
  -g developers \
  -G wheel \
  -m \
  -s /bin/bash \
  alice

# 3) Set the user's password
passwd alice

# 4) Set account expiration date
chage -E 2026-12-31 alice

# 5) Verification (DO NOT SKIP ON EXAM)

# Confirm user entry
getent passwd alice

# Confirm group membership
id alice

# Confirm home directory and ownership
ls -ld /home/alice

# Confirm account aging information
chage -l alice
