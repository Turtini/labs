# Lab 02: Projects, Users & RBAC

This lab focuses on **project creation, user access, and role-based access control (RBAC)** in OpenShift.

On the EX280 exam, many tasks fail not because applications are misconfigured, but because **permissions are incorrect or mis-scoped**. This lab builds the precision required to grant exactly the access requested — no more, no less.

RBAC is not a background concern. It directly controls whether your work succeeds or silently fails.

---

## Objectives

By the end of this lab, you will be able to:

- Create OpenShift projects intentionally
- Understand the difference between Roles and ClusterRoles
- Apply RoleBindings and ClusterRoleBindings correctly
- Scope permissions to the correct namespace
- Verify access using `oc auth can-i`
- Diagnose and correct RBAC-related failures

These skills are required for almost every OpenShift exam task.

## Scenario & Constraints

You are working on a shared OpenShift cluster used by multiple teams and environments.

Different users and service accounts require **different levels of access** across **multiple projects**. Some tasks require namespace-scoped permissions, while others require cluster-scoped access.

This lab simulates the RBAC conditions you will encounter on the EX280 exam.

---

### Assumptions

- You have access to an OpenShift cluster
- Your kubeconfig is functional
- At least one non-default user or ServiceAccount exists
- You may not have cluster-admin privileges

You are **not** expected to modify cluster-level authentication configuration.

---

### Constraints

- Permissions must be granted **only** as requested
- Namespace-scoped access must use `Role` and `RoleBinding`
- Cluster-wide access must use `ClusterRole` and `ClusterRoleBinding` **only if required**
- You must verify permissions before assuming success
- You must not rely on the web console

These constraints mirror EX280 exam expectations.

---

### Success Criteria

This lab is complete when you can:

- Create projects with exact names
- Grant precise permissions to users or ServiceAccounts
- Scope access correctly to namespaces or the cluster
- Verify permissions using `oc auth can-i`
- Identify and fix RBAC mistakes without guesswork

## RBAC Concepts & Inspection Commands

This lab requires **precision**, not memorization.  
You must understand *which* RBAC object to use and *where* it applies.

---

### Core RBAC Objects

- **Role**  
  Grants permissions **within a single project (namespace)**.

- **ClusterRole**  
  Grants permissions **cluster-wide** or reusable permissions that can be bound to a namespace.

- **RoleBinding**  
  Assigns a **Role or ClusterRole** to a subject **within a specific project**.

- **ClusterRoleBinding**  
  Assigns a **ClusterRole** to a subject **across the entire cluster**.

---

### Scoping Rules (Memorize These)

- Namespace-scoped access → `Role` + `RoleBinding`
- Cluster-wide access → `ClusterRole` + `ClusterRoleBinding`
- Reusing a ClusterRole in one namespace → `RoleBinding` (not ClusterRoleBinding)

Over-scoping permissions is a common exam deduction.

---

### RBAC Inspection Commands

Inspect existing roles in the current project:

- `oc get roles`
- `oc describe role <role-name>`

Inspect cluster roles:

- `oc get clusterroles`
- `oc describe clusterrole <clusterrole-name>`

Inspect bindings in a project:

- `oc get rolebindings`
- `oc describe rolebinding <binding-name>`

Inspect cluster-wide bindings:

- `oc get clusterrolebindings`
- `oc describe clusterrolebinding <binding-name>`

---

### Permission Verification (Critical)

Before and after applying RBAC, verify permissions:

- `oc auth can-i <verb> <resource>`
- `oc auth can-i <verb> <resource> -n <project>`
- `oc auth can-i <verb> <resource> --as=<user> -n <project>`

Verification prevents silent failures and wasted debugging time.

---

### RBAC Discipline

- Grant the **minimum** permissions required
- Verify access immediately after binding
- If something fails, check RBAC before checking the application

RBAC correctness determines whether your work is even allowed to run.

## Guided Tasks

Complete the following tasks **in order**.  
Treat each task as if it were an exam requirement.

Do not skip verification steps.

---

### Task 1 — Create Projects

1. Create two new projects:
   - One representing a **development** environment
   - One representing a **production** environment

2. Verify both projects exist.
3. Switch between projects and confirm context each time.

Projects must be created with **exact names**. Naming accuracy matters on the exam.

---

### Task 2 — Inspect Default Roles

In one of the projects you created:

1. List available Roles.
2. Identify common default roles such as:
   - `admin`
   - `edit`
   - `view`

3. Inspect the permissions granted by one Role.

Understanding what already exists often prevents unnecessary custom RBAC.

---

### Task 3 — Grant Namespace-Scoped Access

Choose a user or ServiceAccount.

1. Grant that subject **edit** access to the development project.
2. Verify that the subject:
   - Can create pods
   - Can create deployments
   - Cannot access resources in the production project

Use permission checks to confirm behavior before proceeding.

---

### Task 4 — Mis-scope Permissions (Intentional Error)

Intentionally introduce an RBAC mistake:

1. Grant broader permissions than required (for example, cluster-wide access).
2. Verify that the subject now has unintended access.

This simulates a common exam error.

---

### Task 5 — Correct the RBAC Scope

1. Identify the incorrect binding.
2. Remove or adjust it.
3. Re-apply permissions using the correct scope.
4. Verify that access is now limited to the intended project.

Precision matters more than generosity.

---

### Task 6 — Final Permission Verification

For each project:

1. Verify which actions the subject can perform.
2. Verify which actions are denied.
3. Confirm behavior matches the task intent exactly.

If permissions are unclear, revisit the bindings.

## Verification Checklist

Before marking this lab complete, verify the following without hesitation:

- You can list all projects you created and switch between them intentionally
- You can identify which Roles and ClusterRoles are available by default
- You can explain why a Role or ClusterRole was chosen for each task
- You can confirm permissions using `oc auth can-i`
- You can identify RBAC mistakes and correct them confidently
- No user or ServiceAccount has broader access than required

If any item above feels uncertain, repeat the relevant task.

---

## Lab Completion Criteria

This lab is complete when:

- You can choose the correct RBAC object without guessing
- You scope permissions intentionally to the correct project or cluster
- You verify access before and after every change
- You recognize RBAC-related failures quickly
- You correct permission mistakes calmly and precisely

RBAC precision is a **graded skill** on the EX280 exam and will be assumed in all future labs.
