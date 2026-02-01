# RHCE Lab 04 — Handlers, Notifications, and Idempotency (Commands)

These commands are meant to be **typed and practiced**, not blindly copy/pasted.
This lab focuses on handlers, notifications, and ensuring idempotent behavior —
all heavily tested on the RHCE exam.

---

## 0) Lab context

You will learn:
- What handlers are and when they run
- How `notify` works
- Why handlers only trigger on change
- How idempotency affects handler execution

---

## 1) Enter the lab directory

```bash
cd rhce/04_handlers_and_idempotency
```

---

## 2) Create role structure

```bash
mkdir -p roles/webserver
cd roles/webserver
ansible-galaxy init .
```

---

## 3) Define default variables

```bash
cat > defaults/main.yml <<'EOF'
web_package: httpd
web_service: httpd
web_port: 80
EOF
```

---

## 4) Create handler

```bash
cat > handlers/main.yml <<'EOF'
- name: restart web service
  ansible.builtin.service:
    name: "{{ web_service }}"
    state: restarted
EOF
```

---

## 5) Create main task file

```bash
cat > tasks/main.yml <<'EOF'
- name: Install web package
  ansible.builtin.package:
    name: "{{ web_package }}"
    state: present

- name: Deploy web config
  ansible.builtin.copy:
    dest: /etc/httpd/conf.d/rhce.conf
    content: |
      Listen {{ web_port }}
  notify: restart web service

- name: Ensure web service is enabled and running
  ansible.builtin.service:
    name: "{{ web_service }}"
    state: started
    enabled: true
EOF
```

---

## 6) Return to lab root

```bash
cd ../../
```

---

## 7) Create inventory

```bash
cat > inventory.ini <<'EOF'
[rhce_targets]
node1 ansible_host=YOUR_NODE_IP ansible_user=YOUR_USER
EOF
```

---

## 8) Create playbook

```bash
cat > lab04.yml <<'EOF'
- name: RHCE Lab 04 - handlers and idempotency
  hosts: rhce_targets
  become: true
  gather_facts: false

  roles:
    - webserver
EOF
```

---

## 9) Run the playbook (first run)

```bash
ansible-playbook -i inventory.ini lab04.yml
```

Observe:
- Package installs
- Config file created
- Handler runs (service restarts)

---

## 10) Run the playbook again (idempotency check)

```bash
ansible-playbook -i inventory.ini lab04.yml
```

Observe:
- No changes reported
- Handler does NOT run
- This is correct RHCE behavior

---

## 11) Force a change to trigger handler

Edit role default:

```bash
sed -i 's/web_port: 80/web_port: 8080/' roles/webserver/defaults/main.yml
```

Run again:

```bash
ansible-playbook -i inventory.ini lab04.yml
```

Observe:
- Config file changes
- Handler triggers again

---

## 12) Flush handlers mid-play (advanced)

Edit playbook:

```bash
cat > lab04.yml <<'EOF'
- name: RHCE Lab 04 - handler flu
