# Lab 07: Troubleshooting & Debugging

This lab focuses on **systematic troubleshooting and recovery** of OpenShift applications and resources.

On the EX280 exam, many tasks do not work on the first attempt — sometimes by design. The exam rewards candidates who can **identify failures quickly, isolate the cause, and fix the correct layer** without thrashing.

This lab builds calm, methodical debugging habits under time pressure.

---

## Objectives

By the end of this lab, you will be able to:

- Diagnose application failures using `oc` inspection commands
- Identify whether issues are caused by:
  - configuration
  - storage
  - networking
  - permissions
  - image or build failures
- Use logs and events to isolate root causes
- Correct misconfigurations without introducing new errors
- Verify recovery and application health after fixes

Troubleshooting is not a separate skill — it is how all OpenShift skills are graded on the EX280 exam.

## Scenario & Constraints

You are given applications and resources that are **not functioning correctly**.

Some failures are obvious, while others are subtle. Multiple layers may be involved, but **each task has a primary root cause**. Your job is to identify that cause and fix it without unnecessary changes.

This lab simulates the troubleshooting conditions commonly encountered on the EX280 exam.

---

### Assumptions

- You have access to an OpenShift cluster
- Your kubeconfig is functional
- Applications and resources already exist
- You are not guaranteed cluster-admin privileges

You are **not** expected to redesign applications or re-architect solutions.

---

### Constraints

- Only fix what is broken
- Do not delete and recreate resources unless required
- Use inspection commands before making changes
- Prefer minimal, targeted fixes
- Verify behavior after every change
- You must not rely on the web console

These constraints mirror EX280 exam expectations.

---

### Success Criteria

This lab is complete when you can:

- Identify the root cause of a failure efficiently
- Explain why the failure occurred
- Apply the correct fix without overcorrecting
- Verify the application returns to a healthy state
- Avoid introducing new failures during recovery

## Troubleshooting Framework & Inspection Commands

This lab is not about memorizing commands — it is about **using them in the correct order**.

On the EX280 exam, effective troubleshooting follows a predictable pattern.

---

### The Debugging Order (Memorize This)

Always inspect in this order:

1. **Context & Permissions**
2. **Pod State**
3. **Logs**
4. **Events**
5. **Configuration**
6. **Storage**
7. **Networking**

Jumping ahead often wastes time.

---

### Context & Permissions

Before troubleshooting anything else:

- Verify your current project
- Verify your user identity
- Verify you have permission to modify the resource

Common failures occur simply because you are in the wrong namespace.

---

### Pod State Inspection

Inspect pod status first:

- Pending
- CrashLoopBackOff
- ImagePullBackOff
- Error

Pod state often immediately narrows the problem domain.

---

### Logs (Primary Signal)

Logs usually reveal:
- application errors
- missing configuration
- permission failures
- incorrect environment variables

Always inspect logs **before changing configuration**.

---

### Events (Secondary Signal)

Events often explain:
- scheduling failures
- storage binding issues
- image pull failures

Events provide cluster-level context that logs may not.

---

### Configuration Inspection

If logs point to configuration issues:
- inspect ConfigMaps
- inspect Secrets
- inspect environment variable injection
- inspect volume mounts

Configuration errors are common and often subtle.

---

### Storage Inspection

If pods fail to start or behave unexpectedly:
- verify PVC state
- verify mounts exist
- verify access modes align with pod behavior

Storage failures frequently masquerade as application bugs.

---

### Networking Inspection

If applications run but cannot be accessed:
- inspect Services
- inspect Endpoints
- inspect Routes
- trace traffic path end-to-end

Networking is often the final step, not the first.

---

### Discipline Reminder

- Inspect before modifying
- Change one thing at a time
- Verify after every change

Calm, ordered debugging earns points.

## Guided Troubleshooting Tasks

Complete the following tasks **in order**.  
Treat each task as if it were an exam requirement.

Do not skip inspection steps. Do not “try fixes.”

---

### Task 1 — Identify a Failing Pod

1. Locate a pod that is not in a healthy `Running` state.
2. Identify the pod status (e.g., `Pending`, `CrashLoopBackOff`, `ImagePullBackOff`).
3. Confirm the project and context before proceeding.

You should be able to explain *why* this pod is unhealthy before changing anything.

---

### Task 2 — Inspect Logs and Events

1. Retrieve logs from the failing pod.
2. Identify any error messages or missing dependencies.
3. Inspect recent events related to the pod.

Determine whether the failure is:
- application-level
- configuration-related
- image-related
- scheduling-related

Logs first, events second.

---

### Task 3 — Diagnose a Configuration Failure

Given a pod that fails due to configuration:

1. Inspect referenced ConfigMaps and Secrets.
2. Verify required keys exist.
3. Verify environment variables or volume mounts reference the correct names.
4. Identify the exact misconfiguration.

Do not recreate configuration unless required. Fix the reference.

---

### Task 4 — Diagnose a Storage Failure

Given a pod that fails due to storage:

1. Inspect any referenced PersistentVolumeClaims.
2. Verify PVC state (`Pending` vs `Bound`).
3. Inspect volume mounts in the pod specification.
4. Identify mismatches between access modes and pod behavior.

Explain the failure before correcting it.

---

### Task 5 — Diagnose a Networking Failure

Given a running application that is not reachable:

1. Inspect the Service selector and ports.
2. Verify Service endpoints exist.
3. Inspect the Route configuration.
4. Trace traffic from Route → Service → Pod → Container.

Identify exactly where traffic stops.

---

### Task 6 — Apply a Targeted Fix and Verify Recovery

1. Apply the **minimum change** required to fix the issue.
2. Observe pod or application behavior.
3. Verify the application reaches a healthy state.
4. Confirm no new errors were introduced.

Recovery is not complete until behavior is verified.

## Verification Checklist

Before marking this lab complete, verify the following without hesitation:

- You can identify unhealthy pods and explain their status
- You inspect logs before changing configuration
- You use events to confirm scheduling, image, or storage issues
- You can distinguish between configuration, storage, networking, and permission failures
- You apply minimal, targeted fixes instead of broad changes
- You verify recovery after every fix
- You can explain *why* the issue occurred, not just how you fixed it
- You do not introduce new failures while recovering from existing ones

If any item above feels uncertain or rushed, repeat the relevant task.

---

## Lab Completion Criteria

This lab is complete when:

- You follow a consistent troubleshooting order under pressure
- You inspect before modifying every time
- You avoid panic-driven changes
- You isolate root causes quickly
- You verify behavior after every fix

On the EX280 exam, **how** you troubleshoot matters as much as **what** you fix.  
Calm, methodical recovery earns points. Random fixes do not.

