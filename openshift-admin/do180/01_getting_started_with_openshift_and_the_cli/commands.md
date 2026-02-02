# DO180 Lab 01 – Commands Reference

Type these commands manually.  
Do not copy/paste during practice unless explicitly noted.

---

## 1. Verify the oc CLI

Confirm that the OpenShift CLI is installed and accessible.

```bash
oc version
```

Verify that:

Client information is displayed

Server information appears once logged in

---

## 2. Log In to the Cluster

Log in using the method provided by your environment.

```bash
oc login
```

Or, if using a token:

oc login --token=<TOKEN> --server=<API_URL>

---

## 3. Verify Identity

Confirm which user you are authenticated as.

```bash
oc whoami
```

This identity determines what actions you are allowed to perform.

---

## 4. Check Current Project

Display the currently active project.

```bash
oc project
```

List all projects you have access to:

```bash
oc get projects
```

---

## 5. Switch Projects

Switch to a different project you have access to.

```bash
oc project <project-name>
```

Verify the switch:

```bash
oc project
```

Never assume context — always confirm.

---

## 6. Inspect Cluster Resources

List pods in the current project:

```bash
oc get pods
```

List services:

```bash
oc get services
```

List common resources:

```bash
oc get all
```

---

## 7. Describe a Resource

Choose a pod and inspect it in detail.

```bash
oc describe pod <pod-name>
```

Pay attention to:

Status

Conditions

Events

---

## 8. Use oc explain

Explore resource definitions directly from the API.

```bash
oc explain pod
```

Drill deeper:

```bash
oc explain pod.spec
oc explain pod.spec.containers
```

This is a critical skill for OpenShift administrators.

---

## Verification Checklist

- Before moving on, confirm you can answer:

- Who am I logged in as?

- What project am I currently using?

- How do I verify both?

- Where do errors and events appear?

---

## Cleanup

No cleanup is required for this lab.
