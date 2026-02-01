# RHCE Lab 06 — Loops, Iteration, and Data Structures (Commands)

These commands are meant to be **typed and practiced**, not blindly copy/pasted.
This lab focuses on loops, lists/dictionaries, and repeatable configuration patterns —
core RHCE skills.

---

## 0) Lab context

You will learn:
- Modern `loop:` usage (preferred)
- Looping over lists and dictionaries
- Creating multiple users and files cleanly
- Using `register` + loop results
- Avoiding common RHCE loop mistakes

---

## 1) Enter the lab directory

```bash
cd rhce/06_loops_and_data_structures
```

---

## 2) Create inventory

```bash
cat > inventory.ini <<'EOF'
[rhce_targets]
node1 ansible_host=YOUR_NODE_IP ansible_user=YOUR_USER
EOF
```

---

## 3) Create playbook: loop over a list

Create `lab06_list.yml`:

```bash
cat > lab06_list.yml <<'EOF'
- name: RHCE Lab 06 - loop over a list
  hosts: rhce_targets
  become: true
  gather_facts: false

  vars:
    lab_users:
      - alice
      - bob
      - carol

  tasks:
    - name: Create users from a list
      ansible.builtin.user:
        name: "{{ item }}"
        state: present
      loop: "{{ lab_users }}"
EOF
```

Run:

```bash
ansible-playbook -i inventory.ini lab06_list.yml
```

Verify on target:

```bash
ansible -i inventory.ini rhce_targets -b -m command -a "getent passwd alice bob carol"
```

Idempotency check:

```bash
ansible-playbook -i inventory.ini lab06_list.yml
```

---

## 4) Create playbook: loop over list of dictionaries

Create `lab06_dicts.yml`:

```bash
cat > lab06_dicts.yml <<'EOF'
- name: RHCE Lab 06 - loop over list of dictionaries
  hosts: rhce_targets
  become: true
  gather_facts: false

  vars:
    lab_files:
      - path: /etc/rhce_lab06/app.conf
        mode: "0644"
        content: "app_enabled=true\n"
      - path: /etc/rhce_lab06/db.conf
        mode: "0600"
        content: "db_enabled=true\n"

  tasks:
    - name: Ensure directory exists
      ansible.builtin.file:
        path: /etc/rhce_lab06
        state: directory
        mode: "0755"

    - name: Create config files from structured data
      ansible.builtin.copy:
        dest: "{{ item.path }}"
        content: "{{ item.content }}"
        mode: "{{ item.mode }}"
      loop: "{{ lab_files }}"
EOF
```

Run:

```bash
ansible-playbook -i inventory.ini lab06_dicts.yml
```

Verify:

```bash
ansible -i inventory.ini rhce_targets -b -m command -a "ls -l /etc/rhce_lab06"
ansible -i inventory.ini rhce_targets -b -m command -a "cat /etc/rhce_lab06/app.conf"
```

Idempotency check:

```bash
ansible-playbook -i inventory.ini lab06_dicts.yml
```

---

## 5) Register loop results (exam-relevant)

Create `lab06_register.yml`:

```bash
cat > lab06_register.yml <<'EOF'
- name: RHCE Lab 06 - register loop results
  hosts: rhce_targets
  become: true
  gather_facts: false

  vars:
    packages:
      - vim
      - curl

  tasks:
    - name: Install packages in a loop
      ansible.builtin.package:
        name: "{{ item }}"
        state: present
      loop: "{{ packages }}"
      register: pkg_install

    - name: Show loop results summary
      ansible.builtin.debug:
        var: pkg_install.results
EOF
```

Run:

```bash
ansible-playbook -i inventory.ini lab06_register.yml
```

---

## 6) Loop control and labeling (quality-of-life)

Create `lab06_loop_control.yml`:

```bash
cat > lab06_loop_control.yml <<'EOF'
- name: RHCE Lab 06 - loop control
  hosts: rhce_targets
  become: true
  gather_facts: false

  vars:
    lab_users:
      - name: dan
        shell: /bin/bash
      - name: erin
        shell: /sbin/nologin

  tasks:
    - name: Create users with loop labels
      ansible.builtin.user:
        name: "{{ item.name }}"
        shell: "{{ item.shell }}"
        state: present
      loop: "{{ lab_users }}"
      loop_control:
        label: "{{ item.name }}"
EOF
```

Run:

```bash
ansible-playbook -i inventory.ini lab06_loop_control.yml
```

Verify:

```bash
ansible -i inventory.ini rhce_targets -b -m command -a "getent passwd dan erin"
```

---

## 7) RHCE loop rules (memorize)

- Prefer `loop:` over legacy `with_items`
- Use list of dictionaries for structured data
- Use `loop_control.label` for readable output
- `register` on loops creates `results[]` (not a single value)

---

## 8) Common RHCE mistakes

- Looping over strings accidentally (wrong quoting)
- Forgetting `become` for user/package tasks
- Using `command` where a module exists (breaks idempotency)
- Assuming `register` returns one result instead of `results[]`

---

## 9) Cleanup (optional)

```bash
ansible -i inventory.ini rhce_targets -b -m user -a "name=alice state=absent remove=true" || true
ansible -i inventory.ini rhce_targets -b -m user -a "name=bob state=absent remove=true" || true
ansible -i inventory.ini rhce_targets -b -m user -a "name=carol state=absent remove=true" || true
ansible -i inventory.ini rhce_targets -b -m user -a "name=dan state=absent remove=true" || true
ansible -i inventory.ini rhce_targets -b -m user -a "name=erin state=absent remove=true" || true
ansible -i inventory.ini rhce_targets -b -m file -a "path=/etc/rhce_lab06 state=absent recurse=true" || true
rm -f inventory.ini lab06_*.yml
```

---

## Exit checklist

You should be able to:
- Loop over lists and dictionaries
- Use structured data cleanly
- Use `register` loop results
- Explain why loops support idempotence

If yes — Lab 06 complete.
