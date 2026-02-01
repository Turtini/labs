# RHCE Timed Mock — Scoring Rubric

This rubric is used to evaluate the **Timed Mock RHCE Exam Scenario**.
Scoring is **outcome-based**, mirroring how Red Hat exams are graded.

> Code style is secondary.  
> Correct results, structure, and idempotency determine the score.

---

## Total Points: 100  
**Recommended passing score: 70–75**

Partial credit is intentionally available.

---

## 1) Inventory & Repository Structure — 15 points

| Criteria | Points | Notes |
|------|------|------|
| Inventory groups correctly defined | 5 | Correct host grouping |
| No hardcoded hostnames/IPs in playbooks | 5 | Inventory-driven targeting |
| Roles directory used cleanly | 5 | No ad-hoc task sprawl |

**Common deductions**
- Hardcoded hosts: −5  
- Tasks in `site.yml`: −3  

---

## 2) Roles & Idempotency — 20 points

| Criteria | Points | Notes |
|------|------|------|
| Roles used for all configuration | 5 | Required |
| Handlers used for restarts | 5 | No service restarts in tasks |
| Second playbook run is clean | 10 | No unnecessary changes |

**Common deductions**
- Services restarted every run: −10  
- Using `shell` instead of modules: −5  

---

## 3) Variables & Precedence — 15 points

| Criteria | Points | Notes |
|------|------|------|
| Defaults used appropriately | 5 | Lowest precedence |
| Group/host vars applied correctly | 5 | No overrides via hacks |
| No misuse of `-e` | 5 | Extra vars only if instructed |

**Common deductions**
- Wrong variable wins: −5  
- Hardcoded values: −5  

---

## 4) Loops & Structured Data — 10 points

| Criteria | Points | Notes |
|------|------|------|
| Loop used where required | 5 | Users, files, packages |
| Structured data (dicts/lists) | 5 | Readable, scalable |

**Common deductions**
- Repetitive tasks instead of loops: −5  

---

## 5) Conditionals & Targeting — 10 points

| Criteria | Points | Notes |
|------|------|------|
| Correct host targeting via conditionals | 5 | No duplication |
| Logic implemented cleanly | 5 | Readable and safe |

**Common deductions**
- Duplicate playbooks: −5  
- Wrong hosts modified: −5  

---

## 6) Error Handling & Recovery — 10 points

| Criteria | Points | Notes |
|------|------|------|
| `block/rescue/always` used correctly | 5 | Recovery logic present |
| Failure handled intentionally | 5 | No blanket ignores |

**Common deductions**
- Using `ignore_errors` incorrectly: −5  

---

## 7) Vault & Security — 10 points

| Criteria | Points | Notes |
|------|------|------|
| Vaulted vars used correctly | 5 | Encrypted at rest |
| Permissions correct (`0600`) | 5 | Ownership enforced |

**Common deductions**
- Secrets in plaintext: −10  
- Vault password committed: automatic fail (practice rule)

---

## 8) Verification & Assertions — 10 points

| Criteria | Points | Notes |
|------|------|------|
| Assert-based verification | 5 | Explicit checks |
| Verification does not change state | 5 | Read-only validation |

**Common deductions**
- Verification modifies system: −5  

---

## Scoring Interpretation

| Score Range | Interpretation |
|-----------|----------------|
| 90–100 | Strong pass — exam confidence |
| 80–89 | Solid pass |
| 70–79 | Likely pass |
| 60–69 | Borderline — fix weak areas |
| < 60 | High risk — repeat mock |

---

## Partial Credit Philosophy

- Incomplete tasks **can still earn points**
- Correct structure with missing features often scores higher than messy “working” code
- Idempotency issues cost more than missing features

---

## Self-Reflection (after grading)

Answer honestly:
- Where did I lose the most points?
- Which tasks took the longest?
- Which patterns were automatic?
- What would I skip if short on time?

That insight is your final 10–15 point gain.

---

## Final Reminder

RHCE is not a trick exam.

It rewards:
- clarity
- restraint
- correctness
- confidence

If your automation is calm, predictable, and explainable —
you are doing it right.
