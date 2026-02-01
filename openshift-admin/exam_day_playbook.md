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
```

If something fails unexpectedly:

- Stop

- Re-check context

- Re-read the task requirements

Do not attempt to “debug” until context is confirmed.

### Common Context Failures

- Creating resources in the wrong project

- Applying RBAC to the wrong namespace

- Verifying resources while scoped elsewhere

- Assuming a project switch persisted between tasks

Treat context checks as a muscle memory habit, not an optional step.

## Recommended Execution Order

The OpenShift exam is **time-constrained**. Sequencing matters as much as correctness.

Use this order as a **default strategy**, not a rigid rule.

### Suggested Task Flow

1. **Project creation and access**
   - Create required projects first
   - Set default project context immediately
   - Apply basic access controls early

2. **RBAC and permissions**
   - ServiceAccounts
   - Roles / ClusterRoles
   - RoleBindings / ClusterRoleBindings
   - Verify permissions *before* deploying workloads

3. **Application deployments**
   - Deployments / DeploymentConfigs
   - ImageStreams
   - Environment variables
   - Replicas and rollout behavior

4. **ConfigMaps and Secrets**
   - Create before attaching to pods
   - Verify mounted paths and env vars
   - Restart pods if required

5. **Storage**
   - PersistentVolumeClaims
   - Volume mounts
   - Access modes and capacity
   - Confirm binding state

6. **Routes and networking**
   - Services first, then Routes
   - Verify target ports and TLS settings
   - Test connectivity early

7. **Resource limits and quotas**
   - Requests and limits
   - Quotas and LimitRanges
   - Watch for scheduling failures

8. **Troubleshooting tasks**
   - Pod failures
   - Image pull errors
   - Permission and SCC issues
   - Events and logs

### Strategic Notes
- Do not block on a single task — move forward and return later
- Dependencies matter: RBAC and storage often gate later tasks
- Small verified wins are better than perfect unfinished solutions

This order is designed to **minimize rework** and **maximize scoring efficiency**.

## Verification Mindset

On the OpenShift exam, **configuration without verification does not count**.

Every task should end with a clear, intentional verification step.

### After completing any task, confirm:

- The resource exists
- It is in the **correct project**
- It is named **exactly** as requested
- It is in the expected state (Running, Bound, Available, etc.)

### Common verification commands

Use these frequently and deliberately:

- `oc get all`
- `oc get pods`
- `oc describe <resource>`
- `oc logs <pod>`
- `oc get events`

Do not rely on assumptions or visual confirmation alone.

If you cannot prove a task is complete using `oc`, the grader cannot either.

### Verification discipline

- Verify immediately after configuration
- Re-verify during your final pass
- If verification fails, stop and fix before moving on

Strong verification habits often matter more than speed.

## Time Management Strategy

Time is a limited resource on the OpenShift exam.  
Managing it intentionally is as important as technical correctness.

### Recommended pacing

Use this as a mental framework, not a stopwatch:

- **First 10 minutes**  
  Read *all* tasks carefully. Identify dependencies and quick wins.

- **First 60% of exam time**  
  Complete easy and medium tasks end-to-end, including verification.

- **Next 25% of exam time**  
  Tackle more complex tasks that require iteration or troubleshooting.

- **Final 15% of exam time**  
  Perform verification, fixes, and cleanup.

### When you are stuck

If a task is not progressing after **5–10 minutes**:

- Stop
- Leave it in a safe state
- Move on to another task
- Return later with fresh context

Partial completion with verification often scores higher than unfinished perfection.

### Momentum matters

- Avoid spending too long on any single task
- Small, verified wins build confidence
- Calm progress reduces mistakes later

A steady pace beats bursts of rushed activity.

## Common Failure Traps

Most point loss on the OpenShift exam comes from a small set of repeatable mistakes.

Be aware of them, and actively guard against them.

### Frequent pitfalls

- **Working in the wrong project**  
  Always confirm namespace before creating or verifying resources.

- **Resources exist, but are misnamed**  
  Names must match the task exactly. Close is not correct.

- **Applications deployed but not exposed**  
  A running pod without a Service or Route often earns no credit.

- **PersistentVolumeClaims bound, but not mounted**  
  Storage must be attached and used by the application.

- **Configuration objects created but not consumed**  
  ConfigMaps and Secrets must be actively referenced.

- **Fixing symptoms instead of root cause**  
  Restarting pods without checking logs or events wastes time.

- **Skipping verification under time pressure**  
  Unverified work is indistinguishable from incomplete work.

### Recovery mindset

When something breaks:

- Pause
- Check context
- Read events and logs
- Re-read the task carefully

Most issues are simple once correctly framed.

## Final Verification Pass 

Reserve the **last 15–20 minutes** of the exam for verification and cleanup.

At minimum, perform a cluster-wide scan:

- `oc get all -A`

### Look specifically for:

- Pods in `CrashLoopBackOff` or `Error`
- Pending or unbound PersistentVolumeClaims
- Failed or incomplete builds
- Resources created in the wrong project
- Misnamed objects that do not match task requirements

Fix **low-effort, high-impact** issues first.

Do not attempt major refactors during this phase.

---

## Mental Reset 

As the exam ends:

- Breathe
- Stop making changes
- Do not delete working resources
- Trust what you have already verified

Last-minute changes introduce more risk than reward.

---

## After the Exam 

For mock exams and study sessions, write down:

- Tasks you skipped
- Tasks that consumed the most time
- Errors caused by context or naming
- Verification steps you forgot initially


---

## Final Thought

The OpenShift Administration exam is not about speed or cleverness.

It rewards:
- correctness
- verification
- recovery
- judgment

Calm, methodical execution wins.

