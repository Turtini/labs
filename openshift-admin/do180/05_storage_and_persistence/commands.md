# DO180 Lab 05 – Commands Reference

Type these commands manually.  
Do not copy/paste during practice unless explicitly noted.

---

## 1. Verify Project Context

Confirm you are in the correct project before working with storage.

```bash
oc project
```

If needed:

```bash
oc project <project-name>
```

---

## 2. Inspect Storage Classes (Cluster-Provided)

List available StorageClasses:

```bash
oc get storageclass
```

Identify the default StorageClass (look for (default)).

---

## 3. Create a PersistentVolumeClaim (PVC)

Create a PVC using the default StorageClass:

```bash
oc create -f - <<'EOF'
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: app-data
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
EOF
```

Verify the PVC:

```bash
oc get pvc
oc describe pvc app-data
```

Expected:

Status becomes Bound (may take a moment)

---

## 4. Attach the PVC to an Application

If you have an existing deployment, add the volume and mount.

Add a volume to the deployment:

```bash
oc set volume deployment/<deployment-name> --add --name=app-data --type=pvc --claim-name=app-data --mount-path=/data
```

Watch pods restart / roll out:

```bash
oc get pods
```

---

## 5. Verify the Volume Mount Inside the Pod

Identify a running pod:

```bash
oc get pods
```

Verify the mount exists:

```bash
oc exec <pod-name> -- df -h | grep /data
```

Write a test file:

```bash
oc exec <pod-name> -- sh -c 'date > /data/persist-test.txt && cat /data/persist-test.txt'
```

---

## 6. Prove Persistence Across Pod Restart

Delete the pod (deployment will recreate it):

```bash
oc delete pod <pod-name>
```

Wait for a new pod to become Running/Ready:

```bash
oc get pods -w
```

Once the new pod is ready, verify the file still exists:

```bash
oc exec <new-pod-name> -- cat /data/persist-test.txt
```

If the file is present, persistence is working.

---

## Verification Checklist

Before moving on, confirm you can answer:

- What is the difference between a PV and a PVC?

- How do you know a PVC is usable?

- How do you prove data persists beyond pod lifecycle?

- Why is local pod filesystem not sufficient for persistent data?

---

## Cleanup

If required by your environment, remove the volume mount:

```bash
oc set volume deployment/<deployment-name> --remove --name=app-data
```

Optionally delete the PVC:

```bash
oc delete pvc app-data
```

Only perform cleanup if explicitly instructed.
