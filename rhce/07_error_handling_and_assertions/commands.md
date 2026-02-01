# RHCE Lab 07 — Error Handling, Blocks, and Assertions (Commands)

These commands are meant to be **typed and practiced**, not blindly copy/pasted.
This lab focuses on how to handle failures cleanly in Ansible:
- `block/rescue/always`
- `failed_when` and `changed_when`
- `ignore_errors` (when it's appropriate)
- `assert` and `fail` for defensive automation

This is RHCE-critical because tasks fail in real environments, and your automation
must respond predictably.

---

## 0) Lab context

You will build a playbook that intentionally triggers failures and then handles them safely.

You will practice:
- creating a controlled failure
- recovering in `rescue`
- always running cleanup
- enforcing expectations with `assert`
- marking tasks changed/failed intentionally

---

## 1) Enter the lab directory

```bash
cd rhce/07_error_handling_and_assertions
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

## 3) Create playbook: block/rescue/always

Create `lab07_block_rescue.yml`:

```bash
cat > lab07_block_rescue.yml <<'EOF'
- name: RHCE Lab 07 - block/rescue/always
  hosts: rhce_targets
  become: true
  gather_facts: false

  vars:
    marker_dir: /etc/rhce_lab07
    marker_file: /etc/rhce_lab07/marker.txt

  tasks:
    - name: Ensure marker directory exists (baseline)
      ansible.builtin.file:
        path: "{{ marker_dir }}"
        state: directory
        mode: "0755"

    - name: Demonstrate block/rescue/always
      block:
        - name: Create marker file
          ansible.builtin.copy:
            dest: "{{ marker_file }}"
            content: "start\n"
            mode: "0644"

        - name: Intentional failure (simulate real issue)
          ansible.builtin.command: /bin/false

        - name: This task should never run
          ansible.builtin.debug:
            msg: "If you see this, block error handling failed"

      rescue:
        - name: Recovery action (write recovery note)
          ansible.builtin.copy:
            dest: "{{ marker_file }}"
            content: "recovered\n"
            mode: "0644"

        - name: Show recovery message
          ansible.builtin.debug:
            msg: "Recovered from a controlled failure"

      always:
        - name: Always run - record completion
          ansible.builtin.lineinfile:
            path: "{{ marker_file }}"
            create: true
            line: "always_ran=true"
EOF
```

Run:

```bash
ansible-playbook -i inventory.ini lab07_block_rescue.yml
```

Verify:

```bash
ansible -i inventory.ini rhcsa_targets -m ping || true
ansible -i inventory.ini rhce_targets -b -m command -a "cat /etc/rhce_lab07/marker.txt"
```

Expected:
- Playbook reports a failure inside the block
- Rescue runs and marker file shows `recovered`
- Always runs and marker file contains `always_ran=true`

---

## 4) Create playbook: failed_when and changed_when

Create `lab07_failed_changed_when.yml`:

```bash
cat > lab07_failed_changed_when.yml <<'EOF'
- name: RHCE Lab 07 - failed_when and changed_when
  hosts: rhce_targets
  become: true
  gather_facts: false

  tasks:
    - name: Run a command that returns rc=2 but should not fail the play
      ansible.builtin.command: "bash -lc 'exit 2'"
      register: cmd_out
      failed_when: false
      changed_when: false

    - name: Show command return code
      ansible.builtin.debug:
        msg: "rc={{ cmd_out.rc }} (expected non-zero, but not failed)"

    - name: Simulate detection of a real failure condition
      ansible.builtin.command: "bash -lc 'echo ERROR: something broke; exit 0'"
      register: err_text
      changed_when: false
      failed_when: "'ERROR:' in err_text.stdout"

    - name: This task should not run if failed_when triggers
      ansible.builtin.debug:
        msg: "If you see this, failed_when did not trigger"
EOF
```

Run:

```bash
ansible-playbook -i inventory.ini lab07_failed_changed_when.yml
```

Expected:
- First command reports rc=2 but does not fail
- Second command triggers failure due to text matching

---

## 5) ignore_errors (use sparingly)

Create `lab07_ignore_errors.yml`:

```bash
cat > lab07_ignore_errors.yml <<'EOF'
- name: RHCE Lab 07 - ignore_errors demonstration
  hosts: rhce_targets
  become: true
  gather_facts: false

  tasks:
    - name: Intentional failure but continue
      ansible.builtin.command: /bin/false
      ignore_errors: true

    - name: Continue after ignored failure
      ansible.builtin.debug:
        msg: "We continued because ignore_errors=true"
EOF
```

Run:

```bash
ansible-playbook -i inventory.ini lab07_ignore_errors.yml
```

Note:
- `ignore_errors` is acceptable for non-critical tasks
- On RHCE, use it intentionally, not as a band-aid

---

## 6) Assert and fail (defensive automation)

Create `lab07_assert_fail.yml`:

```bash
cat > lab07_assert_fail.yml <<'EOF'
- name: RHCE Lab 07 - assert and fail
  hosts: rhce_targets
  become: false
  gather_facts: false

  vars:
    required_env: lab

  tasks:
    - name: Assert required variable exists and is correct
      ansible.builtin.assert:
        that:
          - required_env is defined
          - required_env == "lab"
        fail_msg: "required_env must be set to 'lab'"
        success_msg: "Environment validated"

    - name: Fail deliberately if a condition is met (demo)
      ansible.builtin.fail:
        msg: "Deliberate fail: demonstration of fail module"
      when: false
EOF
```

Run:

```bash
ansible-playbook -i inventory.ini lab07_assert_fail.yml
```

Expected:
- Assert passes
- Fail task does not run (when: false)

---

## 7) RHCE error-handling rules (memorize)

- `block/rescue/always` is for controlled recovery
- `failed_when` lets you define what "failure" means
- `changed_when` protects idempotence and prevents false change reports
- `ignore_errors` is a last resort for non-critical tasks
- `assert` is for enforcing assumptions early

---

## 8) Common RHCE mistakes

- Using `ignore_errors` everywhere instead of handling failure properly
- Allowing noisy tasks to report "changed" every run
- Not validating required variables/inputs
- Not using `block/rescue` when recovery is possible

---

## 9) Cleanup (optional)

```bash
ansible -i inventory.ini rhce_targets -b -m file -a "path=/etc/rhce_lab07 state=absent recurse=true" || true
rm -f inventory.ini lab07_*.yml
```

---

## Exit checklist

You should be able to:
- Create a controlled failure and recover using rescue
- Explain when always runs
- Use failed_when/changed_when confidently
- Use assert to enforce assumptions

If yes — Lab 07 complete.
