# Verification Checklist (Post-Run)

- `getent passwd deploy`
- `id deploy`
- `chage -l deploy`

- `ls -ld /srv/appdata`
- `getfacl /srv/appdata`

- `pvs`, `vgs`, `lvs`
- `df -h | grep appdata`
- `mount -a` (no errors)

- `nmcli device status`
- `nmcli connection show`
- `hostnamectl`

- `systemctl status httpd`
- `systemctl is-enabled httpd`
- `systemctl show httpd -p FragmentPath`

- `ls -Z /srv/appdata/web`
- `semanage fcontext -l | grep httpd`
- `getenforce`

- `crontab -l`
- `atq`

- `systemctl get-default`
- `systemctl list-units --type=target`
