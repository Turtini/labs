# EX280 Exam Day Playbook  
Red Hat Certified Specialist in OpenShift Administration

This document is about **execution discipline**, not commands.

You already know *how* to use OpenShift — this helps you perform under exam conditions.

---

## Before the Exam Starts

- Take 60 seconds to breathe and slow down
- Skim all tasks **once**
- Mentally categorize tasks:
  - easy / medium / complex
- Note any dependencies (projects, users, apps reused later)

---

## Golden Rules

1. **Verify everything**
2. **Never assume context**
3. **Small wins > perfect elegance**
4. **Move on if stuck**

---

## Context Hygiene (Critical)

Before *any* task:

```bash
oc whoami
oc project
