# RHCE Lab 01 — Ansible Execution Model (Commands)

These commands are meant to be **typed and practiced**, not blindly copy/pasted during study sessions.
This lab focuses on understanding *how Ansible executes*, which is critical for the RHCE exam.

---

## 0) Sanity check: Ansible availability

```bash
ansible --version
ansible-playbook --version
```

Observe:
- Ansible Core version
- Python version
- Config file path (important later)

---

## 1) Create a minimal inventory

From the lab directory:

```bash
cd rhce/01_ansible_execution_model
```

Create `inventory.ini`:

```bash
cat > inventory.ini <<'EOF'
[rhce_targets]
node1 ansible_host=YOUR_NODE1_IP ansible_user=YOUR_USER

# Optional second node
# node2 ansible_host=YOUR_NODE2_IP ansible_user=YOUR_USER

[all:vars]
ansible_ssh_common_args='-o StrictHostKeyChecking=accept-new'
EOF
```

Verify:

```bash
cat inventory.ini
```

---

## 2) Confirm connectivity (ping module)

```bash
ansible -i inventory.ini all -m ping
```

If it fails, debug SSH:

```bash
ansible -i inventory.ini all -m ping -vv
```

---

## 3) Fact gathering awareness

```bash
ansible -i inventory.ini rhce_targets -m setup | head
```

Facts are expensive. On RHCE, disable them unless needed.

---

## 4) Targeting discipline

```bash
ansible -i inventory.ini rhce_targets --list-hosts
```

Limit to one host:

```bash
ansible -i inventory.ini rhce_targets -l node1 -m ping
```

---

## 5) Privilege escalation (become)

Without become:

```bash
ansible -i inventory.ini rhce_targets -m command -a "id"
ansible -i inventory.ini rhce_targets -m command -a "cat /etc/shadow" || true
```

With become:

```bash
ansible -i inventory.ini rhce_targets -b -m command -a "id"
```

With sudo password prompt:

```bash
ansible -i inventory.ini rhce_targets -b -K -m command -a "id"
```

---

## 6) Idempotence via ad-hoc command

```bash
ansible -i inventory.ini rhce_targets -b -m file -a "path=/etc/turtini_lab01 state=touch mode=0644"
```

Run again — second run should be `ok`.

Verify:

```bash
ansible -i inventory.ini rhce_targets -b -m command -a "ls -l /etc/turtini_lab01"
```

---

## 7) Create a simple playbook

```bash
cat > lab01.yml <<'EOF'
- name: RHCE Lab 01 - execution model demo
  hosts: rhce_targets
  become: true
  gather_facts: false

  tasks:
    - name: Create marker file
      ansible.builtin.file:
        path: /etc/turtini_lab01_playbook
        state: touch
        mode: "0644"

    - name: Ensure config line exists
      ansible.builtin.lineinfile:
        path: /etc/turtini_lab01.conf
        create: true
        line: "lab01_enabled=true"
EOF
```

---

## 8) Run the playbook twice

```bash
ansible-playbook -i inventory.ini lab01.yml
ansible-playbook -i inventory.ini lab01.yml
```

Second run should show idempotence.

---

## 9) Check mode and diff

```bash
ansible-playbook -i inventory.ini lab01.yml --check --diff
```

---

## 10) Verbosity for debugging

```bash
ansible-playbook -i inventory.ini lab01.yml -v
ansible-playbook -i inventory.ini lab01.yml -vv
```

---

## 11) Verify results manually

```bash
ansible -i inventory.ini rhce_targets -b -m command -a "ls -l /etc/turtini_lab01_playbook"
ansible -i inventory.ini rhce_targets -b -m command -a "cat /etc/turtini_lab01.conf"
```

---

## 12) Cleanup (optional)

```bash
ansible -i inventory.ini rhce_targets -b -m file -a "path=/etc/turtini_lab01 state=absent"
ansible -i inventory.ini rhce_targets -b -m file -a "path=/etc/turtini_lab01_playbook state=absent"
ansible -i inventory.ini rhce_targets -b -m file -a "path=/etc/turtini_lab01.conf state=absent"
```

---

## Exit checklist

You should be able to:
- Explain inventory targeting
- Use `become` confidently
- Demonstrate idempotence
- Use `--check --diff`
- Verify results manually

If yes — Lab 01 complete.

