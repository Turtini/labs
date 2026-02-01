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
