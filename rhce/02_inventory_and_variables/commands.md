# RHCE Lab 02 — Inventory, Variables, and Precedence (Commands)

These commands are meant to be **typed and practiced**, not blindly copy/pasted.
This lab focuses on inventory structure, variable precedence, and how Ansible
decides *which value wins* — a critical RHCE skill.

---

## 0) Lab context

You will learn:
- Inventory hierarchy
- Group vs host variables
- Variable precedence
- How to prove which variable is applied

---

## 1) Enter the lab directory

```bash
cd rhce/02_inventory_and_variables
```

---

## 2) Create inventory structure

```bash
mkdir -p inventory group_vars host_vars
```

Create `inventory/inventory.ini`:

```bash
cat > inventory/inventory.ini <<'EOF'
[rhce_web]
node1 ansible_host=YOUR_NODE1_IP

[rhce_db]
node2 ansible_host=YOUR_NODE2_IP

[rhce_all:children]
rhce_web
rhce_db

[all:vars]
ansible_user=YOUR_USER
ansible_ssh_common_args='-o StrictHostKeyChecking=accept-new'
EOF
```

Verify:

```bash
ansible-inventory -i inventory/inventory.ini --graph
```

---

## 3) Define group variables

Create web group vars:

```bash
cat > group_vars/rhce_web.yml <<'EOF'
app_port: 8080
app_name: web_app
log_level: INFO
EOF
```

Create db group vars:

```bash
cat > group_vars/rhce_db.yml <<'EOF'
app_port: 5432
app_name: database
log_level: WARN
EOF
```

Create global vars:

```bash
cat > group_vars/all.yml <<'EOF'
environment: lab
owner: turtini
log_level: ERROR
EOF
```

---

## 4) Define host-specific override

```bash
cat > host_vars/node1.yml <<'EOF'
log_level: DEBUG
special_feature: enabled
EOF
```

---

## 5) Inspect variable resolution

```bash
ansible-inventory -i inventory/inventory.ini --host node1
ansible-inventory -i inventory/inventory.ini --host node2
```

Observe:
- `log_level` differs per host
- `host_vars` overrides group and all

---

## 6) Create variable inspection playbook

```bash
cat > lab02.yml <<'EOF'
- name: RHCE Lab 02 - variable precedence demo
  hosts: rhce_all
  gather_facts: false

  tasks:
    - name: Show resolved variables
      ansible.builtin.debug:
        msg:
          host: "{{ inventory_hostname }}"
          app_name: "{{ app_name | default('undefined') }}"
          app_port: "{{ app_port | default('undefined') }}"
          log_level: "{{ log_level | default('undefined') }}"
          environment: "{{ environment | default('undefined') }}"
          special_feature: "{{ special_feature | default('undefined') }}"
EOF
```

---

## 7) Run the playbook

```bash
ansible-playbook -i inventory/inventory.ini lab02.yml
```

Expected:
- `node1` log_level = DEBUG
- `node2` log_level = WARN
- `environment` applies to all

---

## 8) Inline variable override

```bash
ansible-playbook -i inventory/inventory.ini lab02.yml -e "log_level=CRITICAL"
```

Observe:
- Extra vars override **everything**

---

## 9) Command-line variable test

```bash
ansible -i inventory/inventory.ini rhce_web -m debug -a "var=log_level"
ansible -i inventory/inventory.ini rhce_db -m debug -a "var=log_level"
```

---

## 10) Variable precedence proof (important)

Order you should remember for RHCE (simplified):

1. Extra vars (`-e`)
2. Host vars
3. Group vars (child > parent)
4. group_vars/all
5. Inventory vars

If something behaves unexpectedly — **this list explains why**.

---

## 11) Cleanup (optional)

```bash
rm -rf inventory group_vars host_vars lab02.yml
```

---

## Exit checklist

You should be able to:
- Predict which variable wins
- Debug variable confusion quickly
- Use `ansible-inventory --host`
- Explain precedence verbally

If yes — Lab 02 complete.
