# DO180 Lab 02 – Commands Reference

Type these commands manually.  
Do not copy/paste during practice unless explicitly noted.

---

## 1. List Available Projects

Display all projects you have access to:

```bash
oc get projects
```

Verify that you recognize at least one project you are permitted to use.

---

## 2. Check Current Project Context

Identify the active project:

```bash
oc project
```

Never assume context. Always verify.

---

## 3. Switch Projects

Switch to an existing project:

```bash
oc project <project-name>
```

Confirm the change:

```bash
oc project
```

---

## 4. Create a New Project (If Permitted)

Create a new project:

```bash
oc new-project <project-name>
```

Verify the project exists and is active:

```bash
oc project
oc get projects
```

If project creation is denied, note the error and continue using an existing project.

---

## 5. Inspect Access and Permissions

Attempt to list resources in the project:

```bash
oc get pods
```

If access is denied, observe the error message and note the reason.

Check whether you can create resources:

```bash
oc auth can-i create pods
```

Check read access:

```bash
oc auth can-i get pods
```

---

## 6. Verify Role Awareness

List role bindings in the project (read-only inspection):

```bash
oc get rolebindings
```

You are not required to modify role bindings in this lab.

---

## Verification Checklist

Before moving on, confirm you can answer:

- What project am I currently in?

- How do I verify my access level?

- How do permission errors present themselves?

- How do I confirm whether I can perform an action before trying it?

---

## Cleanup

If you created a project and your environment requires cleanup, delete it:

```bash
oc delete project <project-name>
```

Only do this if explicitly instructed by your environment.
