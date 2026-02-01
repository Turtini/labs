# RHCE Lab 08 — Ansible Vault (Commands)

These commands are meant to be **typed and practiced**, not blindly copy/pasted.
This lab focuses on Ansible Vault — encrypting variables, files, and secrets —
a guaranteed RHCE exam topic.

---

## 0) Lab context

You will learn:
- How Ansible Vault works
- How to create and edit encrypted files
- How to use vaulted variables in playbooks
- How to run playbooks with vault passwords
- Common RHCE vault mistakes (and how to avoid them)

---

## 1) Enter the lab directory

```bash
cd rhce/08_ansible_vault
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

## 3) Create a vault password file (exam-style)

```bash
cat > vault_pass.txt <<'EOF'
rhce_vault_password
EOF
```

Secure it:

```bash
chmod 600 vault_pass.txt
```

RHCE note:
- On the exam, you may be *given* a vault password
- You may also be instructed to create one

---

## 4) Create an encrypted variables file

```bash
ansible-vault create secret_vars.yml --vault-password-file vault_pass.txt
```

When the editor opens, paste:

```yaml
db_user: rhce_admin
db_password: SuperSecretPassword123
api_key: abc123xyz
```

Save and exit.

Verify it’s encrypted:

```bash
cat secret_vars.yml
```

You should see:
- `$ANSIBLE_VAULT;1.1;AES256`
- Encrypted gibberish (this is correct)

---

## 5) Create a playbook that uses vaulted variables

Create `lab08.yml`:

```bash
cat > lab08.yml <<'EOF'
- name: RHCE Lab 08 - Ansible Vault usage
  hosts: rhce_targets
  become: true
  gather_facts: false

  vars_files:
    - secret_vars.yml

  tasks:
    - name: Show non-sensitive variable
      ansible.builtin.debug:
        msg: "DB user is {{ db_user }}"

    - name: Create secret file (simulating app config)
      ansible.builtin.copy:
        dest: /etc/rhce_lab08_secrets.conf
        owner: root
        group: root
        mode: '0600'
        content: |
          DB_USER={{ db_user }}
          DB_PASSWORD={{ db_password }}
          API_KEY={{ api_key }}
EOF
```

---

## 6) Run playbook with vault password file

```bash
ansible-playbook -i inventory.ini lab08.yml --vault-password-file vault_pass.txt
```

Expected:
- Playbook runs successfully
- Secrets are decrypted at runtime only

---

## 7) Verify secrets on target node

```bash
ansible -i inventory.ini rhce_targets -b -m command -a "ls -l /etc/rhce_lab08_secrets.conf"
ansible -i inventory.ini rhce_targets -b -m command -a "cat /etc/rhce_lab08_secrets.conf"
```

Confirm:
- File permissions are `0600`
- Variables rendered correctly

---

## 8) Edit vaulted file

```bash
ansible-vault edit secret_vars.yml --vault-password-file vault_pass.txt
```

Change:
```yaml
db_password: EvenMoreSecretPassword456
```

Run playbook again:

```bash
ansible-playbook -i inventory.ini lab08.yml --vault-password-file vault_pass.txt
```

---

## 9) Encrypt an existing plaintext file (common task)

Create plaintext vars:

```bash
cat > plaintext_vars.yml <<'EOF'
token: plaintext_token_value
EOF
```

Encrypt it:

```bash
ansible-vault encrypt plaintext_vars.yml --vault-password-file vault_pass.txt
```

Verify:

```bash
cat plaintext_vars.yml
```

---

## 10) Decrypt (exam troubleshooting skill)

```bash
ansible-vault decrypt plaintext_vars.yml --vault-password-file vault_pass.txt
```

Re-encrypt it:

```bash
ansible-vault encrypt plaintext_vars.yml --vault-password-file vault_pass.txt
```

---

## 11) Vault prompt instead of password file

Run with interactive prompt:

```bash
ansible-playbook -i inventory.ini lab08.yml --ask-vault-pass
```

RHCE note:
- Both methods are valid
- Follow exam instructions exactly

---

## 12) RHCE vault rules (memorize)

- Vault encrypts **data at rest**, not in memory
- Vaulted files can be used anywhere vars are allowed
- Permissions matter (`0600` for secret files)
- You must supply the vault password at runtime
- Extra vars can also be vaulted

---

## 13) Common RHCE mistakes

- Committing vault passwords to Git
- Forgetting to pass vault password to playbook
- Encrypting entire playbooks unnecessarily
- Printing secrets with `debug` unintentionally

---

## 14) Cleanup (optional)

```bash
ansible -i inventory.ini rhce_targets -b -m file -a "path=/etc/rhce_lab08_secrets.conf state=absent" || true
rm -f inventory.ini lab08.yml vault_pass.txt secret_vars.yml plaintext_vars.yml
```

---

## Exit checklist

You should be able to:
- Create and edit vaulted files
- Run playbooks with vault passwords
- Explain when and why to use Vault
- Avoid leaking secrets accidentally

If yes — Lab 08 complete.
