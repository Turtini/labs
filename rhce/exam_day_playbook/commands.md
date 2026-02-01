# RHCE Exam Day Playbook

This playbook is a **mental and technical checklist** for exam day.
It exists to prevent panic, scope creep, and self-inflicted mistakes.

You do not need to be clever to pass RHCE.
You need to be **calm, methodical, and precise**.

---

## Before You Start (5–10 minutes)

### 1. Breathe and read everything
- Read **all exam tasks first**
- Do NOT start typing immediately
- Identify:
  - host groups
  - roles required
  - vault usage
  - verification requirements

> The exam rewards planning. Speed comes *after* clarity.

---

### 2. Create your skeleton immediately

Do this before solving any task.

```bash
mkdir -p roles group_vars host_vars
touch site.yml inventory.ini
```

Create inventory **first**.

---

## Time Strategy (4 hours total)

| Phase | Time | Goal |
|----|----|----|
| Planning | 20 min | Understand scope |
| Core roles | 90 min | Base + services |
| Vars + logic | 45 min | Precedence, conditionals |
| Vault + errors | 30 min | Secure + resilient |
| Verification | 30 min | Assert everything |
| Buffer | 25 min | Fix mistakes calmly |

If you feel rushed early, **slow down** — rushing causes rework.

---

## Inventory Discipline (Critical)

- Name groups clearly
- Never hardcode hostnames in playbooks
- Verify targeting early

```bash
ansible-inventory -i inventory.ini --graph
```

If targeting is wrong, **everything else is wrong**.

---

## Role-First Rule

- Use roles for **everything**
- No inline tasks in `site.yml`
- One role = one responsibility

Correct pattern:

```yaml
- hosts: app
  roles:
    - webserver
```

Incorrect:
- giant playbooks
- copy-pasted tasks
- shell hacks

---

## Variable Strategy (Memorize)

From lowest to highest:

1. role defaults
2. inventory vars
3. group_vars
4. host_vars
5. play vars
6. extra vars

If something behaves oddly, **this list explains why**.

---

## Handlers & Idempotency

- Restart services **only** via handlers
- Handlers run once per play
- If a service restarts every run, you will lose points

Test often:

```bash
ansible-playbook site.yml
ansible-playbook site.yml
```

Second run should be mostly `ok`.

---

## Vault Rules (Non-Negotiable)

- Vault passwords must not be committed
- Use vaulted vars only where needed
- Permissions matter (`0600`)

Run with intent:

```bash
ansible-playbook site.yml --vault-password-file vault_pass.txt
```

or

```bash
ansible-playbook site.yml --ask-vault-pass
```

---

## Error Handling Discipline

Use:
- `block / rescue / always` when recovery is possible
- `failed_when` to define real failure
- `assert` to enforce expectations

Avoid:
- blanket `ignore_errors`
- hiding failures

---

## Verification Is Part of the Task

If the exam asks you to “configure X”:
- You must **prove X exists and works**

Use:
- `assert`
- `stat`
- `service_facts`
- `package_facts`

Verification playbooks **must not change state**.

---

## Debugging Under Pressure

Start small:
```bash
-v
```

Escalate only if needed:
```bash
-vv
```

If you’re confused:
- stop
- re-read the task
- check variable resolution

---

## Common Exam Killers (Avoid These)

- Hardcoding values
- Restarting services in tasks
- Forgetting `become: true`
- Using `shell` instead of modules
- Not verifying permissions
- Ignoring idempotency

---

## Final 30 Minutes Checklist

- Run full playbook twice
- Run verification playbook
- Scan output for unexpected changes
- Re-read tasks and confirm coverage

Ask yourself:
> “If I were grading this, could I clearly see that each requirement is met?”

---

## Mindset Reminder

You are not being tested on:
- speed typing
- clever tricks
- obscure flags

You *are* being tested on:
- clarity
- structure
- correctness
- calm execution

If something breaks:
- isolate it
- fix it
- move on

---

## Exam End Reflection (Optional)

Immediately after:
- Write down what felt hard
- Note where you hesitated
- That’s your growth edge

---

## Final Thought

RHCE is not about automation.
It’s about **trust**.

Show the grader they can trust:
- your structure
- your intent
- your results

You’ve already done the hard part.
Now just execute.
