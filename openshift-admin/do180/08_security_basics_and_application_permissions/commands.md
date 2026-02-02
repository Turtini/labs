# DO180 Lab 08 – Commands Reference

Type these commands manually.  
Do not copy/paste during practice unless explicitly noted.

---

## 1. Verify Project Context

Confirm you are in the correct project before inspecting security behavior.

```bash
oc project
```

If needed:

```bash
oc project <project-name>
```

---

## 2. Identify a Running Pod

List pods and select one that is Running/Ready:

```bash
oc get pods
```

---

## 3. Inspect Pod Security Context (High-Level)

Describe the pod and look for security-related details:

```bash
oc describe pod <pod-name>
```

Pay attention to:

SecurityContext settings (if shown)

Volumes and mount permissions

Events related to permission denials

---

## 4. Confirm the Runtime User Inside the Container

Check which user the container is running as:

```bash
oc exec <pod-name> -- id
```

Confirm whether it is running as non-root (common default):

```bash
oc exec <pod-name> -- id -u
```

---

## 5. Test Filesystem Permissions (Safe Validation)

Check common writable locations:

```bash
oc exec <pod-name> -- sh -c 'touch /tmp/security-test.txt && ls -l /tmp/security-test.txt'
```

Attempt to write in a protected directory (this should fail in many cases):

```bash
oc exec <pod-name> -- sh -c 'touch /root/security-test.txt'
```

Observe the error message. Do not attempt to bypass security controls.

---

## 6. Inspect Service Account (Application Identity)

View the service account associated with the pod:

```bash
oc get pod <pod-name> -o jsonpath='{.spec.serviceAccountName}{"\n"}'
```

List service accounts in the project:

```bash
oc get serviceaccounts
```

Service accounts represent how workloads authenticate to the cluster API.

---

## 7. Recognize Common Security Signals

If an application fails due to permissions, common signals include:

"permission denied" errors in logs

pods failing to start due to restricted security assumptions

inability to write to container filesystem paths

Check logs if needed:

```bash
oc logs <pod-name>
```

---

## Verification Checklist

Before completing the track, confirm you can answer:

- Why does OpenShift prefer non-root containers?

- How do you prove what user a container runs as?

- How do filesystem permissions affect application behavior?

- What evidence would you use before requesting elevated permissions?

---

## Cleanup

If you created test files, remove them:

```bash
oc exec <pod-name> -- rm -f /tmp/security-test.txt
```

No other cleanup is required.
