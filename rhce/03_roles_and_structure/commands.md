# RHCE Lab 03 — Roles, Defaults vs Vars, and Structure (Commands)

These commands are meant to be **typed and practiced**, not blindly copy/pasted.
This lab focuses on Ansible roles, directory structure, and variable precedence
*inside roles* — a core RHCE concept.

---

## 0) Lab context

You will learn:
- How roles are structured
- The difference between defaults and vars
- How Ansible resolves role variables
- How roles are executed in playbooks

---

## 1) Enter the lab directory

```bash
cd rhce/03_roles_and_structure
```

---

## 2) Create role skeleton

```bash
mkdir -p roles/demo_role
cd roles/demo_role
ansible-galaxy init .
```

Verify structure:

```bash
tree .
```

Key directories to remember for RHCE:
- defaults/
- vars/
- tasks/
- handlers/
- templates/
- files/

---

## 3) Define role defaults (lowest precedence)

```bash
cat > defaults/main.yml <<'EOF'
app_name: demo_app
app_port: 8080
log_level: INFO
EOF
```

---

## 4) Define role vars (higher precedence than defaults)

```bash
cat > vars/main.yml <<'EOF'
log_level: WARN
role_owner: rhce_candidate
EOF
```

---

## 5) Create main task file

```bash
cat > tasks/main.yml <<'EOF'
- name: Show role variable resolution
  ansible.builtin.debug:
    msg:
      app_name: "{{ app_name }}"
      app_port: "{{ app_port }}"
      log_level: "{{ log_level }}"
      role_owner: "{{ role_owner | default('undefined') }}"
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

## 8) Create playbook using role

```bash
cat > lab03.yml <<'EOF'
- name: RHCE Lab 03 - role execution
  hosts: rhce_targets
  gather_facts: false

  roles:
    - demo_role
EOF
```

---

## 9) Run the playbook

```bash
ansible-playbook -i inventory.ini lab03.yml
```

Observe:
- `log_level` comes from **vars**, not defaults
- defaults only apply when nothing overrides them

---

## 10) Override role vars from playbook

Edit playbook:

```bash
cat > lab03.yml <<'EOF'
- name: RHCE Lab 03 - role execution with override
  hosts: rhce_targets
  gather_facts: false

  vars:
    log_level: DEBUG

  roles:
    - demo_role
EOF
```

Run again:

```bash
an
