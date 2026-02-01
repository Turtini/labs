# EX280 Exam Day Playbook

OpenShift Administration Exam Day Playbook (EX280)

This playbook is designed to be used during a timed mock exam or as a mental checklist on real exam day. It emphasizes context awareness, verification habits, and efficient task sequencing under pressure.

These instructions are meant to be followed, not memorized line-by-line.

## Core Principles (Read First)

These principles guide *how* you work during the exam, not just *what* you do.

- **Verify everything**  
  Never assume a resource exists, is running, or is correctly configured.

- **Never assume context**  
  Always confirm:
  - Who you are logged in as
  - Which project (namespace) you are in
  - Which cluster context is active

- **Small wins > perfect elegance**  
  A working, verifiable solution scores more than an elegant one that fails validation.

- **Move forward, then return to optimize**  
  Complete tasks end-to-end before refining. Partial credit is better than perfection left unfinished.

- **Read tasks literally**  
  Do exactly what is asked — no more, no less.

## Context Hygiene (CRITICAL)

Most OpenShift exam failures come from **working in the wrong context**, not from lack of knowledge.

Before **ANY** task, and again before **verification**, confirm your context.

### Always verify:
- Who you are logged in as
- Which project (namespace) you are operating in
- That you have the expected permissions

Run **before every task**:

```bash
oc whoami
oc project


