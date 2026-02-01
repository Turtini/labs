# Lab 01: Cluster Access & Context

This lab focuses on **cluster access, user identity, and project context** — the most common source of silent failure on the OpenShift Administration (EX280) exam.

Before you can configure applications, storage, or networking, you must be able to reliably answer three questions:

1. Who am I logged in as?
2. Which project am I operating in?
3. What permissions do I have in this context?

This lab builds the habits required to answer those questions **every time**, under exam pressure.

---

## Objectives

By the end of this lab, you will be able to:

- Verify your OpenShift user identity
- Inspect and understand kubeconfig context
- Switch projects intentionally
- Confirm permissions before performing actions
- Detect and recover from context-related mistakes

These skills are foundational and will be assumed in all subsequent labs.

## Scenario & Constraints

You have been granted access to an existing OpenShift cluster used by multiple teams.

During the exam, you will be required to perform tasks across **multiple projects** and **multiple permission scopes**. Mistakes made early due to incorrect context often cause cascading failures later.

This lab simulates that environment.

---

### Assumptions

- You already have access to an OpenShift cluster
- Your `kubeconfig` is configured and functional
- You may be logged in as a non-admin user
- Multiple projects already exist on the cluster

You are **not** expected to create or destroy the cluster itself.

---

### Constraints

- You must not assume your current project
- You must not assume your current user
- You must verify context before performing any action
- You must rely on `oc` commands only (no web console)

These constraints mirror EX280 exam conditions.

---

### Success Criteria

This lab is complete when you can:

- Confidently identify your active user and context
- Switch projects intentionally and verify the change
- Confirm permissions before attempting modifications
- Recognize and correct context-related errors without guesswork

## Required Commands & Inspection Techniques

This lab emphasizes **inspection before action**.

You should be able to answer the following questions *without hesitation*:

- Who am I logged in as?
- What cluster context am I using?
- Which project is currently active?
- What permissions do I have here?

---

### Core Identity & Context Commands

Use these commands **frequently** and **intentionally**.

- Display the current user:
  - `oc whoami`

- Display the current project:
  - `oc project`

- View current context information:
  - `oc config current-context`

- Inspect all configured contexts:
  - `oc config get-contexts`

These commands are read-only and safe to run at any time.

---

### Project Inspection

Before switching projects, list what is available:

- `oc get projects`

After switching, always confirm:

- `oc project <project-name>`
- `oc project`

Never assume a project switch succeeded without verification.

---

### Permission Inspection

Before performing write operations, confirm permissions:

- `oc auth can-i <verb> <resource>`
- `oc auth can-i <verb> <resource> -n <namespace>`

For example:
- Can you create pods?
- Can you create deployments?
- Can you modify routes?

Permission checks prevent wasted time debugging failures caused by access restrictions.

---

### Inspection Discipline

- Inspect before creating
- Inspect after switching context
- Inspect again before verification

Context checks should become **automatic muscle memory**.

## Guided Tasks

Complete the following tasks **in order**.  
Treat each task as if it were an exam requirement.

Do not skip verification steps.

---

### Task 1 — Verify Identity and Context

1. Confirm the user you are logged in as.
2. Confirm the active project.
3. Confirm the current kubeconfig context.

You should be able to state, out loud:
- your username
- your current project
- your active context

If any of these are unclear, stop and investigate before proceeding.

---

### Task 2 — Inspect Available Projects

1. List all projects you have access to.
2. Identify at least two projects you can switch into.
3. Choose one project and switch to it.

After switching:
- Verify the active project explicitly
- Do not assume the switch succeeded

---

### Task 3 — Verify Permissions in the New Project

In the project you just switched to:

1. Check whether you can create pods.
2. Check whether you can create deployments.
3. Check whether you can create services.

Record which actions are allowed and which are denied.

This step simulates exam tasks where permissions differ per project.

---

### Task 4 — Recover from a Context Mistake

Intentionally create a context error:

1. Switch to a different project than intended.
2. Attempt an action that should fail or behave unexpectedly.

Then recover by:
- Identifying the incorrect context
- Switching back to the correct project
- Re-verifying identity and permissions

This recovery pattern is more important than avoiding mistakes.

---

### Task 5 — Final Context Confirmation

Before declaring the lab complete:

1. Confirm your user identity
2. Confirm your active project
3. Confirm your permissions in that project

If you cannot answer all three confidently, repeat the tasks.

## Verification Checklist

Before marking this lab complete, verify the following without hesitation:

- You can identify your current user using `oc whoami`
- You can identify your active project using `oc project`
- You can identify your active kubeconfig context
- You can list available projects and switch between them intentionally
- You can confirm permissions using `oc auth can-i`
- You can detect and recover from context-related errors quickly

If any item above feels uncertain or slow, repeat the relevant task.

---

## Lab Completion Criteria

This lab is complete when:

- Context checks feel automatic
- You no longer assume identity or project
- You verify permissions before taking action
- You can recover from mistakes calmly and quickly

These habits are foundational and will be assumed in all future labs.

