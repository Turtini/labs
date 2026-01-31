# 1) Identify the available disk
lsblk

# Confirm /dev/sdb exists and has no partitions or mountpoints

# 2) Create the physical volume
pvcreate /dev/sdb

# Verify
pvs

# 3) Create the volume group
vgcreate vg_data /dev/sdb

# Verify
vgs

# 4) Create the logical volume (use all free space)
lvcreate -n lv_projects -l 100%FREE vg_data

# Verify
lvs

# 5) Create the filesystem (xfs is default for RHEL)
mkfs.xfs /dev/vg_data/lv_projects

# 6) Create the mount point
mkdir -p /mnt/projects

# 7) Mount the filesystem
mount /dev/vg_data/lv_projects /mnt/projects

# Verify mount
df -h | grep projects
lsblk

# 8) Make the mount persistent
blkid /dev/vg_data/lv_projects

# Copy the UUID, then edit /etc/fstab
# Example entry:
# UUID=<uuid>  /mnt/projects  xfs  defaults  0 0

# 9) Validate fstab safely (DO NOT reboot blindly)
mount -a

# If no errors appear, persistence is correct
