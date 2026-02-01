# RHCE Lab 05 — Templates, Facts, and Conditionals (Commands)

These commands are meant to be **typed and practiced**, not blindly copy/pasted.
This lab focuses on Jinja2 templates, Ansible facts, and conditional logic —
all heavily tested on the RHCE exam.

---

## 0) Lab context

You will learn:
- How Ansible facts are gathered and used
- How to write Jinja2 templates
- How to use conditionals (`when`)
- How templates interact with handlers
- How to avoid common RHCE templating mistakes

---

## 1) Enter the lab directory

```bash
cd rhce/05_templates_and_conditionals
```

---

## 2) Create role structure

```bash
mkdir -p roles/motd
cd roles/motd
ansible-galaxy init .
```

---

## 3) Create template file

```bash
cat > templates/motd.j2 <<'EOF'
Welcome to {{ ansible_hostname }}

OS: {{ ansible_distribution }} {{ ansible_distribution_version }}
Kernel: {{ ansible_kernel }}
Architecture: {{ ansible_architecture }}

{% if ansible_memtotal_mb >= 2048 %}
System memory status: OK
{% else %}
System memory status: LOW
{% endif %}

Managed by Ansible
EOF
```

---

## 4) Create handler

```bash
cat > handlers/main.yml <<'EOF'
- name: reload motd
  ansible.builtin.command: /bin/true
EOF
```

(Note: RHCE often uses no-op handlers like this to test handler mechanics.)

---

## 5) Create main task file

```bash
cat > tasks/main.yml <<'EOF'
- name: Deploy dynamic MOTD
  ansible.builtin.template:
    src: motd.j2
    dest: /etc/motd
    owner: root
    group: root
    mode: '0644'
  notify: reload motd
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
cat > lab05.yml <<'EOF'
- name: RHCE Lab 05 - templates and conditionals
  hosts: rhce_targets
  become: true
  gather_facts: true

  roles:
    - motd
EOF
```

---

## 9) Run the playbook (first run)

```bash
ansible-playbook -i inventory.ini lab05.yml
```

Observe:
- Facts gathered
- Template rendered
- Handler notified

---

## 10) Verify output on target node

```bash
ssh YOUR_USER@YOUR_NODE_IP
cat /etc/motd
```

Confirm:
- Hostname is correct
- OS details are accurate
- Memory condition reflects system state

Exit SSH:

```bash
exit
```

---

## 11) Idempotency check

```bash
ansible-playbook -i inventory.ini lab05.yml
```

Observe:
- No changes reported
- Handler does not re-run

---

## 12) Modify template to force change

```bash
sed -i 's/Managed by Ansible/Managed by RHCE Ansible/' roles/motd/templates/motd.j2
```

Run again:

```bash
ansible-playbook -i inventory.ini lab05.yml
```

Observe:
- Template change detected
- Handler triggered

---

## 13) Add conditional task (advanced)

Edit tasks file:

```bash
cat > roles/motd/tasks/main.yml <<'EOF'
- name: Deploy dynamic MOTD
  ansible.builtin.template:
    src: motd.j2
    dest: /etc/motd
    owner: root
    group: root
    mode: '0644'
  notify: reload motd

- name: Debug memory warning
  ansible.builtin.debug:
    msg: "System memory is below recommended threshold"
  when: ansible_memtotal_mb < 2048
EOF
```

Run:

```bash
ansible-playbook -i inventory.ini lab05.yml
```

---

## 14) RHCE templating rules (memorize)

- Facts require `gather_facts: true`
- Templates are evaluated on the controller
- Conditionals use `when`
- Jinja2 logic must not break YAML structure
- Handlers still obey idempotency rules

---

## 15) Common RHCE mistakes

- Forgetting to gather facts
- Using `{{ }}` inside `when`
- Putting logic inside templates that belongs in tasks
- Hardcoding values instead of using facts

---

## 16) Cleanup (optional)

```bash
rm -rf roles inventory.ini lab05.yml
```

---

## Exit checklist

You should be able to:
- Use facts in templates
- Write conditional logic confidently
- Predict template rendering
- Debug broken Jinja2 syntax quickly

If yes — Lab 05 complete.
