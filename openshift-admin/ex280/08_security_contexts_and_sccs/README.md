# Lab 08: Security Contexts & SCCs

This lab focuses on **Security Contexts and Security Context Constraints (SCCs)** in OpenShift.

On the EX280 exam, applications often fail to start not because they are broken, but because they are **not allowed to run** under the cluster’s security policies. Understanding *why* an application is blocked — and how to fix it correctly — is critical.

This lab builds the discipline required to identify SCC-related failures and apply **minimal, correct security adjustments**.

---

## Objectives

By the end of this lab, you will be able to:

- Understand how OpenShift enforces security through SCCs
- Identify SCC-related pod startup failures
- Inspect security context settings on pods and containers
- Associate ServiceAccounts with appropriate SCCs
- Apply the least-privileged SCC required for an application
- Verify that applications start successfully after security fixes
- Avoid unsafe or over-privileged configurations

Security failures are common on the EX280 exam and are often **silent until inspected correctly**.

## Scenario & Constraints

You are responsible for deploying and troubleshooting applications that are **restricted by OpenShift security policies**.

Some applications require specific permissions (such as running as a particular user, accessing certain filesystem paths, or using privileged features). OpenShift enforces these restrictions using **Security Context Constraints (SCCs)**.

This lab simulates SCC-related failures commonly encountered on the EX280 exam.

---

### Assumptions

- You have access to an OpenShift cluster
- Your kubeconfig is functional
- Applications and workloads already exist or can be deployed
- You are not guaranteed cluster-admin privileges

You are **not** expected to disable security features or use unrestricted access.

---

### Constraints

- Applications must comply with OpenShift security policies
- Security must be adjusted using **supported mechanisms**
- The **least-privileged** SCC must be applied
- Changes must be scoped to the correct ServiceAccount
- You must verify application behavior after changes
- You must not rely on the web console

These constraints mirror EX280 exam expectations.

---

### Success Criteria

This lab is complete when you can:

- Identify pod failures caused by SCC restrictions
- Explain which security requirement is blocking the pod
- Select the correct SCC to satisfy the requirement
- Bind the SCC to the correct ServiceAccount
- Verify the pod starts successfully after the fix
- Avoid granting unnecessary or excessive privileges

## Security Contexts & SCC Concepts (Exam-Aligned)

This lab tests your ability to recognize when an application is blocked by security policy and to apply the **smallest correct fix**.

On the EX280 exam, SCC-related failures often look like generic pod startup failures unless you know where to look.

---

### Security Contexts (Pod & Container Level)

A security context defines **how a pod or container is allowed to run**.

Common attributes you may encounter:
- `runAsUser`
- `runAsGroup`
- `fsGroup`
- `allowPrivilegeEscalation`
- `readOnlyRootFilesystem`

Security contexts are **requested** by the pod, but they are **validated** against the SCC.

A valid security context can still fail if the SCC does not allow it.

---

### Security Context Constraints (SCCs)

SCCs define **what is allowed on the cluster**.

Important points:
- SCCs are cluster-scoped
- Pods do not reference SCCs directly
- SCCs are **assigned to users or ServiceAccounts**
- OpenShift selects the most restrictive SCC that satisfies the pod

If no SCC allows the pod’s requested security context, the pod will not start.

---

### Common SCCs (Exam-Relevant)

You should recognize these by name and intent:

- `restricted`  
  Default, least-privileged SCC  
  Most applications should run here

- `anyuid`  
  Allows containers to run as any user ID  
  Commonly required by legacy images

- `privileged`  
  Allows almost all permissions  
  Rarely required and usually incorrect on the exam

Always prefer the **least-privileged SCC** that satisfies the requirement.

---

### ServiceAccounts & SCC Binding

SCCs are granted to:
- users
- ServiceAccounts

Most application pods run as a **ServiceAccount**, not as a user.

Correct workflow:
1. Identify which ServiceAccount the pod uses
2. Identify which SCC is required
3. Grant the SCC to that ServiceAccount
4. Verify pod startup

Granting SCCs directly to users is rarely correct for application workloads.

---

### Diagnosing SCC Failures

Common indicators of SCC issues:
- Pod stuck in `Pending`
- Pod fails immediately after scheduling
- Events mention security, user IDs, or forbidden actions

Logs may be empty — events are often more useful here.

---

### Discipline Reminder

- Do not over-privilege
- Fix the ServiceAccount, not the deployment
- Verify behavior after every change
- If it runs, confirm *why* it now runs

Correct security fixes are small and precise.

## Guided Tasks

Complete the following tasks **in order**.  
Treat each task as if it were an exam requirement.

Do not guess. Inspect first.

---

### Task 1 — Identify an SCC-Related Pod Failure

1. Deploy or locate an application pod that fails to start.
2. Inspect the pod status and note whether it is:
   - `Pending`
   - Immediately failing after scheduling

3. Inspect pod events carefully.

Look specifically for messages referencing:
- forbidden user IDs
- security context violations
- SCC rejections

Do not modify anything yet.

---

### Task 2 — Inspect the Pod Security Context

1. Inspect the pod or deployment specification.
2. Identify any requested security context settings such as:
   - `runAsUser`
   - `fsGroup`
   - privilege escalation settings

Determine what the pod is **asking for**, not what it is allowed to do.

---

### Task 3 — Identify the ServiceAccount in Use

1. Determine which ServiceAccount the pod is using.
2. Verify whether the default ServiceAccount is in use or a custom one.

This step is critical — SCCs are applied to **ServiceAccounts**, not pods directly.

---

### Task 4 — Determine the Required SCC

Based on the failure and requested security context:

1. Identify which SCC is blocking the pod.
2. Identify the **least-privileged SCC** that would allow the pod to start.

Do not select a broader SCC than required.

---

### Task 5 — Grant the SCC to the ServiceAccount

1. Grant the selected SCC to the correct ServiceAccount.
2. Ensure the scope is limited to only what is required.

Do not grant the SCC to all users or all ServiceAccounts.

---

### Task 6 — Verify Pod Startup and Behavior

1. Trigger a new pod creation (if required).
2. Verify the pod transitions to `Running`.
3. Confirm no new security warnings appear in events.
4. Confirm application behavior is correct.

A pod that runs must also be **understood** — know why it now works.

---

### Task 7 — Introduce and Recover from an Over-Privilege Error

Intentionally over-privilege an application by granting an unnecessary SCC.

Then:
1. Identify why this is unsafe or incorrect.
2. Remove the excessive privilege.
3. Reapply the minimal required SCC.
4. Verify the application still runs successfully.

The exam rewards least privilege, not brute force fixes.

## Verification Checklist

Before marking this lab complete, verify the following without hesitation:

- You can identify pod failures caused by SCC restrictions
- You inspect events to diagnose security-related failures
- You can identify requested security context settings
- You can determine which SCC is required to satisfy the pod
- You grant SCCs to the correct ServiceAccount
- You apply the least-privileged SCC necessary
- You verify pod startup after applying security changes
- You can explain *why* the pod now runs successfully
- You can remove unnecessary privileges without breaking the application

If any item above feels uncertain, repeat the relevant task.

---

## Lab Completion Criteria

This lab is complete when:

- You never default to `privileged`
- You always fix security issues at the ServiceAccount level
- You understand the relationship between security contexts and SCCs
- You apply minimal, precise security changes
- You verify behavior after every fix

On the EX280 exam, **over-privileging an application can cost points**, even if it runs.  
Correct, least-privileged security fixes earn full credit.

