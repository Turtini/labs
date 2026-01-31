# 1) Identify interfaces and connections
nmcli device status
nmcli connection show

# Identify the active connection name (e.g., "Wired connection 1")

# 2) Configure static IPv4 addressing
nmcli connection modify "Wired connection 1" \
  ipv4.method manual \
  ipv4.addresses 192.168.1.50/24 \
  ipv4.gateway 192.168.1.1 \
  ipv4.dns "8.8.8.8 8.8.4.4"

# 3) Bring the connection down and back up
nmcli connection down "Wired connection 1"
nmcli connection up "Wired connection 1"

# 4) Verify IP configuration
ip addr show
ip route

# 5) Set the system hostname
hostnamectl set-hostname node1.example.com

# Verify hostname
hostnamectl

# 6) Verify DNS resolution
resolvectl status
ping -c 3 google.com

# 7) Verify persistence (inspect connection profile)
nmcli connection show "Wired connection 1"
