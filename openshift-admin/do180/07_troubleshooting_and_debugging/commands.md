# DO180 Lab 07 – Commands Reference

Type these commands manually.  
Do not copy/paste during practice unless explicitly noted.

---

## 1. Verify Project Context

Confirm you are in the correct project before troubleshooting.

```bash
oc project
```

If needed:

```bash
oc project <project-name>
```

---

## 2. Identify Failing or Unhealthy Pods

List all pods and review their status:

```bash
oc get pods
```

Look for pods in states such as:

CrashLoopBackOff

Error

ImagePullBackOff

Pending

---

## 3. Describe a Problematic Pod

Choose a pod that is not running correctly and inspect it:

```bash
oc describe pod <pod-name>
```

Pay close attention to:

Events (near the bottom)

Container state

Restart count

Error messages

Events often explain why a pod is failing.

---

## 4. Review Container Logs

Retrieve logs from the container:

```bash
oc logs <pod-name>
```

If the pod has restarted, view logs from the previous container instance:

```bash
oc logs <pod-name> --previous
```

Logs are the primary signal for application-level issues.

---

## 5. Inspect Deployment Status

If the pod is managed by a deployment, inspect it:

```bash
oc get deployment
oc describe deployment <deployment-name>
```

Look for:

Replica availability

Failed rollout conditions

Image or configuration issues

---

## 6. Debug a Running Pod

Start a debug session for a running pod:

```bash
oc exec -it <pod-name> -- /bin/sh
```

Inside the container, you may check:

Environment variables

Filesystem paths

Configuration files

Exit the container when finished:

```bash
exit
```

---

## 7. Inspect Resource Relationships

Verify which pods belong to which deployment:

```bash
oc get pods --show-labels
```

Verify which pods a service selects:

```bash
oc get service <service-name> -o yaml
```

Confirm endpoints are populated:

```bash
oc get endpoints <service-name>
```

---

## Verification Checklist

Before moving on, confirm you can answer:

- Why is this pod failing?

- Which signal identified the failure first?

- Do events support what logs show?

- What would you fix before restarting or redeploying?

---

## Cleanup

No cleanup is required for this lab.

If you modified configuration during troubleshooting, ensure it is returned to its expected state.
