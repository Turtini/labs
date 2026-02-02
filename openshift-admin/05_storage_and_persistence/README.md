# Lab 05: Storage & Persistence

This lab focuses on **persistent storage in OpenShift**, including the creation, attachment, and verification of PersistentVolumeClaims (PVCs).

On the EX280 exam, storage-related tasks often fail because candidates stop at “PVC exists” and do not verify that storage is **mounted and actively used** by the application.

This lab builds the discipline required to validate storage end-to-end: from claim creation to application behavior.

---

## Objectives

By the end of this lab, you will be able to:

- Create PersistentVolumeClaims with correct specifications
- Understand StorageClasses and access modes
- Attach persistent storage to applications
- Verify that PVCs are bound and mounted
- Confirm that applications read from and write to persistent storage
- Identify and recover from common storage-related failures

These skills are directly tested on the EX280 exam and often carry partial credit.

## Scenario & Constraints

You are responsible for deploying applications that require **persistent storage**.

Applications may write data that must survive pod restarts, rescheduling, or scaling events. OpenShift provides this capability through PersistentVolumeClaims backed by cluster storage.

This lab simulates storage-related tasks commonly found on the EX280 exam.

---

### Assumptions

- You have access to an OpenShift cluster with at least one functional StorageClass
- Your kubeconfig is configured and working
- You can deploy applications in at least one project
- Dynamic provisioning is available on the cluster

You are **not** expected to create PersistentVolumes manually.

---

### Constraints

- Storage must be provisioned using PersistentVolumeClaims
- PVC specifications (size, access mode, StorageClass) must match requirements exactly
- Storage must be **mounted into the application**
- The application must actively use the mounted storage
- You must verify PVC state and application behavior using `oc` commands
- You must not rely on the web console

These constraints mirror EX280 exam expectations.

---

### Success Criteria

This lab is complete when you can:

- Create PVCs with correct specifications
- Verify PVCs reach the `Bound` state
- Mount PVCs into applications at the correct path
- Confirm data persists across pod restarts
- Detect and fix storage that exists but is unused

## Storage Concepts (Exam-Aligned)

This lab tests your ability to provision, attach, and **verify persistent storage** correctly.

On the EX280 exam, storage tasks are graded end-to-end.  
A PVC that exists but is not mounted — or mounted but unused — does not fully satisfy the requirement.

---

### PersistentVolumeClaims (PVCs)

A PersistentVolumeClaim is a request for storage resources.

Key attributes you must get right:
- **Name**
- **Requested size**
- **Access mode**
- **StorageClass** (if specified)

If any of these are incorrect, the PVC may not bind or may not meet the task requirements.

---

### StorageClasses

StorageClasses define how storage is dynamically provisioned.

Important expectations:
- A default StorageClass may exist
- A specific StorageClass may be required by the task
- Using the wrong StorageClass can result in a PVC that binds but does not meet requirements

Always inspect available StorageClasses before creating a PVC.

---

### Access Modes (What Matters)

Common access modes you may encounter:
- `ReadWriteOnce` (RWO)
- `ReadOnlyMany` (ROX)
- `ReadWriteMany` (RWX)

The access mode must match the task intent and the cluster’s capabilities.

---

### Mounting Storage into Applications

Creating a PVC is only the first step.

To receive full credit:
- The PVC must be mounted into the pod
- The mount path must be correct
- The application must be able to read from or write to the mount

A bound PVC that is not mounted earns partial credit at best.

---

### Persistence Verification

You must be able to demonstrate persistence by:
- Writing data to the mounted path
- Restarting or recreating the pod
- Confirming the data still exists

If persistence cannot be demonstrated, the requirement is not met.

---

### Discipline Reminder

- Inspect StorageClasses before creating PVCs
- Verify PVC state (`Pending` vs `Bound`)
- Confirm mounts inside the running pod
- Prove persistence, do not assume it

Bound ≠ mounted ≠ used.

## Guided Tasks

Complete the following tasks **in order**.  
Treat each task as if it were an exam requirement.

Do not skip verification steps.

---

### Task 1 — Inspect Available StorageClasses

1. List available StorageClasses.
2. Identify the default StorageClass (if one exists).
3. Identify any non-default StorageClasses available.

Before creating any PVCs, you should know **which StorageClasses exist** and which one you intend to use.

---

### Task 2 — Create a PersistentVolumeClaim

1. Create a PersistentVolumeClaim with:
   - A specific name
   - A defined storage size
   - The required access mode
   - The correct StorageClass (if specified)

2. Verify the PVC exists.
3. Verify the PVC reaches the `Bound` state.

Do not proceed until the PVC is bound.

---

### Task 3 — Mount the PVC into an Application

1. Deploy or select an existing application.
2. Mount the PVC into the application at a specific path.
3. Trigger a rollout if required.
4. Verify the pod starts successfully.

After deployment:
- Confirm the volume is mounted inside the pod
- Confirm the mount path matches the task requirement

---

### Task 4 — Verify Persistence

1. Write a file to the mounted storage path from inside the pod.
2. Delete the pod or trigger a rollout.
3. Verify a new pod is created.
4. Confirm the file still exists at the mounted path.

This step proves persistence across pod lifecycle events.

---

### Task 5 — Scale and Observe Behavior

1. Scale the application to multiple replicas (if supported).
2. Observe pod behavior related to storage access.
3. Confirm the behavior matches the access mode of the PVC.

If scaling is not supported due to access mode, you should be able to explain why.

---

### Task 6 — Introduce and Recover from a Storage Error

Intentionally introduce a storage-related misconfiguration, such as:
- Incorrect mount path
- Referencing a non-existent PVC
- Using an incorrect access mode

Then recover by:
1. Identifying the failure using inspection commands
2. Correcting the configuration
3. Verifying the application returns to a healthy state

Recovery is part of the exam skill set.

## Verification Checklist

Before marking this lab complete, verify the following without hesitation:

- You can list available StorageClasses and identify the default
- You can create a PersistentVolumeClaim with the correct name, size, access mode, and StorageClass
- You can verify that the PVC reaches the `Bound` state
- You can mount the PVC into an application at the correct path
- You can verify the mount exists inside the running pod
- You can write data to the mounted path
- You can restart or recreate the pod and confirm the data persists
- You can explain application behavior when scaling with different access modes
- You can identify and fix common storage misconfigurations

If any item above feels uncertain or slow, repeat the relevant task.

---

## Lab Completion Criteria

This lab is complete when:

- You treat storage as an end-to-end requirement
- You never stop at “PVC exists”
- You always verify that storage is mounted and used
- You can prove persistence across pod restarts
- You recover from storage-related failures calmly and methodically

On the EX280 exam, storage that is **bound but not used** earns partial credit at best.  
Verified, persistent storage earns points.

