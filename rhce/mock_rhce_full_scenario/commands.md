# RHCE Full Mock Exam Scenario

This is a **full-length mock RHCE exam** designed to simulate the real test environment.

You are expected to:
- read requirements carefully
- make minimal, correct changes
- verify results
- manage time intentionally

This scenario is **not automated** — it is meant to be **executed and reasoned through manually**, exactly like the RHCE exam.

---

## Exam Rules (simulate real RHCE)

- ⏱ Recommended time: **3.5–4 hours**
- ❌ Internet access not allowed (during practice, try to avoid it)
- ✅ Use only Ansible + Linux CLI tools
- ❌ Do NOT write shell scripts unless explicitly instructed
- ✅ Idempotency is required
- ✅ Verification matters more than elegance

---

## Environment Overview

### Control Node
- Ansible installed
- SSH access to managed nodes
- You will run all commands from here

### Managed Nodes
- `node1` — application host
- `node2` — database host

---

## Task 0 — Initial Setup (do first)

Create inventory:

```bash
cat > inventory.ini <<'EOF'
[app]
node1 ansible_host=NODE1_IP ansible_user=YOUR_USER

[db]
node2 ansible_host=NODE2_IP ansible_user=YOUR_USER

[all:vars]
ansible_ssh_common_args='-o StrictHostKeyChecking=accept-new'
EOF
```

Verify connectivity:

```bash
ansible -i inventory.ini all -m ping
```

---

## Task 1 — Role Creation (Required)

Create a role named `base_config` that:

- Ensures `vim` and `curl` are installed
- Ensures `/etc/motd` contains the line:
  ```
  Managed by Ansible (RHCE)
  ```
- Is idempotent
- Uses handlers appropriately if services are modified

**Requirements**
- Role must live in `roles/base_config`
- No inline tasks in the playbook

---

## Task 2 — Web Service Configuration

Create a role named `webserver` that:

- Installs and enables `httpd`
- Deploys a configuration file using a Jinja2 template:
  - Port must be configurable via variable `web_port`
  - Default port: `8080`
- Restarts the service **only if config changes**
- Applies only to `app` hosts

---

## Task 3 — Variable Precedence

Define variables so that:

- Default `web_port` is `8080`
- `node1` runs on port `9090`
- No extra-vars are used to achieve this

You must demonstrate correct use of:
- defaults
- group_vars / host_vars
- precedence

---

## Task 4 — Looping and Structured Data

Using Ansible, ensure the following users exist **on all nodes**:

| Username | Shell           |
|--------|------------------|
| alice  | /bin/bash        |
| bob    | /bin/bash        |
| svcapp | /sbin/nologin    |

Requirements:
- Use a loop
- Use structured data (list of dictionaries)
- Idempotent behavior required

---

## Task 5 — Conditional Logic

On **database hosts only**:

- Create `/etc/db_role.conf`
- File must contain:
  ```
  role=database
  ```
- Task must be conditional
- No duplicated playbooks

---

## Task 6 — Error Handling

Create a task block that:

- Attempts to read `/etc/nonexistent.conf`
- If it fails:
  - Writes `/tmp/recovery.log` with content:
    ```
    recovered=true
    ```
- Always:
  - Appends the line `checked=true` to `/tmp/recovery.log`

You must use:
- `block`
- `rescue`
- `always`

---

## Task 7 — Ansible Vault

Create a vaulted variable file that contains:

```yaml
db_user: rhce_admin
db_password: SuperSecretPassword
```

Requirements:
- File must be encrypted with Ansible Vault
- Playbook must consume vaulted variables
- Create `/etc/db_credentials.conf` on database hosts:
  - Permissions `0600`
  - Owner `root`
  - Uses vaulted variables

---

## Task 8 — Verification Playbook

Create a playbook named `verify.yml` that:

- Confirms:
  - Required packages are installed
  - Services are running
  - Files exist with correct permissions
- Uses `assert` to fail if expectations are not met
- Does NOT modify system state

---

## Final Playbook Requirements

Create `site.yml` that:

- Uses roles only
- Applies roles to correct host groups
- Is idempotent
- Runs cleanly **twice**

Run:

```bash
ansible-playbook -i inventory.ini site.yml
ansible-playbook -i inventory.ini site.yml
```

Second run should show **no unintended changes**.

---

## Scoring Rubric (Self-Assessment)

| Area | Pass Criteria |
|----|--------------|
| Inventory | Correct groups & targeting |
| Roles | Clean structure, reuse |
| Variables | Correct precedence |
| Handlers | Trigger only on change |
| Loops | Structured, readable |
| Conditionals | No duplication |
| Error handling | Proper recovery |
| Vault | Secure + functional |
| Verification | Assert-based |

---

## Exam Completion Checklist

You should be able to answer **yes** to all:

- Did I avoid ad-hoc shell hacks?
- Are my changes minimal and targeted?
- Can I explain *why* each variable wins?
- Does everything survive a second run?
- Could another admin understand this repo?

If yes — you are RHCE-ready.

---

## Post-Exam Reflection (Optional but Valuable)

Write down:
- What slowed you down
- Where you hesitated
- Which task felt automatic

That’s where your last 10% improvement lives.
